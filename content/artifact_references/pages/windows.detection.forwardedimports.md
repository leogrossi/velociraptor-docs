---
title: Windows.Detection.ForwardedImports
hidden: true
tags: [Client Artifact]
---

In Windows a common DLL hooking technique is to replace a dll with a
forwarder dll - i.e. one that forwards all imports to the real
dll. If the forwarder DLL is placed earlier in the import order, the
malicous DLL will be seamlessly loaded and injected into another
process.

This artifact searches for dlls which are named the same as the DLL
they are forwarding to.


```yaml
name: Windows.Detection.ForwardedImports
description: |
  In Windows a common DLL hooking technique is to replace a dll with a
  forwarder dll - i.e. one that forwards all imports to the real
  dll. If the forwarder DLL is placed earlier in the import order, the
  malicous DLL will be seamlessly loaded and injected into another
  process.

  This artifact searches for dlls which are named the same as the DLL
  they are forwarding to.

reference:
  - https://github.com/monoxgas/Koppeling
  - https://silentbreaksecurity.com/adaptive-dll-hijacking/
  - https://www.mdsec.co.uk/2020/10/i-live-to-move-it-windows-lateral-movement-part-3-dll-hijacking/

parameters:
  - name: DLLGlob
    default: C:\windows\**\*.dll
  - name: ExcludeRegex
    default: WinSXS|Servicing
    type: regex

sources:
  - query: |
      LET DLLs = SELECT OSPath, Name,
             parse_pe(file=OSPath).Forwards AS Forwards,

             -- Remove the .dll extension if present to get the bare dll filename.
             lowcase(string=parse_string_with_regex(
                  regex="^(?P<BareName>[^.]+)", string=Name).BareName) AS DLLBareName

        FROM glob(globs=DLLGlob)
        WHERE NOT OSPath =~ ExcludeRegex

      -- Speed up analysis a bit by using more workers.
      SELECT * FROM foreach(row=DLLs, workers=20,
        query={
           SELECT OSPath AS DllPath, ForwardedImport,

                  -- The Bare DLL Name from the forwarded name
                  Parse.DllPath AS DllImportPath,

                  -- The export this is forwarding to.
                  Parse.Export AS DLLExportFunc,
                  DLLBareName,

                  -- The bare dll name the export is referring to.
                  basename(path=lowcase(string=Parse.DllPath)) AS ExportDLLName
           FROM foreach(row=Forwards,
             query={
                 SELECT parse_string_with_regex(
                               regex="(?P<DllPath>.+)\\.(?P<Export>[^.]+$)",
                               string=_value) AS Parse,
                        _value AS ForwardedImport
                 FROM scope()
             })

          -- Only flag imports for forwarder dll name the same as its own dll.
          WHERE ExportDLLName = DLLBareName
      })

```
