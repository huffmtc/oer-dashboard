# Open Education Data Dashboard

Public-facing Open Education impact dashboard for Midlands Technical College. The dashboard is designed for embedding in a LibGuide and hosting through GitHub Pages.

## What this dashboard shows

The dashboard separates **verified OER impact** from the broader **OER implementation pipeline**.

Verified impact includes:

* fully deployed OER courses only
* only the terms beginning with each course’s deployment term
* estimated student savings
* enrollments impacted
* OER sections

Pipeline/status information includes:

* total OER pipeline courses
* fully deployed courses
* courses in development
* courses in pilot

Pilot and development courses are shown as implementation status, but they are **not included** in verified savings, enrollment, or section totals.

## Public files to upload to GitHub

Upload or replace these files in the public GitHub repository:

```text
oer-dashboard/
├── index.html
└── data/
    └── dashboard-data.json
```

These are the only files required for the public dashboard.

## Private files to keep off GitHub

Do **not** upload these files to the public repository:

```text
Master Data for Dashboard.xlsx
OER Data for Dashboard.xlsx
update_dashboard_data.py
```

`Master Data for Dashboard.xlsx` is the main working file where the source data is updated and maintained.

`OER Data for Dashboard.xlsx` is updated through Power Query and serves as the structured workbook used to generate the public JSON file.

`update_dashboard_data.py` is the local Python script used to generate `dashboard-data.json`.

## Data workflow

The dashboard data begins in:

```text
Master Data for Dashboard.xlsx
```

That workbook is the main private source file.

Power Query then updates:

```text
OER Data for Dashboard.xlsx
```

The Python updater reads the updated dashboard workbook and generates:

```text
data/dashboard-data.json
```

The public dashboard reads from that JSON file.

## Routine update workflow

Use this process when refreshing dashboard data:

1. Open `Master Data for Dashboard.xlsx`.

2. Update the source data as needed.

3. Refresh the Power Query connections so `OER Data for Dashboard.xlsx` updates.

4. Save `OER Data for Dashboard.xlsx`.

5. Run the Python updater locally:

   ```bash
   python update_dashboard_data.py "OER Data for Dashboard.xlsx"
   ```

6. Confirm that a new file was created or updated at:

   ```text
   data/dashboard-data.json
   ```

7. Upload or commit only this file to GitHub:

   ```text
   data/dashboard-data.json
   ```

8. Refresh the GitHub Pages dashboard and LibGuide embed to confirm the numbers updated.

## When to upload `index.html`

Only upload or replace `index.html` when the dashboard design, wording, layout, filters, or JavaScript behavior changes.

For ordinary data updates, only `data/dashboard-data.json` needs to change.

## Term-based data logic

The dashboard is designed around terms instead of hard-coded Fall/Spring fields.

Supported term pattern examples:

```text
FA25
SP26
SU26
FA26
SP27
```

The core impact rule is:

```text
For each course, count only terms where the course is fully deployed by that term.
```

This allows Summer 2026 and future terms to be added without redesigning the dashboard. New term data should be added to the workbook, Power Query should refresh `OER Data for Dashboard.xlsx`, and the updater should regenerate `dashboard-data.json`.

## Impact-period filter

The dashboard’s impact-period filter should represent a reporting period such as:

```text
AY 2025-2026 impact to date
Fall 2025
Spring 2026
Summer 2026
```

At MTC, the academic year includes:

```text
Fall
Spring
Summer
```

For example:

```text
AY 2025-2026 = Fall 2025 + Spring 2026 + Summer 2026
```

The combined academic-year view sums only eligible term-level impact for each course. A course deployed in Spring 2026, for example, is not counted for Fall 2025 impact.

## Course-Level Impact page

The Course-Level Impact page shows verified OER impact only. It should not include pilot or in-development courses as savings impact.

The course table uses **Verified term(s)** to show the term or terms where a course is actually counted in the selected impact period.

## OER Student Perceptions page

The Student Perceptions page is survey-based and separate from the verified savings/enrollment calculations.

Important display rules:

* Use plain-language labels where possible.
* Avoid raw score notation in key takeaways.
* Use percentage-based outcomes for public readability when the underlying data supports it.
* Response-rate filtering should not appear dynamic unless the JSON includes filtered response-rate denominators.

## Notes on interpretation

* **Estimated student savings** are based on enrollment and textbook cost assumptions.
* **Enrollments impacted** may include duplicated students across courses or terms.
* **OER sections** count sections associated with verified OER impact.
* **Fully deployed courses** are current implementation-status counts, while savings, enrollment, and section totals are term-aware.
* Pilot and in-development courses represent pipeline activity and are excluded from verified impact totals until full deployment can be confirmed.

## Current public-hosting model

The dashboard can be hosted on GitHub Pages and embedded in LibGuides with an iframe.

Typical public dashboard URL pattern:

```text
https://huffmtc.github.io/oer-dashboard/
```

Typical public JSON URL pattern:

```text
https://huffmtc.github.io/oer-dashboard/data/dashboard-data.json
```

## Troubleshooting

If the dashboard shows dashes or blank charts:

1. Confirm that `data/dashboard-data.json` exists in the GitHub repository.

2. Confirm the file path is exactly:

   ```text
   data/dashboard-data.json
   ```

3. Open the public JSON URL directly in a browser to confirm it loads.

4. Hard-refresh the dashboard page.

5. Check that `index.html` and `dashboard-data.json` were both uploaded to the correct repository and branch.

If the dashboard numbers do not match the Excel workbook:

* Confirm that `Master Data for Dashboard.xlsx` was updated.
* Confirm that Power Query refreshed `OER Data for Dashboard.xlsx`.
* Confirm that the Python updater was run against the updated `OER Data for Dashboard.xlsx`.
* Check whether Excel totals include pilot or development courses.
* Check whether Excel totals include pre-deployment terms.
* The public dashboard should use verified, term-aware impact totals unless intentionally changed.

## What to upload after changes

### Data-only update

Upload:

```text
data/dashboard-data.json
```

### Design or wording update

Upload:

```text
index.html
```

### Full public dashboard update

Upload:

```text
index.html
data/dashboard-data.json
```

Do not upload:

```text
Master Data for Dashboard.xlsx
OER Data for Dashboard.xlsx
update_dashboard_data.py
```
