# Google Data Analytics — Course 5, Module 1: Organize Data for More Effective Analysis

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 1 readings

> *(guide grows as more module 1 readings are added)*

## 🎯 What this module is about (one sentence)

Course 5 ("Analyze Data to Answer Questions") is where you finally *work* the data instead of
prepping it — and module 1 starts with the two moves every analysis begins with: **sorting**
(put rows in a meaningful order) and **filtering** (show only the rows that match), done both in
spreadsheets and in SQL on BigQuery, plus the .csv plumbing that gets data in and out of tools.

**Sue's note:** you have done this module every payday for 20 years. Sorting a payroll register by
department, filtering the GL export to one cost center, pulling "everyone with OT > 0 this
period" — that *is* sorting and filtering. The new part is the vocabulary and doing it in SQL
instead of Excel's Data tab. Course 5 overview says it plainly: you've climbed to higher ground;
now you get to look at the view.

## 🗺️ Where this course goes (from the Course 5 overview)

| Module | What you'll do | Payroll parallel |
|---|---|---|
| **1 — Organize data** | Sort & filter in spreadsheets and SQL; temporary tables | Sorting the register, filtering the GL export |
| **2 — Format & adjust data** | Convert/format data types; combine data with SQL; get feedback from colleagues | Fixing text-vs-number pay codes; merging HR and payroll files; peer review before month-end close |
| **3 — Aggregate data** | Combine cells in spreadsheets; JOIN multiple tables in SQL | Department totals; matching employee master to timecards |
| **4 — Perform calculations** | Formulas, functions, pivot tables, SQL calculations, temp tables | Every gross-to-net calc and every pivot you've ever built |

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Organize data** (phase 1 of analysis) | Arrange data so patterns and trends become obvious before you dig in | Before you review a payroll register you sort it into an order that makes exceptions jump out — same instinct. |
| **Table** | Rows and columns; the shape almost every dataset takes | A payroll register or GL detail export. One row = one observation (one check, one journal line). |
| **Sorting** | Arranging data in a meaningful order (ascending/descending) by a metric you choose — ranks it, groups similar things, gives immediate insight | Sort the register by gross pay descending to spot the outlier check; sort by department to review one group at a time. |
| **Filtering** | Showing only rows that meet a criterion while hiding the rest; remove the filter and the data returns to its original state | AutoFilter on the GL export: show only account 6100, only cost center 210, only employees with a 401(k) deduction. Nothing is deleted — you just clear the filter when you're done. |
| **Outlier** | A data point very different from similarly collected data; may not be reliable | The $48,000 "regular pay" line that turns out to be a fat-fingered hourly rate. Filtering is how you find it before it hits the bank file. |
| **Sort + filter together** | Filter to the relevant subset, *then* sort it — organizes only what matters | "Show me just the OT lines, sorted highest to lowest" — that's the whole overtime audit in one move. |
| **Sort sheet vs. sort range** (spreadsheets) | *Sort sheet* keeps every row intact; *sort range* on one column shuffles that column alone and **scrambles the rows** | Sorting only the Employee Name column and leaving Net Pay where it was = every check now belongs to the wrong person. You've seen someone do this. Never sort a single column of a register. |
| **Pivot table sort** | Pivot rows/columns sort ascending by default (custom lists first); setting descending creates a rule that persists as new data is added | Your department-total pivot: set it to descending once and it stays ranked correctly every pay period you refresh it. |
| **`WHERE` clause** (SQL filter) | `WHERE Genre = 'Comedy'` keeps only rows meeting the condition | `WHERE dept = 'Payroll'` or `WHERE ot_hours > 0` — the AutoFilter dropdown, written as a sentence. |
| **`ORDER BY`** (SQL sort) | Sorts the result set; `ORDER BY column DESC` for descending (covered in the sort videos alongside spreadsheet sorting) | "Sort by gross pay, largest first" — the same as clicking Z→A on the Gross column. |
| **BigQuery** | Google Cloud's data warehouse for querying/filtering large datasets, aggregating, and complex ops — used when data is too big for a spreadsheet | The GL when it's 5 million lines and Excel chokes. Same questions, bigger engine. |
| **BigQuery Studio panes** | **Navigation pane** (moves between GCP tools), **Explorer pane** (your projects, starred projects, + ADD), **SQL Workspace** (write/run queries; personal & project history) | Navigation = the ERP main menu; Explorer = the folder tree of companies/ledgers; SQL Workspace = the report writer window. |
| **Schema / Details / Preview tabs** | Column names & types / metadata like creation date / first rows | Schema = the file layout spec you got with every 401(k) vendor file; Preview = opening the file to eyeball the first 20 rows before loading. |
| **Public datasets** | Free datasets under `bigquery-public-data` (e.g., NOAA lightning, Austin 311); star it in Explorer to search them | Like BLS wage tables — reference data someone else collected that you can query directly. |
| **Sandbox vs. free trial** | Sandbox: free, no card, max 12 projects, can't INSERT/UPDATE records, processing limits — enough for this course. Free trial: $300 / 90 days, card required, no auto-charge; upgrade keeps projects, trial→sandbox does not | Sandbox is read-only access to the ledger; trial is full posting rights. Read-only is fine for reviewing — and safer. |
| **Dataset / Table** (BigQuery) | Dataset = a container (e.g., `movie_data`); Table = the actual data inside it (e.g., `movies`) | Dataset = the company folder; table = the payroll register file inside it. Fully qualified: `` `projectID.movie_data.movies` `` |
| **.csv file** | Plain-text table; values separated by commas; universally importable/exportable | The interface file format of your whole career — every 401(k), garnishment, and GL export you ever sent or received. |
| **Column name character map V2** (BigQuery upload) | Advanced option that lets column headers contain parentheses; without it the table creation fails | The vendor upload that rejects your file because a header has "(hrs)" in it. Same fix: adjust the mapping, not the data. |

