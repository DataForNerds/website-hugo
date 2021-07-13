---
title: "Microsoft Locale IDs"
date: 2021-07-08T16:28:20-04:00
draft: false
---

Microsoft Locale IDs (used by a number of applications) are in JSON format at this address: [https://raw.datafornerds.io/ms/msother/mslocales.json](https://raw.datafornerds.io/ms/msother/mslocales.json). The source of this information is [this site](https://docs.microsoft.com/en-us/openspecs/office_standards/ms-oe376/6c085406-a698-4e12-9d4d-c3b0ee3dbc4a). The data is validated hourly.

## Sample Data
```json
{
	"DataForNerds": {
		"LastUpdatedUTC": "2021-07-13T15:37:31.0389417Z",
		"SourceList": ["https://docs.microsoft.com/en-us/openspecs/office_standards/ms-oe376/6c085406-a698-4e12-9d4d-c3b0ee3dbc4a"]
	},
	"Data": [{
		"LangCode": 1025,
		"LangName": "Arabic - Saudi Arabia",
		"LangTag": "ar-SA"
	}, {
		"LangCode": 1026,
		"LangName": "Bulgarian",
		"LangTag": "bg-BG"
	}, {
		"LangCode": 1027,
		"LangName": "Catalan",
		"LangTag": "ca-ES"
	}, {
		"LangCode": 1033,
		"LangName": "English - United States",
		"LangTag": "en-US"
	}, {
		"LangCode": 1034,
		"LangName": "Spanish - Spain (Traditional Sort)",
		"LangTag": "es-ES"
	}, {
		"LangCode": 58378,
		"LangName": "Spanish - Latin America",
		"LangTag": "es-419"
	}, {
		"LangCode": 58380,
		"LangName": "French - North Africa",
		"LangTag": "fr-015"
	}]
}
```

## Sample Usage in PowerShell

```powershell
$d4nData = Invoke-WebRequest "https://raw.datafornerds.io/ms/msother/mslocales.json" | Select -ExpandProperty Content | ConvertFrom-Json

Write-Host "The following locales include English in the name"

$d4nData.Data | Where-Object { $_.LangName -like "*English*" } | Format-Table -AutoSize
```