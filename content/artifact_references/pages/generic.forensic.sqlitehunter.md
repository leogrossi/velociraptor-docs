---
title: Generic.Forensic.SQLiteHunter
hidden: true
tags: [Client Artifact]
---

Hunt for SQLite files.

SQLite has become the de-facto standard for storing application data,
in many types of applications:

- Web Browsers
- Operating Systems
- Various applications, such as iMessage, TCC etc

This artifact can hunt for these artifacts in a mostly automated way.
More info at https://github.com/Velocidex/SQLiteHunter


```yaml

name: Generic.Forensic.SQLiteHunter
description: |
    Hunt for SQLite files.
    
    SQLite has become the de-facto standard for storing application data,
    in many types of applications:
    
    - Web Browsers
    - Operating Systems
    - Various applications, such as iMessage, TCC etc
    
    This artifact can hunt for these artifacts in a mostly automated way.
    More info at https://github.com/Velocidex/SQLiteHunter
    
    

column_types:
- name: Image
  type: preview_upload

export: |
  LET SPEC <= "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"
  LET Specs <= parse_json(data=gunzip(string=base64decode(string=SPEC)))
  LET CheckHeader(OSPath) = read_file(filename=OSPath, length=12) = "SQLite forma"
  LET Bool(Value) = if(condition=Value, then="Yes", else="No")

  -- In fast mode we check the filename, then the header then run the sqlite precondition
  LET matchFilename(SourceName, OSPath) = OSPath =~ get(item=Specs.sources, field=SourceName).filename
    AND CheckHeader(OSPath=OSPath)
    AND Identify(SourceName= SourceName, OSPath= OSPath)
    AND log(message=format(format="%v matched by filename %v",
            args=[OSPath, get(item=Specs.sources, field=SourceName).filename]))

  -- If the user wanted to also upload the file, do so now
  LET MaybeUpload(OSPath) = if(condition=AlsoUpload, then=upload(file=OSPath)) OR TRUE

  LET Identify(SourceName, OSPath) = SELECT if(
    condition=CheckHeader(OSPath=OSPath),
    then={
      SELECT *
      FROM sqlite(file=OSPath, query=get(item=Specs.sources, field=SourceName).id_query)
    }) AS Hits
  FROM scope()
  WHERE if(condition=Hits[0].Check = get(item=Specs.sources, field=SourceName).id_value,
    then= log(message="%v was identified as %v",
            args=[OSPath, get(item=Specs.sources, field=SourceName).Name]),
    else=log(message="%v was not identified as %v (got %v, wanted %v)",
             args=[OSPath, get(item=Specs.sources, field=SourceName).Name, str(str=Hits),
                   get(item=Specs.sources, field=SourceName).id_value]) AND FALSE)

  LET ApplyFile(SourceName) = SELECT * FROM foreach(row={
     SELECT OSPath FROM AllFiles
     WHERE if(condition=MatchFilename,  then=matchFilename(SourceName=SourceName, OSPath=OSPath),
      else=Identify(SourceName= SourceName, OSPath= OSPath))

  }, query={
     SELECT *, OSPath FROM sqlite(
        file=OSPath, query=get(item=Specs.sources, field=SourceName).SQL)
  })

  -- Filter for matching files without sqlite checks.
  LET FilterFile(SourceName) =
     SELECT OSPath FROM AllFiles
     WHERE if(condition=MatchFilename,
              then=OSPath =~ get(item=Specs.sources, field=SourceName).filename)

  -- Build a regex for all enabled categories.
  LET all_categories = SELECT _value FROM foreach(row=["All","MacOS","Chrome","Browser","Firefox","Windows"]) WHERE get(field=_value)
  LET category_regex <= join(sep="|", array=all_categories._value)
  LET AllGlobs <= filter(list=Specs.globs, condition="x=> x.tags =~ category_regex")
  LET _ <= log(message="Globs for category %v is %v", args=[category_regex, CustomGlob || AllGlobs.glob])
  LET AllFiles <= SELECT OSPath FROM glob(globs=CustomGlob || AllGlobs.glob)
    WHERE NOT IsDir AND MaybeUpload(OSPath=OSPath)

parameters:
- name: MatchFilename
  description: |
    If set we use the filename to detect the type of sqlite file.
    When unset we use heristics (slower)
  type: bool
  default: Y

- name: CustomGlob
  description: Specify this glob to select other files


- name: All
  description: Select targets with category All
  type: bool
  default: Y


- name: MacOS
  description: Select targets with category MacOS
  type: bool
  default: N


- name: Chrome
  description: Select targets with category Chrome
  type: bool
  default: N


- name: Browser
  description: Select targets with category Browser
  type: bool
  default: N


- name: Firefox
  description: Select targets with category Firefox
  type: bool
  default: N


- name: Windows
  description: Select targets with category Windows
  type: bool
  default: N


- name: SQLITE_ALWAYS_MAKE_TEMPFILE
  type: bool
  default: Y

- name: AlsoUpload
  description: If specified we also upload the identified file.
  type: bool

sources:
- name: AllFiles
  query: |
    SELECT * FROM AllFiles


- name: iMessage_Profiles
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="iMessage_Profiles")
    SELECT timestamp(epoch=date / 1000000000 + 978307200) AS Timestamp, *
    FROM Rows
    


- name: Chromium Browser Autofill_Profiles
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Autofill_Profiles")
    SELECT GUID,
      timestamp(epoch= date_modified) AS DateModified,
      timestamp(epoch= use_date) AS UseDate,
      FirstName, MiddleName, LastName, EmailAddress,
      PhoneNumber, CompanyName, StreetAddress,
      City, State, ZipCode, UseCount, OSPath
    FROM Rows
    


- name: Chromium Browser Autofill_Masked Credit Cards
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Autofill_Masked Credit Cards")
    SELECT * FROM Rows


- name: Chromium Browser Bookmarks
  query: |
    LET Rows = SELECT * FROM FilterFile(SourceName="Chromium Browser Bookmarks")
    -- Recursive function to report the details of a folder
    LET ReportFolder(Data, BaseName) = SELECT * FROM chain(a={
      -- First row emit the data about the actual folder
      SELECT BaseName + " | " + Data.name AS Name,
             timestamp(winfiletime=int(int=Data.date_added) * 10) AS DateAdded,
             timestamp(winfiletime=int(int=Data.date_last_used) * 10) AS DateLastUsed,
             Data.type AS Type,
             Data.url || ""  AS URL
      FROM scope()
    },
    b={
       -- If this folder has children recurse into it
       SELECT * FROM foreach(row={
          SELECT _value FROM items(item=Data.children)
       },  query={
          SELECT * FROM ReportFolder(Data=_value, BaseName=BaseName + " | " + Data.name)
       })
    })
    
    LET MatchingFiles = SELECT OSPath, parse_json(data=read_file(filename=OSPath)) AS Data
    FROM Rows
    
    SELECT * FROM foreach(row=MatchingFiles, query={
      SELECT * FROM chain(
      a={
        SELECT OSPath, *, "bookmark_bar" AS Type
        FROM ReportFolder(Data=Data.roots.bookmark_bar, BaseName="")
      },
      b={
        SELECT OSPath, *, "other" AS Type
        FROM ReportFolder(Data=Data.roots.other, BaseName="")
      },
      c={
        SELECT OSPath, *, "synced" AS Type
        FROM ReportFolder(Data=Data.roots.synced, BaseName="")
      })
    })
    


- name: Chromium Browser_Cookies
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser_Cookies")
    SELECT timestamp(winfiletime=(creation_utc * 10) || 0) AS CreationUTC,
           timestamp(winfiletime=(expires_utc * 10) || 0) AS ExpiresUTC,
           timestamp(winfiletime=(last_access_utc * 10) || 0) AS LastAccessUTC,
           HostKey, Name, Path,
           Bool(Value=is_secure) AS IsSecure,
           Bool(Value=is_httponly) AS IsHttpOnly,
           Bool(Value=has_expires) AS HasExpiration,
           Bool(Value=is_persistent) AS IsPersistent,
           Priority, SourcePort, OSPath
    FROM Rows
    


- name: Chromium Browser Extensions
  query: |
    LET Rows = SELECT * FROM FilterFile(SourceName="Chromium Browser Extensions")
    -- Resolve the message string against the Locale dict
    LET ResolveName(Message, Locale) = get(item=Locale,
          field=lowcase(string=parse_string_with_regex(regex="^__MSG_(.+)__$", string=Message).g1),
          default=Message).message || Message
    
    -- Read the manifest files
    LET ManifestData = SELECT OSPath, parse_json(data=read_file(filename=OSPath)) AS Manifest
    FROM Rows
    
    -- Find the Locale file to help with.
    LET LocaleData = SELECT *, if(condition=Manifest.default_locale, else=dict(),
         then=parse_json(data=read_file(
            filename=OSPath.Dirname + "_locales" + Manifest.default_locale + "messages.json"))) AS Locale
    FROM ManifestData
    
    LET GetIcon(Manifest) = Manifest.icons.`128` || Manifest.icons.`64` || Manifest.icons.`32` || Manifest.icons.`16`
    
    SELECT OSPath, Manifest.author.email AS Email,
      ResolveName(Message = Manifest.name, Locale=Locale) AS name,
      ResolveName(Message = Manifest.description, Locale=Locale) AS description,
      Manifest.oauth2.scopes as Scopes,
      Manifest.permissions as Permissions,
      Manifest.key as Key, if(condition=GetIcon(Manifest=Manifest),
                then=upload(file=OSPath.Dirname + GetIcon(Manifest=Manifest))) AS Image,
      Manifest AS _Manifest
    FROM LocaleData
    


- name: Chromium Browser Favicons
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Favicons")
    SELECT ID, IconID,
      timestamp(winfiletime= (LastUpdated * 10) || 0) AS LastUpdated,
      PageURL, FaviconURL,
      upload(accessor="data",
         file=_image,
         name=format(format="Image%v.png", args=ID)) AS Image,
      OSPath as _OSPath
    FROM Rows
    


- name: Chromium Browser History_Visits
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser History_Visits")
    SELECT ID,
       timestamp(winfiletime=(visit_time * 10) || 0) AS VisitTime,
       timestamp(winfiletime=(last_visit_time * 10) || 0) AS LastVisitedTime,
       URLTitle, URL, VisitCount, TypedCount,
       if(condition=hidden =~ '1', then="Yes", else="No") AS Hidden,
       VisitID, FromVisitID,
       visit_duration / 1000000 AS VisitDurationInSeconds,
       OSPath
    FROM Rows
    


- name: Chromium Browser History_Downloads
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser History_Downloads")
    LET StateLookup <= dict(`0`='In Progress', `1`='Complete', `2`="Cancelled", `3`="Interrupted", `4`="Interrupted")
    LET DangerType <= dict(`0`='Not Dangerous', `1`="Dangerous", `2`='Dangerous URL', `3`='Dangerous Content',
        `4`='Content May Be Malicious', `5`='Uncommon Content', `6`='Dangerous But User Validated',
        `7`='Dangerous Host', `8`='Potentially Unwanted', `9`='Whitelisted by Policy')
    LET InterruptReason <= dict(`0`= 'No Interrupt', `1`= 'File Error', `2`='Access Denied', `3`='Disk Full',
      `5`='Path Too Long',`6`='File Too Large', `7`='Virus', `10`='Temporary Problem', `11`='Blocked',
      `12`='Security Check Failed', `13`='Resume Error', `20`='Network Error', `21`='Operation Timed Out',
      `22`='Connection Lost', `23`='Server Down', `30`='Server Error', `31`='Range Request Error',
      `32`='Server Precondition Error', `33`='Unable to get file', `34`='Server Unauthorized',
      `35`='Server Certificate Problem', `36`='Server Access Forbidden', `37`='Server Unreachable',
      `38`='Content Length Mismatch', `39`='Cross Origin Redirect', `40`='Cancelled', `41`='Browser Shutdown',
      `50`='Browser Crashed')
    
    SELECT ID, GUID, CurrentPath, TargetPath, OriginalMIMEType, ReceivedBytes, TotalBytes,
      timestamp(winfiletime=(start_time * 10) || 0) AS StartTime,
      timestamp(winfiletime=(end_time * 10) || 0) AS EndTime,
      timestamp(winfiletime=(opened * 10) || 0) AS Opened,
      timestamp(winfiletime=(last_access_time * 10) || 0) AS LastAccessTime,
      timestamp(epoch=last_modified) AS LastModified,
      get(item=StateLookup, field=str(str=state), default="Unknown") AS State,
      get(item=DangerType, field=str(str=danger_type), default="Unknown") AS DangerType,
      get(item=InterruptReason, field=str(str=interrupt_reason), default="Unknown") AS InterruptReason,
      ReferrerURL, SiteURL, TabURL, TabReferrerURL, DownloadURL, OSPath
    FROM Rows
    


- name: Chromium Browser History_Keywords
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser History_Keywords")
    SELECT KeywordID, URLID,
       timestamp(winfiletime=(last_visit_time * 10) || 0) AS LastVisitedTime,
       KeywordSearchTerm, Title, URL, OSPath
    FROM Rows
    


- name: Chromium Browser Media_History
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Media_History")
    SELECT ID, URL, WatchTimeSeconds,
       Bool(Value=has_video) AS HasVideo,
       Bool(Value=has_audio) AS HasAudio,
       timestamp(winfiletime=last_updated_time_s || 0) AS LastUpdated,
       OriginID, OSPath
    FROM Rows
    


- name: Chromium Browser Media_Playback Session
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Media_Playback Session")
    SELECT ID,
      timestamp(winfiletime=last_updated_time_s || 0) AS LastUpdated, URL,
      duration_ms / 1000 AS DurationInSeconds,
      position_ms / 1000 AS PositionInSeconds,
      Title, Artist, Album, SourceTitle, OriginID, OSPath
    FROM Rows
    


- name: Chromium Browser Network_Predictor
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Network_Predictor")
    SELECT * FROM Rows
    


- name: Chromium Browser Shortcuts
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Shortcuts")
    SELECT ID,
      timestamp(winfiletime= (last_access_time * 10) || 0) AS LastAccessTime,
      TextTyped, FillIntoEdit, URL, Contents,
      Description, Type, Keyword, TimesSelectedByUser, OSPath
    FROM Rows
    


- name: Chromium Sessions_Sessions
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Sessions_Sessions")
    SELECT * FROM info()
    


- name: Chromium Browser Top Sites
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Chromium Browser Top Sites")
    SELECT * FROM Rows
    


- name: Firefox Places
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Places")
    LET BookmarkTypes <= dict(`1`="URL", `2`="Folder", `3`="Separator")
    SELECT ID, ParentID,
       get(item= BookmarkTypes, field=str(str=type), default="Unknown") AS Type,
       timestamp(epoch=dateAdded) AS DateAdded,
       timestamp(epoch=lastModified) AS LastModified,
       Position, Title, URL, ForeignKey, OSPath
    FROM Rows
    


- name: Firefox Places_Downloads
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Places_Downloads")
    SELECT PlaceID, Content,
       timestamp(epoch=dateAdded) AS DateAdded,
       timestamp(epoch=lastModified) AS LastModified,
       OSPath
    FROM Rows
    


- name: Firefox Places_History
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Places_History")
    LET VisitType <= dict(`1`='TRANSITION_LINK', `2`='TRANSITION_TYPED', `3`='TRANSITION_BOOKMARK',
      `4`='TRANSITION_EMBED', `5`= 'TRANSITION_REDIRECT_PERMANENT', `6`='TRANSITION_REDIRECT_TEMPORARY',
      `7`='TRANSITION_DOWNLOAD', `8`='TRANSITION_FRAMED_LINK', `9`='TRANSITION_RELOAD')
    
    SELECT VisitID, FromVisitID,
       timestamp(epoch= last_visit_date) AS LastVisitDate,
       VisitCount, URL, Title, Description,
       get(item= VisitType, field=str(str=visit_type), default="Unknown") AS VisitType,
       Bool(Value=hidden) AS Hidden,
       Bool(Value=types) AS Typed,
       Frecency, PreviewImageURL, OSPath
    FROM Rows
    


- name: Firefox Cookies
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Cookies")
    SELECT ID, Host, Name, Value,
       timestamp(epoch= creationTime) AS CreationTime,
       timestamp(epoch= lastAccessed) AS LastAccessedTime,
       timestamp(epoch= expiry) AS Expiration,
       Bool(Value= isSecure) AS IsSecure,
       Bool(Value= isHttpOnly) AS IsHTTPOnly, OSPath
    FROM Rows
    


- name: Firefox Downloads
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Downloads")
    SELECT ID, Name, MIMEType, Source, Target,
       timestamp(epoch= startTime) AS StartTime,
       timestamp(epoch= endTime) AS EndTime,
       timestamp(epoch= expiry) AS Expiration,
       CurrentBytes, MaxBytes, OSPath
    FROM Rows
    


- name: Firefox Favicons
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Favicons")
    SELECT ID, PageURL, FaviconURL,
       timestamp(epoch= expire_ms) AS Expiration,
       OSPath
    FROM Rows
    


- name: Firefox Form History
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Firefox Form History")
    SELECT ID, FieldName, Value, TimesUsed,
       timestamp(epoch= firstUsed) AS FirstUsed,
       timestamp(epoch= lastUsed) AS LastUsed,
       GUID, OSPath
    FROM Rows
    


- name: MacOS Applications Cache
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="MacOS Applications Cache")
    SELECT
       time_stamp AS Timestamp,
       OSPath.Base AS Application,
       entry_ID AS EntryID,
       version AS Version,
       hash_value AS Hash,
       storage_policy AS StoragePolicy,
       request_key AS URL,
       plist(file=request_object, accessor="data") AS Request,
       plist(file=response_object, accessor="data") AS Response,
       partition AS Partition,
       OSPath
    FROM Rows
    


- name: MacOS NetworkUsage
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="MacOS NetworkUsage")
    SELECT timestamp(epoch= ZTIMESTAMP + 978307200) AS Timestamp,
      timestamp(epoch= ZFIRSTTIMESTAMP + 978307200) AS FirstTimestamp,
      timestamp(epoch= LIVE_USAGE_TIMESTAMP + 978307200) AS LiveUsageTimestamp,
      ZBUNDLENAME AS BundleID,
      ZPROCNAME AS ProcessName,
      ZWIFIIN AS WifiIn,
      ZWIFIOUT AS WifiOut,
      ZWWANIN AS WanIn,
      ZWWANOUT AS WandOut,
      ZWIREDIN AS WiredIn,
      ZWIREDOUT AS WiredOut,
      ZXIN AS _XIn,
      ZXOUT AS _XOut,
      Z_PK AS LiveUsageTableID
    FROM Rows
    


- name: MacOS Notes
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="MacOS Notes")
    SELECT Key AS _Key,
     OSPath[1] AS User,
     Note,
     Title,
     Snippet,
     NoteID AS _NoteID,
     timestamp(cocoatime=CreatedTS) AS CreatedTime,
     timestamp(cocoatime=LastOpenedDate) AS LastOpenedTime,
     timestamp(cocoatime=DirModificationDate) AS LastDirModifcation,
     Account AS _Account,
     Directory,
     DirectoryID,
     AttachmentName,
     AttachmentSize,
     AttachmentUUID,
     if(condition=AttachmentUUID,
        then=OSPath[:2] + '/Library/Group Containers/group.com.apple.notes/Accounts/LocalAccount/Media/' + AttachmentUUID + '/' + AttachmentName) AS AttachmentLocation,
     AccountName AS _AccountName,
     AccountID AS _AccountID,
     AccountType AS _AccountType,
     gunzip(string=Data) AS Data,
     OSPath
    FROM Rows
    


- name: Windows Activities Cache_ActivityPackageId
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Windows Activities Cache_ActivityPackageId")
    SELECT format(format="%0X-%0X-%0X-%0X-%0X", args=[
      ActivityId[0:4], ActivityId[4:6], ActivityId[6:8],
      ActivityId[8:10], ActivityId[10:] ]) AS ActivityId,
      Platform, PackageName, ExpirationTime, OSPath
    FROM Rows
    


- name: Windows Activities Cache_Clipboard
  query: |
    LET Rows = SELECT * FROM ApplyFile(SourceName="Windows Activities Cache_Clipboard")
    SELECT
      CreatedTime,
      LastModifiedTime,
      LastModifiedOnClient,
      StartTime,
      EndTime,
      Payload,
      OSPath[1] AS User,
      base64decode(string=parse_json_array(data=ClipboardPayload)[0].content) AS ClipboardPayload,
      OSPath AS Path,
      Mtime
    FROM Rows
    




```
