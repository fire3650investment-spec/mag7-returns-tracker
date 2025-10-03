# Identified Follow-up Tasks

## Spelling / Wording Fix
* **Issue:** The CSV export headers label the ticker column as `股票代碼`, while the on-screen table and the rest of the interface use `股票代號`. This inconsistent wording stems from a typo in `index.html` (and the mirrored `mag7` file) at lines 189-193, and should be corrected to `股票代號` for consistency.

## Functional Bug Fix
* **Issue:** The chart data builder at lines 204-208 of `index.html` (and `mag7`) only filters out rows with `monthlyReturn === 'N/A'`, but it still calls `parseFloat` on `ytdReturn`. When `ytdReturn` is `'N/A'` (for example, after a failed fetch) `parseFloat('N/A')` becomes `NaN`, which produces invalid values in Recharts and prevents the chart from rendering correctly. The logic should filter out or coerce non-numeric YTD values before plotting.

## Documentation Update
* **Issue:** `README.md` currently contains only the project title and lacks the usage instructions that appear in the UI (API key requirement, data source explanation, etc.). The documentation should be expanded to describe how to obtain a Financial Modeling Prep API key and how to run the tracker so that the code and documentation stay aligned.

## Testing Improvement
* **Issue:** There are no automated tests covering the date helpers (`formatDate`, `getPreviousMonthEnd`, `getYearStart`) or the CSV export formatting logic in `index.html`. Adding a small Jest test suite (or similar) would prevent regressions in these calculations, especially around edge cases like January (previous year rollover) and leap years.
