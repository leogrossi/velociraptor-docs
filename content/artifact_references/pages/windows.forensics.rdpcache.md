---
title: Windows.Forensics.RDPCache
hidden: true
tags: [Client Artifact]
---

This artifact views and enables simplified upload of RDP 
cache files. 

Filters include User regex to target a user and Accessor to target
vss via ntfs_vss.

Best combined with:

- Windows.EventLogs.RDPAuth to collect RDP focused event logs.
- Windows.Registry.RDP to collect user RDP mru and server info


```yaml
name: Windows.Forensics.RDPCache
author: Matt Green - @mgreen27
description: |
   This artifact views and enables simplified upload of RDP 
   cache files. 
   
   Filters include User regex to target a user and Accessor to target
   vss via ntfs_vss.

   Best combined with:

   - Windows.EventLogs.RDPAuth to collect RDP focused event logs.
   - Windows.Registry.RDP to collect user RDP mru and server info

reference:
   - https://github.com/ANSSI-FR/bmc-tools
   - https://github.com/BSI-Bund/RdpCacheStitcher

parameters:
   - name: RDPCacheGlob
     default: C:\{{Users,Windows.old\Users}\*\AppData\Local,Documents and Settings\*\Local Settings\Application Data}\Microsoft\Terminal Server Client\Cache\*
   - name: Accessor
     description: Set accessor to use. blank is default, file for api, ntfs for raw, ntfs_vss for vss
   - name: UserRegex
     default: .
     description: Regex filter of user to target. StartOf(^) and EndOf($)) regex may behave unexpectanly.
     type: regex
   - name: UploadRDPCache
     type: bool

sources:
  - query: |
      LET results = SELECT OSPath, Size, Mtime, Atime, Ctime, Btime
        FROM glob(globs=RDPCacheGlob,accessor=Accessor)
        WHERE OSPath =~ UserRegex
      
      LET upload_results = SELECT *, upload(file=OSPath) as CacheUpload
        FROM results
      
      SELECT * FROM if(condition= UploadRDPCache,
        then= upload_results,
        else= results )
```
