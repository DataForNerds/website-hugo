---
title: "Microsoft Windows Releases"
date: 2021-07-08T16:28:20-04:00
draft: false
---

Windows Release IDs are available in JSON format at this address: [https://raw.datafornerds.io/ms/mswin/buildnumbers.json](https://raw.datafornerds.io/ms/mswin/releases.json). The source of this information is [this site](https://docs.microsoft.com/en-us/windows/release-health/release-information) which contains a link to [this data](https://winreleaseinfoprod.blob.core.windows.net/winreleaseinfoprod/en-US.html).  The data is validated hourly.

## Sample Data
```json
{
	"DataForNerds": {
		"LastUpdatedUTC": "2021-07-08T15:56:35.0659636Z",
		"SourceList": [
			"https://docs.microsoft.com/en-us/windows/release-health/release-information", 
			"https://winreleaseinfoprod.blob.core.windows.net/winreleaseinfoprod/en-US.html"
		]
	},
	"Data": [{
		"Version": "10240",
		"FullVersion": "10.0.10240",
		"Build": "1507 (RTM)"
	}, {
		"Version": "10586",
		"FullVersion": "10.0.10586",
		"Build": "1511"
	}, {
		"Version": "19042",
		"FullVersion": "10.0.19042",
		"Build": "20H2"
	}, {
		"Version": "19043",
		"FullVersion": "10.0.19043",
		"Build": "21H1"
	}]
}
```

## Sample Usage in PowerShell

```powershell
$d4n = Invoke-RestMethod -Uri "https://raw.datafornerds.io/ms/mswin/releases.json"

$myW10Version = Get-CimInstance Win32_OperatingSystem | Select -ExpandProperty BuildNumber

$myBuild = $d4n.data | Where-Object { $_.Version -eq $myW10Version }

Write-Host "I am running Windows 10 Build Number $($myW10Version) which is $($myBuild.Build)."

```