### Sorting vs. filtering — one line each (exam favorite!)
- **Sorting** = *arranges* the data in a meaningful order (ranks, chronological lists, grouping like with like)
- **Filtering** = *shows only* the data meeting criteria; hides the rest — reversible
- **Both** work in spreadsheets **and** SQL databases; combine them to organize only what's relevant

### The one-column sort trap (from "Sort datasets in spreadsheets")
- **Sort sheet** (Data → Sort sheet → by column B, A→Z): every row moves together. Safe.
- **Sort range** on a single highlighted column (Data → Sort range → column A, A→Z): only that column moves; every row is now a lie. In the demo, *The Devil Inside* went from release date 2012-01-06 to 2015-06-16 — because the title moved but the dates didn't.
- Rule: **each row is one observation** — sort the whole sheet, or select the full range, never one column.
- Bonus analyst instinct from the reading: after sorting by release date, the titles *also* looked alphabetical. Too neat = suspicious. The data had probably been sorted before and never restored. Same gut check as a bank rec that ties to the penny on the first try.

### Filter with SQL — the pattern (from "Step-by-step: Filter data with SQL")
```sql
SELECT *
FROM `projectID.movie_data.movies`
WHERE Genre = 'Comedy';
```
- `SELECT *` = every column; `FROM` = which table (project.dataset.table in backticks); `WHERE` = the filter
- Text values go in single quotes; replace `projectID` with your own project ID
- Run it → shorter list, only comedies. Payroll version: `WHERE pay_code = 'OT'`

### Upload a .csv to BigQuery — the recipe (from "Upload the movie dataset")
1. Explorer → three dots next to project → **Create dataset** → ID `movie_data`, Location type **Multi-region → US**, Google-managed encryption → CREATE DATASET
2. Click the dataset → **+ CREATE TABLE**
3. Source: **Upload** → Browse to `movie_data.csv` → format CSV
4. Destination: table name `movies`
5. Schema: **Auto detect**
6. Advanced options → **Column name character map = V2** (allows parentheses in headers; skipping this = table creation fails)
7. CREATE TABLE → click table → **Preview** to confirm

### .csv download/upload tips (from "Working with .csv files")
- Download: click the link/attachment; right-click → Save as (make sure extension is `.csv`); or **Alt+click** to force download
- Chrome sometimes opens a .csv in a tab instead: File → Save as Google Sheets → File → Download → Comma Separated Values (.csv)
- Upload: find the platform's Upload/Import button or drag-and-drop area; file lands in Downloads by default; watch for **size/format limits** on the platform

## 🗣️ Teach it to a friend

Every analysis starts by organizing the data, and the two basic tools are sorting and
filtering. Sorting puts rows in a meaningful order — alphabetical, by date, biggest to smallest —
so you can rank things or see them grouped. Filtering hides everything except the rows that
match what you're looking for, and when you clear it the data snaps back to normal, so it's
great for hunting errors and outliers. You can do both in a spreadsheet (Data → Sort sheet, or
the filter dropdowns) or in SQL, where `WHERE` is the filter and `ORDER BY` is the sort. The
big spreadsheet trap: sorting one column by itself scrambles the rows, because each row is one
record — always sort the whole sheet. When the data is too big for a spreadsheet you use
BigQuery: create a dataset, upload a .csv as a table, and query it in the SQL Workspace. And
.csv is the universal plain-text table format that moves data between all these tools — comma-
separated, rows and columns, works everywhere.

