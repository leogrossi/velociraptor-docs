---
title: Linux.Triage.ProcessMemory
hidden: true
tags: [Client Artifact]
---

Dump process memory and upload to the server


```yaml
name: Linux.Triage.ProcessMemory
description: |
  Dump process memory and upload to the server

precondition: SELECT OS From info() where OS = 'linux'

parameters:
  - name: processPid
    type: int
    default: 2215

sources:
  - query: |
      SELECT Name as ProcessName, CommandLine, Pid,
             upload(file=format(format="/%d", args=processPid),
                    accessor="process") as CrashDump
      FROM pslist(pid=processPid)

```
