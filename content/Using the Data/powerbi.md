---
title: "Microsoft PowerBI"
date: 2021-07-08T16:28:20-04:00
draft: false
---

The data from DataForNerds can be brought into PowerBI using the Web data source type. The following steps outline the overall steps to gather the data.

1. Launch PowerBI Desktop. Create a new report or open an existing report.
2. From the `Home` ribbon, select `Get Data`.  Either select `Web` from the drop down (if available), or select `More` and then choose `Web` from the resulting dialog box.
3. Enter the URL to the JSON file (e.g. [https://raw.datafornerds.io/ms/mswin/releases.json](https://raw.datafornerds.io/ms/mswin/releases.json)) and click OK.
4. You may be prompted for authentication parameters (you can use anonymous authentication) or be prompted to apply your new changes to the report.

The data is now available as a source within your PowerBI report that can be linked to existing data and displayed.