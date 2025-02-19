---
title: Windows.EventLogs.AlternateLogon
hidden: true
tags: [Client Artifact]
---

Logon specifying alternate credentials - if NLA enabled on
destination Current logged-on User Name Alternate User Name
Destination Host Name/IP Process Name


```yaml
name: Windows.EventLogs.AlternateLogon
description: |
  Logon specifying alternate credentials - if NLA enabled on
  destination Current logged-on User Name Alternate User Name
  Destination Host Name/IP Process Name

reference:
  - https://digital-forensics.sans.org/media/SANS_Poster_2018_Hunt_Evil_FINAL.pdf

precondition: SELECT OS From info() where OS = 'windows'

parameters:
  - name: securityLogFile
    default: C:/Windows/System32/Winevt/Logs/Security.evtx

sources:
  - query: |
      SELECT EventData.IpAddress AS IpAddress,
               EventData.IpPort AS Port,
               EventData.ProcessName AS ProcessName,
               EventData.SubjectUserSid AS SubjectUserSid,
               EventData.SubjectUserName AS SubjectUserName,
               EventData.TargetUserName AS TargetUserName,
               EventData.TargetServerName AS TargetServerName,
               System.TimeCreated.SystemTime AS LogonTime
      FROM parse_evtx(filename=securityLogFile)
      WHERE System.EventID.Value = 4648
        AND EventData

```
