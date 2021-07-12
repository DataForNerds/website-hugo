---
title: "Microsoft PowerShell"
date: 2021-07-08T16:28:20-04:00
draft: false
---

The data from DataForNerds can be brought into PowerShell as a Custom Object using the `Invoke-RestMethod` command and passing it the JSON URL as the `uri` parameter.  For example:

```powershell
$d4n = Invoke-RestMethod -Uri "https://raw.datafornerds.io/ms/mswin/releases.json"
```

The resulting object typically have two properties:

Property|Purpose
-|-
DataForNerds|Metadata containing at least the information about the last time the content was updated (LastUpdatedUTC property) and where we got the information from (SourceList property).
Data|The actual data you're looking for.

To view the data in PowerShell, output the data property. For example:

```powershell
$d4n = Invoke-RestMethod -Uri "https://raw.datafornerds.io/ms/mswin/releases.json"
$d4n.Data | Format-Table -AutoSize
```

You can use the Data property like any other array of objects in PowerShell.  It can be viewed, sorted, queried, exported, etc.
