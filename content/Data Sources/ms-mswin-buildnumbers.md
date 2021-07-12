---
title: "Microsoft Windows Builds"
date: 2021-07-08T16:28:20-04:00
draft: false
---

Windows Builds are available in JSON format at this address: [https://raw.datafornerds.io/ms/mswin/buildnumbers.json](https://raw.datafornerds.io/ms/mswin/buildnumbers.json). The source of this information is [this site](https://docs.microsoft.com/en-us/windows/release-health/release-information).  The data is validated hourly.


## Sample Data
```json
{
	"DataForNerds": {
		"LastUpdatedUTC": "\/Date(1625758980460)\/",
		"SourceList": [
			"https://docs.microsoft.com/en-us/windows/release-health/release-information",
			"https://winreleaseinfoprod.blob.core.windows.net/winreleaseinfoprod/en-US.html"
		]
	},
	"Data": [{
		"Win10Version": "10.0.10240.16683",
		"Version": "10240.16683",
		"ReleaseDate": "2016-02-09",
		"Article": "KB3135174",
		"Comment": ""
	}, {
		"Win10Version": "10.0.19042.1055",
		"Version": "19042.1055",
		"ReleaseDate": "2021-06-11",
		"Article": "KB5004476",
		"Comment": "Out-of-band"
	}, {
		"Win10Version": "10.0.19043.1055",
		"Version": "19043.1055",
		"ReleaseDate": "2021-06-11",
		"Article": "KB5004476",
		"Comment": "Out-of-band"
	}, {
		"Win10Version": "10.0.17763.2028",
		"Version": "17763.2028",
		"ReleaseDate": "2021-06-15",
		"Article": "KB5003703",
		"Comment": "Preview"
	}, {
		"Win10Version": "10.0.10240.16769",
		"Version": "10240.16769",
		"ReleaseDate": "2016-04-12",
		"Article": "KB3147461",
		"Comment": ""
	}]
}
```

## Sample Usage in PowerShell

```powershell
$d4n = Invoke-RestMethod -Uri "https://raw.datafornerds.io/ms/mswin/buildnumbers.json"

$props = Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion'
$osVer = ([string]$props.CurrentMajorVersionNumber + '.' + [string]$props.CurrentMinorVersionNumber + '.' + [string]$props.CurrentBuildNumber + '.' + [string]$props.UBR)

$myBuild = $d4n.data | Where-Object { $_.Win10Version -eq $osVer }

Write-Host "You are running $osVer with Update $($myBuild.Article)"
Write-Host "Your patch level was released by Microsoft on $($myBuild.ReleaseDate)"

$patchDiff = New-TimeSpan -Start (Get-Date $myBuild.ReleaseDate) -End (Get-Date)

If($patchDiff.TotalDays -ge 30) {
    Write-Host "It might be time to look for an updated patch!" -ForegroundColor Red
} else {
    Write-Host "You're patch is recent enough." -ForegroundColor Green
}
```