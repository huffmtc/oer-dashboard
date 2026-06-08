GitHub Pages upload instructions

Upload these two files to the root of your oer-dashboard repository:

1. index.html
2. OER Data Dashboard.xlsx

The dashboard loads the Excel workbook directly from the same GitHub Pages folder. To update the dashboard later, replace the Excel file in GitHub with a new version using the exact same filename:

OER Data Dashboard.xlsx

Your published dashboard URL should stay:
https://huffmtc.github.io/oer-dashboard/

LibGuides iframe embed code:

<iframe
  src="https://huffmtc.github.io/oer-dashboard/"
  width="100%"
  height="1500"
  style="border:0;"
  loading="lazy"
  title="Open Education Data Dashboard">
</iframe>

Notes:
- GitHub Pages may take a minute or two to refresh after you replace files.
- If the dashboard shows a workbook-not-found message, confirm that the Excel filename matches exactly, including spaces and capitalization.
- Do not rename the Excel file unless you also update WORKBOOK_URL near the bottom of index.html.
