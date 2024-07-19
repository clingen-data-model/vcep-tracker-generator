# vcep-tracker-generator
This repository contains projects for the auto-generation of VCEP Tracker reports.

This is intended for more efficient, less error-prone updates made to the VCEP Tracker reports as the quantity of VCEP Tracker reports grows. This project is new and still in the design phase of work.

## Generating New Reports
1. Update VCEP submitter info in the [ClinVar Report BQ Support Tables "Report Submitter List" sheet](https://docs.google.com/spreadsheets/d/1bADskBcobHTmmXungY09beWPDEa1nqM-PP__86yGVj0/edit?gid=2067576827#gid=2067576827), ensuring the "active report" column in the "Report Submitter List" is marked as "Yes".
2. Generate corresponding ClinVar-VCEP report tables within ClinVar by running procedures from the Big Query 00. Readme script, starting with proc 07. report variants to the end.
3. In the [ClinVar Report BQ Support Tables "Reports" sheet](https://docs.google.com/spreadsheets/d/1bADskBcobHTmmXungY09beWPDEa1nqM-PP__86yGVj0/edit?gid=1018498593#gid=1018498593), select "Build Report" from the dropdown menu in column "Google Spreadsheet ID" and click the "Generate Sheets" button within the header of the column.

## Updating Existing Reports
In progress.
