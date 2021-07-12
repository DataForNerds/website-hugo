---
title: "Microsoft M365 Apps Builds"
date: 2021-07-08T16:28:20-04:00
draft: false
---

Microsoft M365 Apps for Business (formerly Office 365) build numbers are in JSON format at this address: [https://raw.datafornerds.io/ms/msapps/buildnumbers.json](https://raw.datafornerds.io/ms/msapps/buildnumbers.json). The source of this information is [this site](https://docs.microsoft.com/en-us/officeupdates/update-history-microsoft365-apps-by-date). The data is validated hourly.

## Known Issues
The following known issues are pending correction:
- [Some Office Versions have a space in the version number](https://github.com/DataForNerds/public/issues/10)
- [Office Builds Without Years are Defaulting to 2021](https://github.com/DataForNerds/public/issues/11)

## Sample Data
```json
{
	"DataForNerds": {
		"LastUpdatedUTC": "\/Date(1625771575455)\/",
		"SourceList": ["https://docs.microsoft.com/en-us/officeupdates/update-history-microsoft365-apps-by-date"]
	},
	"Data": [{
		"ReleaseDate": "2017-12-12",
		"Channel": "Semi-Annual Enterprise",
		"Build": "7766.2130",
		"Version": "1701",
		"FullBuild": "16.0.7766.2130"
	}, {
		"ReleaseDate": "2018-08-14",
		"Channel": "Semi-Annual Enterprise",
		"Build": " 8431.2299",
		"Version": "1708",
		"FullBuild": "16.0. 8431.2299"
	}, {
		"ReleaseDate": "2021-12-06",
		"Channel": "Current",
		"Build": "8730.2122",
		"Version": "1711",
		"FullBuild": "16.0.8730.2122"
	}]
}
```

## Sample Usage in PowerShell

```powershell
$d4n = Invoke-RestMethod -Uri "https://raw.datafornerds.io/ms/msapps/buildnumbers.json"

Write-Host "Builds Released in Past 7 days"
ForEach($build in $d4n.Data) {
    $diff = New-TimeSpan -Start (Get-Date $build.ReleaseDate) -End (Get-Date)
    If($diff.TotalDays -le 7) {
        Write-Host "Office 365 Version $($build.FullBuild) is $($build.Version) and was released $($build.ReleaseDate)"
    } else { <# Do Nothing #> }
}
```