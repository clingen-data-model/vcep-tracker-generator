# Variant Tracker Report Maintenance
## All of the Variant Tracker Reports are housed  here: [Google Folder Containing Existing Reports](https://drive.google.com/drive/folders/10vEGdTMJ5IxajPVwMV2jfRMFJadlXLM4)
These reports all run on a set of functions contained in the “VariationTrackerProject” library, contained here: [Variation Tracker Project Google Apps Script](https://script.google.com/home/projects/1bIhg7fWREGLvxvuhn_oNXexZnd6vRRkuzA7TgL--67JS0QW5rP6WKwr9/edit). Within each individual report, selecting "Extensions" followed by "Apps Script" will open a new window with the local functions running the operations of the individual Variant Tracker Report. The parent functions in the "VariantTrackerProject" library are called using wrapper functions, executing the master functions locally for each individual Variant Tracker Report.

* When updating any individual Variant Tracker Report, various sheets may have to be manipulated to create the desired change(s). When modifications are complete, all sheets should be hidden except for "home", "alerts", "priorities", and "tracking".

## General Sheets Infrastructure
* The "alerts by release" and "priorities by release" hidden sheets are data connectors that link to the available ClinVar data in BigQuery. They pull variants in ClinVar with out-of-date/discrepant classifications with another submitter or ClinVar variant records within genes in the VCEP’s scope of work that could be prioritized for curation or used in a variant curation pilot, respectively.
* The "alert extract" and "priority extract" hidden sheets sort the data from "alerts by release" and "priorities by release". "Alert extract" is sorted by gene symbol, name of the variant, and alert type in ascending order. "Priority extract" is sorted by the pathogenicity conflict type, gene symbol, and name of the variant in ascending order and also includes an extra column listing each variant's ClinVar link.
* The "alerts" and "priorities" sheets, which remain visible, are the cleaned and sorted versions of the "alert extract" and "priority extract" sheets. Repeated values for the same variants are removed so that only the alert types and current classifications corresponding to each variant are indicated, respectively.

# Functionality of the VariationTrackerProject Library

## createVarTrackerMenu()
### Description
This function will create a custom menu called "🧬 Tracker" in the active spreadsheet. The custom menu will include two menu items:
1. "☁ Get Release!": When selected, this menu item will execute the getRelease() function. You can customize the getRelease() function to retrieve and display a selected release date or perform any other relevant actions.
2. "ℹ️ How to Use": When selected, this menu item will execute the showHowTo() function. This displays a pop-up of this document: [How To Use VCEP Variant Tracker Report](https://docs.google.com/document/d/1UMVFD1q55rkvNKoeG_Yb_oZBfW6J5UJ9KHW7o6P6IV4/edit).
3. "🔀 Track": When selected, this menu item will execute the appendToTracker() function. This will copy selected (checked) variant reports from the active sheet, either "alerts" or "priorities" to the "tracking" sheet.
Users can access the custom menu by navigating to the "🧬 Tracker" menu in the Google Sheets document. They can then select the desired menu item to perform the associated action. This provides a user-friendly interface for interacting with the tracker and accessing specific functionalities.
### Parameters
None
### Returns
None

## getReleaseDate()
### Description
This function adjusts the release date for all of the sheets in use.
### Parameters
selectedAsOfDate - The date selected by the user in the VCEP Tracker Report.
### Returns
The single release date result.

## refresh()
### Description
This function adjusts refresh/release dates for the spreadsheet, updating the "selectedAsOf", "Last Refresh As Of", "Last Refresh Release", and "Last Refresh Executed" variables as well.
### Parameters
None
### Returns
None

## refreshAll()
### Description
This function will first enable the execution of all data sources in the spreadsheet using SpreadsheetApp.enableAllDataSourcesExecution(). This ensures that the data sources can be refreshed. Then, it calls spreadsheet.refreshAllDataSources() to initiate the refresh process for all data sources in the spreadsheet. This action retrieves the latest data from the sources and updates the corresponding data in the spreadsheet. As a result, you can maintain accurate and up-to-date information in the Variant Tracker Reports.
### Parameters
None
### Returns
None


## resetStandardFilterViews()
### Description
This function will retrieve the filter views in the "alerts" and "priorities" sheet, update the filter ranges to include the latest data, and apply the changes to the filter views in the spreadsheet. This ensures that the filter views display the most up-to-date information as well as default ClinGen filters.
### Parameters
sheetName - Desired sheet to reset the standard filter views for.
### Returns
None


## getRelease()
### Description
This function calls refreshAll() to refresh all of the data in the spreadsheet, then updates the filter views in the spreadsheet by calling the updateFilterView() function. It then pulls data for the “selectedRelease” date and updates the “loadedRelease” to this value to make the Variant Tracker Report display data to reflect this date.
### Parameters
None
### Returns
None


## showHowTo()
### Description
This function will display a dialog box titled "How to use this report" in the active spreadsheet. The dialog box contains an embedded Google Document that provides detailed instructions and guidelines on how to navigate, interpret, and interact with the report. Users can refer to the instructions in the dialog box to better understand and utilize the features and functionality of the report.
### Parameters
None
### Returns
None

## formatDate(thisDate, inclTime)
### Description
Formats the given date into a string representation.
### Parameters
thisDate - The date to be formatted.
inclTime - Whether to include the time in the formatted string.
### Returns
fdate - The given date, formatted as a string.

# Deploying Changes to the Functions and Updating Existing Reports
Changes to these functions that are meant to be applied to all Variant Tracker Reports must be done in the master file, [Variation Tracker Project Google Apps Script](https://script.google.com/home/projects/1bIhg7fWREGLvxvuhn_oNXexZnd6vRRkuzA7TgL--67JS0QW5rP6WKwr9/edit).

1. Once all updates are complete, deploy the Google Script as a new version of the Variation Tracker Project Google Apps Script.
 * Select the blue “Deploy” button in the top right corner of the interface.
 * Select “New deployment” from the dropdown menu.
 * Select the deployment type as “Library” and add a description to the deployment that includes a version number to ensure the most up-to-date Google Script can be easily selected.
 * Select “Deploy” in the bottom right hand corner of the popup window you are working in.

2. Separately update each Variant Tracker Report.
 * Work through each report by selecting “Extensions” followed by “Apps Script” in each report’s Google Sheets toolbar. (This process is in the process of being automated).
 * The new window that opens will contain wrapper functions that locally execute the functions from the master file. 
 * On the left-hand sidebar, select the library titled, “VariationTrackerProject”.
 * In the popup window, select the most recent version (highest number) of the VariationTrackerProject library.
 * Select “Save”.

Once this step is completed for every variant tracker report, all of the sheets will be properly updated.
