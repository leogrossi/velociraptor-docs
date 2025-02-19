---
title: Windows.EventLogs.Cleared
hidden: true
tags: [Client Artifact]
---

Extract Event Logs related to EventLog clearing
- Security Log  - EventID 1102
- System Log - EventID 104


```yaml
name: Windows.EventLogs.Cleared
author: Matt Green - @mgreen27

description: |
  Extract Event Logs related to EventLog clearing
  - Security Log  - EventID 1102
  - System Log - EventID 104

reference:
  - https://attack.mitre.org/versions/v6/techniques/T1070/

type: CLIENT

parameters:
  - name: TargetGlob
    default: C:\Windows\System32\Winevt\Logs\{System,Security}.evtx
  - name: DateAfter
    type: timestamp
    description: "search for events after this date. YYYY-MM-DDTmm:hh:ssZ"
  - name: DateBefore
    type: timestamp
    description: "search for events before this date. YYYY-MM-DDTmm:hh:ssZ"

  - name: VSSAnalysisAge
    type: int
    default: 0
    description: |
      If larger than zero we analyze VSS within this many days
      ago. (e.g 7 will analyze all VSS within the last week).  Note
      that when using VSS analysis we have to use the ntfs accessor
      for everything which will be much slower.

sources:
  - query: |
      SELECT
        EventTime,
        UserData.LogFileCleared.Channel || Channel as ClearedLog,
        Message,
        UserData.LogFileCleared.SubjectDomainName + "\\" + UserData.LogFileCleared.SubjectUserName as Username,
        UserData.LogFileCleared.SubjectUserSid || UserSID as UserSID,
        dict(
            EventTime=EventTime,
            Computer=Computer,
            Channel=Channel,
            EventID=EventID,
            EventRecordID=EventRecordID,
            OSPath=OSPath,
            UserData=UserData
        ) as EventData
      FROM Artifact.Windows.EventLogs.EvtxHunter(EvtxGlob=TargetGlob,
            ChannelRegex='^(Security|System)$',
            IdRegex='^(1102|104)',
            IocRegex='clear|cleared',
            DateAfter=DateAfter,
            DateBefore=DateBefore,
            VSSAnalysisAge=VSSAnalysisAge)

```
