---
title: Windows.Persistence.PowershellRegistry
hidden: true
tags: [Client Artifact]
---

A common way of persistence is to install a hook into a user profile
registry hive, using powershell. When the user logs in, the
powershell script downloads a payload and executes it.

This artifact searches the user's profile registry hive for
signatures related to general Powershell execution. We use a yara
signature specifically targeting the user's profile which we extract
using raw NTFS parsing (in case the user is currently logged on and
the registry hive is locked).


```yaml
name: Windows.Persistence.PowershellRegistry
description: |
  A common way of persistence is to install a hook into a user profile
  registry hive, using powershell. When the user logs in, the
  powershell script downloads a payload and executes it.

  This artifact searches the user's profile registry hive for
  signatures related to general Powershell execution. We use a yara
  signature specifically targeting the user's profile which we extract
  using raw NTFS parsing (in case the user is currently logged on and
  the registry hive is locked).

parameters:
  - name: yaraRule
    type: yara
    default: |
      rule PowerShell {
        strings:
          $a = /ActiveXObject.{,500}eval/ wide nocase

        condition:
          any of them
      }
  - name: userRegex
    default: .
    type: regex

sources:
  - precondition:
      SELECT OS From info() where OS = 'windows'
    query: |
        SELECT * from foreach(
        row={
          SELECT Name,
                 expand(path=Directory) AS HomeDir
          FROM Artifact.Windows.Sys.Users()
          WHERE HomeDir and Gid AND Name =~ userRegex
        },
        query={
          SELECT File.OSPath As OSPath,
                 String.Offset AS Off,
                 String.HexData As Hex,
                 upload(file=File.FullPath, accessor="auto") AS Upload
              FROM yara(
              files=HomeDir + "\\ntuser.dat",
              rules=yaraRule, context=50)
        })

```
