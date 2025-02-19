---
title: Linux.Forensics.Journal
hidden: true
tags: [Client Artifact]
---

Parses the binary journal logs. Systemd uses a binary log format to
store logs. You can read these logs using journalctl command:

`journalctl --file /run/log/journal/*/*.journal`

This artifact uses the Velociraptor Binary parser to parse the
binary format. The format is documented
https://www.freedesktop.org/wiki/Software/systemd/journal-files/


```yaml
name: Linux.Forensics.Journal
description: |
  Parses the binary journal logs. Systemd uses a binary log format to
  store logs. You can read these logs using journalctl command:

  `journalctl --file /run/log/journal/*/*.journal`

  This artifact uses the Velociraptor Binary parser to parse the
  binary format. The format is documented
  https://www.freedesktop.org/wiki/Software/systemd/journal-files/

parameters:
- name: JournalGlob
  type: glob
  description: A Glob expression for finding journal files.
  default: /run/log/journal/*/*.journal

- name: OnlyShowMessage
  type: bool
  description: If set we only show the message entry (similar to syslog).

- name: AlsoUpload
  type: bool
  description: If set we also upload the raw files.

export: |
    LET JournalProfile = '''[
    ["Header", "x=>x.header_size", [
      ["Signature", 0, "String", {
          "length": 8,
      }],
      ["header_size", 88, "uint64"],
      ["arena_size", 96, "uint64"],
      ["n_objects", 144, uint64],
      ["n_entries", 152, uint64],
      ["Objects", "x=>x.header_size", "Array", {
          "type": "ObjectHeader",
          "count": "x=>x.n_objects",
          "max_count": 100000
      }]
    ]],

    ["ObjectHeader", "x=>x.size", [
     ["Offset", 0, "Value", {
        "value": "x=>x.StartOf",
     }],
     ["type", 0, "Enumeration",{
         "type": "uint8",
         "choices": {
          "0": OBJECT_UNUSED,
          "1": OBJECT_DATA,
          "2": OBJECT_FIELD,
          "3": OBJECT_ENTRY,
          "4": OBJECT_DATA_HASH_TABLE,
          "5": OBJECT_FIELD_HASH_TABLE,
          "6": OBJECT_ENTRY_ARRAY,
          "7": OBJECT_TAG,
         }
     }],
     ["flags", 1, "uint8"],
     ["__real_size", 8, "uint64"],
     ["__round_size", 8, "Value", {
         "value": "x=>int(int=x.__real_size / 8) * 8",
     }],
     ["size", 0, "Value", {
         "value": "x=>if(condition=x.__real_size = x.__round_size, then=x.__round_size, else=x.__round_size + 8)",
     }],
     ["payload", 16, Union, {
         "selector": "x=>x.type",
         "choices": {
             "OBJECT_DATA": DataObject,
             "OBJECT_ENTRY": EntryObject,
         }
     }]
    ]],
    ["DataObject", 0, [
      ["payload", 48, String]
    ]],

    # This is basically a single log line -
    # it is really a list of references to data Objects
    ["EntryObject", 0, [
      ["seqnum", 0, "uint64"],
      ["realtime", 8, "uint64"],
      ["monotonic", 16, "uint64"],
      ["items", 48, Array, {
          "type": EntryItem,
          "count": 50,
          "sentinel": "x=>x.object.payload = NULL",
      }]
    ]],
    ["EntryItem", 16, [
     ["object", 0, "Pointer", {
         "type": "ObjectHeader",
     }],
    ]]
    ]
    '''

    -- We make a quick pass over the file to get all the OBJECT_ENTRY
    -- objects which are all we care about. By extracting Just the
    -- offsets of the OBJECT_ENTRY Objects in the first pass we can
    -- free memory we wont need.
    LET Offsets(File) = SELECT Offset
      FROM foreach(row=parse_binary(filename=File, profile=JournalProfile,
         struct="Header").Objects)
      WHERE type = "OBJECT_ENTRY"

    -- Now parse the ObjectEntry in each offset
    LET _ParseFile(File) = SELECT Offset,
        parse_binary(
         filename=File, profile=JournalProfile,
         struct="ObjectHeader", offset=Offset) AS Parsed
    FROM Offsets(File=File)

    -- Extract the timestamps and all the attributes
    LET ParseFile(File) = SELECT File, Offset,
       timestamp(epoch=Parsed.payload.realtime) AS Timestamp,
       Parsed.payload.items.object.payload.payload AS Data
    FROM _ParseFile(File=File)

sources:
- query: |
    SELECT * FROM foreach(row={
      SELECT OSPath FROM glob(globs=JournalGlob)
    }, query={
      SELECT *, if(condition=OnlyShowMessage,
          then=filter(list=Data, regex="^MESSAGE=")[0], else=Data) AS Data,
          if(condition=AlsoUpload, then=upload(file=File)) AS Upload
      FROM ParseFile(File=OSPath)
    })

```
