---
title: MacOS.System.Wifi
hidden: true
tags: [Client Artifact]
---

This artifact looks for all Wifi networks to which a host has joined.  This can be useful in determining where a machine has been, or if a user has joined an illegitimate or unauthorized wireless network.


```yaml
name: MacOS.System.Wifi
description: |
   This artifact looks for all Wifi networks to which a host has joined.  This can be useful in determining where a machine has been, or if a user has joined an illegitimate or unauthorized wireless network.

type: CLIENT

author: Wes Lambert - @therealwlambert

parameters:
  - name: WifiGlob
    default: /Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist

precondition:
      SELECT OS From info() where OS = 'darwin'

sources:
  - query: |
      LET WifiPlist = SELECT OSPath from glob(globs=WifiGlob)
      LET KnownNetworks = SELECT get(member="KnownNetworks") as KN from plist(file=WifiPlist.OSPath)
      LET EachNetwork = SELECT * from foreach(
         row=KnownNetworks,
         query={
            SELECT _key AS Network, _value AS Value
            FROM items(item=KN)
         })
      SELECT Network,
             Value.SSIDString AS SSID,
             Value.SecurityType AS SecurityType,
             Value.HiddenNetwork AS HiddenNetwork,
             Value.PersonalHotspot AS PersonalHotspot,
             Value.AddedAt AS AddedAt,
             Value.LastAutoJoinAt AS LastAutoJoinAt,
             Value.LastManualJoinAt AS LastManualJoinAt,
             Value AS _Data
      FROM EachNetwork

```