## 🃏 Flashcards

**Q:** What's the difference between sorting and filtering?
**A:** Sorting arranges data in a meaningful order (ascending/descending by a chosen metric); filtering displays only the data that meets specified criteria and hides the rest.

**Q:** Why is filtering useful for finding errors or outliers?
**A:** You can zero in on the rows that contain errors/outliers, fix or flag them, then remove the filter and return the data to its original organization.

**Q:** What is an outlier?
**A:** A data point that is very different from similarly collected data and might not be a reliable value.

**Q:** In a spreadsheet, what happens if you sort a single column with "Sort range" instead of sorting the whole sheet?
**A:** Only that column reorders; the rest of the row stays put, so the data across rows becomes jumbled/incorrect (each row is one observation, so you've broken the observations).

**Q:** Which SQL clause filters rows? Write an example.
**A:** `WHERE` — e.g., `SELECT * FROM \`projectID.movie_data.movies\` WHERE Genre = 'Comedy';`

**Q:** How are items in a pivot table's row/column areas sorted by default, and what changes when you set descending?
**A:** Ascending by any custom list first, otherwise ascending by default. Setting descending creates a rule that keeps controlling the sort even after new data is added.

**Q:** Name the three main components of the BigQuery console.
**A:** The Navigation pane, the Explorer pane, and the SQL Workspace.

**Q:** What are the Schema, Details, and Preview tabs for a BigQuery table?
**A:** Schema = column names (and types); Details = metadata such as creation date; Preview = the first rows of the data.

**Q:** Sandbox account vs. free-of-charge trial — key differences?
**A:** Sandbox: free, no payment info, max 12 projects, limits on data processed, can't insert or update records. Free trial: $300 credit for 90 days, requires payment info but no automatic charge. Sandbox is enough for all activities in this course.

**Q:** If you upgrade a BigQuery account, do your projects transfer? What about trial → sandbox?
**A:** Upgrading (sandbox or trial → paid) retains and transfers all projects. Going from an expired trial to a sandbox does NOT transfer projects — it's like starting from scratch.

**Q:** When uploading the movie .csv to BigQuery, which Advanced option must you change and why?
**A:** Column name character map → V2, so parentheses in column names are accepted; otherwise the table fails to create.

**Q:** What is a .csv file and why do analysts use it so much?
**A:** A plain-text file with a table structure (rows and columns, values separated by commas). It's easy to read/edit and has widespread compatibility — nearly every analysis tool imports and exports it.

**Q:** A .csv opens in a new Chrome tab instead of downloading. What do you do?
**A:** File → Save as Google Sheets, then File → Download → Comma Separated Values (.csv). (Alt+click on the link also forces a download.)

**Q:** What is the fully qualified table name format in BigQuery?
**A:** `` `projectID.dataset.table` `` in backticks — e.g., `` `projectID.movie_data.movies` ``.

## 💡 How I'll actually use this

- **flask-analytics-app — the `/query` page:** it already runs SQL with `WHERE` and `ORDER BY`. This module is the textbook version of exactly that page: `WHERE` = filter, `ORDER BY` = sort. Next step: add a couple of saved example queries to the page (e.g., filter to one category then sort descending) so a visitor sees sort + filter *combined*, which the reading calls out as the real skill.
- **nyc-payroll-explorer:** the NYC payroll CSV is the .csv workflow from this module at scale — download, check size limits, upload. Load a slice into BigQuery (dataset `nyc_payroll`, table `citywide`, Auto detect schema, and remember the **V2 character map** if headers have parentheses), then run `WHERE agency_name = '...' ORDER BY regular_gross_paid DESC` to find outliers — the same overtime-audit filter I've run in Excel for years, now in SQL.
- **The one-column-sort trap is a portfolio talking point:** I can explain *why* sorting a single column corrupts a dataset in payroll terms (checks land on the wrong names) — that's data integrity from Course 4 meeting sorting from Course 5. Worth a sentence in the nyc-payroll-explorer README under "data handling."
- **Job hunt:** every analyst posting says "filter and sort large datasets in Excel and SQL." Interview line: *"Sorting and filtering are how I've reviewed payroll registers and GL exports for 20 years — sort by gross to catch outliers, filter to a cost center to reconcile it. In Course 5 I moved the same workflow into SQL with WHERE and ORDER BY on BigQuery, and I use it in my Flask query app."*
- **BigQuery hygiene:** stay on the sandbox for now (no card, enough for this course); star `bigquery-public-data` in Explorer so public datasets are searchable; keep the movie_data upload recipe above as my checklist for any future CSV upload.
