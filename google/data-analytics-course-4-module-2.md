# Google Data Analytics — Course 4, Module 2: Clean Data for More Accurate Insights

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 2 readings + module 2 glossary

## 🎯 What this module is about (one sentence)

Real data arrives dirty — duplicated, outdated, incomplete, wrong, or inconsistent — and this
module covers how to recognize each kind, the pitfalls that trip analysts up while fixing it, the
spreadsheet tools and functions that do the fixing, and how to make the cleaning repeatable
(CSV handling, checklists, automation).

**Sue's note:** data cleaning IS reconciliation. Every technique in this module is something you
already do at month-end under a different name — tying out two registers, chasing blanks,
fixing the one line where somebody keyed $1,000 instead of $100, splitting "Last, First" into
two fields, TRIM-ing the trailing space that breaks a VLOOKUP. The course just names the moves.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Dirty data** | Data that is incomplete, incorrect, or irrelevant to the problem being solved | The payroll import file before you've reconciled it: it "loaded," but you wouldn't sign the certified report off it yet. |
| **Clean data** | Data that is complete, correct, and relevant to the problem being solved | The register after tie-out: every employee present, every number traces, nothing in it that doesn't belong. |
| **Duplicate data** | Any record that inadvertently shares data with another record — from manual entry, batch imports, or migrations | The same employee loaded twice from a batch file → two paychecks, inflated headcount, an overstated 941. |
| **Outdated data** | Data superseded by newer, more accurate information — people change roles, systems get retired | A terminated employee still active in the benefits file; last year's pay rate still on the roster after a raise. |
| **Incomplete data** | Data missing important fields — from improper collection or bad entry | New hire with no tax status, no direct-deposit account, no department code. Can't run payroll until it's filled. |
| **Incorrect / inaccurate data** | Complete but wrong — human error at input, fake or mock data | -$200 in the dues column, a $0.73 price that should be $7.30, a rate keyed as 15.00 instead of 51.00. |
| **Inconsistent data** | Different formats representing the same thing — stored wrong or mangled in transfer | "NY," "N.Y.," "New York" all in one state column; dates as 3/1/24 in one row and 2024-03-01 in the next. |
| **Data validation** | A tool for checking the accuracy and quality of data (drop-downs, allowed ranges, required entries) | Payroll system edits and lookup tables: only approved deduction codes, pay rate within the grade's range. Prevent, don't repair. |
| **Conditional formatting** | Changes how cells look when values meet a condition (e.g., highlight blanks, highlight length ≠ 6) | Highlighting every blank SSN cell red before the file goes to the carrier — the visual "what's missing" pass. |
| **Remove duplicates** | Spreadsheet tool that finds and deletes duplicate rows automatically | De-duping the census file before the 401(k) upload — but back it up first (see pitfalls: a "duplicate" may be a real second check). |
| **Split (text to columns)** | Divides text around a delimiter and puts each piece in its own cell | Splitting "Rivera, Susan" into last/first, or "Dept-Location" codes into two fields. Also fixes numbers stored as text. |
| **Delimiter** | The character marking the boundary between data items (comma, tab, pipe) | The comma in a .csv; the pipe in a GL export. Pick the wrong delimiter on import and every column shifts. |
| **CONCATENATE** | Joins two or more text strings — add `" "` between them for a space | Building "Street + Suite" into one address line, or First + " " + Last for a mailing label. |
| **TRIM** | Removes leading, trailing, and repeated spaces | The invisible reason your VLOOKUP returns #N/A: "Smith " ≠ "Smith". Every payroll analyst has lost an hour to this. |
| **LEN / Length** | Returns the number of characters in a text string | SSN must be 9, ZIP must be 5, employee ID must be 6 — a LEN column + conditional formatting flags every violator instantly. |
| **LEFT / RIGHT / MID** | Return a set number of characters from the left / right / middle of a text string (a **substring**) | Pulling the 2-digit state code out of a location string, the year off a pay-period ID, the last 4 of an SSN for a report. |
| **Text string / Substring** | A group of characters in a cell / a smaller piece of it | The full account code vs. the department segment inside it. |
| **COUNTIF** | Counts cells in a range that meet a condition (`"<100"`, `">500"`) | "How many hourly rates are below minimum wage?" "How many dues are negative?" — a one-cell exception report. |
| **Pivot table** | Summarization tool: sort, group, count, total, average — a clutter-free view for spotting oddities | Summarizing gross pay by department to see the one department that's 3× normal — same as your variance review. |
| **VLOOKUP** | Vertically searches a column for a value and returns the matching info from another column (`FALSE` = exact match) | Pulling names onto a file that only has employee IDs; matching HR's roster to payroll's register — the workhorse of every reconciliation. |
| **Plotting** | Quick chart to spot outliers or skew | Bar chart of pay rates makes the $0.73 stand out at a glance — eyes catch what a scroll misses. |
| **Data mapping** | Matching fields from one data source to another (critical for migrations and merges) | The conversion crosswalk: old system's "EE_ID" = new system's "employee_number," old dept codes → new. You've built these. |
| **Data merging** | Combining two or more datasets into one | Merging two associations' membership lists after a **merger**; combining two entities' payroll files after an acquisition. |
| **Compatibility** | How well two or more datasets can work together | Do both files use the same date format, same ID scheme, same units? If not, map before merging. |
| **Field length** | Tool for setting how many characters can be keyed into a field | Setting the SSN field to exactly 9 so an extra digit can't be entered — a constraint at the source. |
| **Unique** | A value that can't have a duplicate | Employee ID, check number, transaction ID — the keys you'd never allow twice. |
| **Null** | An indication that a value does not exist in the dataset | Blank 401(k) % — not zero, *unknown*. Don't sum it as 0 without confirming. |
| **.csv file** | Plain-text table; rows on lines, values separated by commas — near-universal compatibility | The export format every payroll system, bank, and carrier speaks. Download → inspect → upload. |
| **Workflow automation** | Automating parts of the work (triggers, scripts, cleaning where the data lives) | The macro/script that reformats the timekeeping export every pay period instead of you doing it by hand — build once, reuse. |
| **Data engineer / Data warehousing specialist** | Engineer: transforms data into a usable format and builds reliable infrastructure. Warehousing specialist: develops processes to store and organize data | The IT people who own the HRIS-to-payroll interface and the reporting database — your upstream partners when the source is broken. |

### The five types of dirty data (exam favorite!)

| Type | Cause | Harm | Payroll version |
|---|---|---|---|
| **Duplicate** | Manual entry, batch imports, migration | Skewed metrics, inflated counts, retrieval confusion | Employee loaded twice → double paycheck |
| **Outdated** | People change roles/companies; systems obsolete | Inaccurate insights and decisions | Old pay rate still on file after a raise |
| **Incomplete** | Improper collection, bad data entry | Lower productivity, inaccurate insights, can't complete essential services | New hire missing tax status |
| **Incorrect/inaccurate** | Human error, fake or mock data | Bad decisions → revenue loss | $1,000 keyed instead of $100 |
| **Inconsistent** | Stored incorrectly, errors in transfer | Contradictory data points, can't classify/segment | "NY" vs "New York" vs "N.Y." |

Business impact figures from the reading: banking inaccuracies cost **15–25% of revenue**; up to
**25%** of B2B contacts are inaccurate; **99%** of companies are working on data quality;
duplicate records are **10–20%** of a hospital's EHR.

### Common data-cleaning pitfalls (the "don't" list)
1. **Not checking for spelling errors** — "John" vs "Jon"; spellcheck won't catch names or addresses.
2. **Forgetting to document errors** — a fix log saves you next time and lets you backtrack. *(Audit workpaper habit.)*
3. **Not checking for misfielded values** — "Spain" in the city column: correctly formatted, wrong field, invisible to filters.
4. **Overlooking missing values** — a missing week of transactions quietly understates the quarter.
5. **Only looking at a subset** — clean one source of several and you miss duplicates across them.
6. **Losing track of business objectives** — interesting snowfall pattern ≠ the rainy-days question. Stay on task.
7. **Not fixing the source of the error** — if the shared tracker keeps breaking, fix the entry setup, not the cells.
8. **Not analyzing the system before cleaning** — the mechanic finds the cause before fixing the car.
9. **Not backing up before cleaning** — duplicate the tab/sheet first (the reading literally does this before Remove duplicates).
10. **Not accounting for cleaning in deadlines** — cleaning takes real time; build it into the ETA you give stakeholders.

### Your cleaning checklist (from "Develop your approach")
Default "what to search for" list — build one and keep it:
- **Size of the dataset** (bigger = more issues, more time)
- **Number of categories/labels** (informs merge and migration strategy)
- **Missing data**
- **Unformatted / inconsistently formatted data**
- **Data types present** (numeric, categorical, text → picks the cleaning method)
- Plus: decide your **preferred methods/tools** ahead of time so you're not inventing a plan mid-clean.

### Spreadsheet cleaning moves (step-by-step readings, condensed)
- **Highlight blanks:** select range → Format → Conditional formatting → "Cell is empty" → bright color.
- **Remove duplicates:** duplicate the tab first → Data → Data cleanup → Remove duplicates → tick "Data has header row."
- **Consistent dates:** select column → Format → Number → Date.
- **Split text to columns:** Data → Split text to columns; delimiter auto-detected (or set manually). Also strips stray quotes so numbers-stored-as-text become numbers again.
- **COUNTIF exception counts:** `=COUNTIF(I2:I72,"<100")` and `=COUNTIF(I2:I72,">500")` → then fix the -$200 and the $1,000.
- **LEN check:** `=LEN(A2)` in a helper column, then conditional format "is not equal to 6" → the 7-character ID lights up.
- **Substrings:** `=LEFT(A2,5)` → `51993`; `=RIGHT(A2,4)` → `Masc`; `=MID(D2,4,2)` → the state code starting at character 4.
- **CONCATENATE:** `=CONCATENATE(D2," ",E2)` → `25 Dyas Rd Ste. 101` (the `" "` adds the space).
- **TRIM:** `=TRIM(C2)`.
- **VLOOKUP across sheets:** `=VLOOKUP(A2,'Sheet 2'!A1:B31,2,FALSE)` — value, range, column number, exact match.
- **Pivot for perspective:** rows = Total (descending) + Products → the top two products jump out.
- **Plot to spot outliers:** column chart of prices → the $0.73 that should be $7.30.

### CSV handling
- .csv = plain text, rows and columns, comma-separated; imported/exported by nearly every tool.
- **Download:** click the link/attachment; right-click → Save as (make sure the extension is .csv); or Alt+click to force download. In Chrome, if it opens in a tab: File → Save as Google Sheets, then File → Download → CSV.
- **Upload:** find Upload/Import, choose the file (usually in Downloads), start the upload; watch for platform size/format limits.

### Workflow automation: what can and can't be automated
| Task | Automatable? | Why |
|---|---|---|
| Communicating with team/stakeholders | **No** | No replacement for person-to-person |
| Presenting findings | **No** | Making data understandable is human work |
| Preparing and cleaning data | **Partially** | Scripts can detect missing values, etc. |
| Data exploration | **Partially** | Tools speed up visualizing; the exploring is still yours |
| Modeling the data | **Yes** | Tools can fully automate the stages |

Best practice: **clean data where it lives** (a script in the folder/database) so nobody repeats the steps.

## 🗣️ Teach it to a friend

Dirty data comes in five flavors: duplicated, outdated, incomplete, incorrect, and inconsistent —
and each one has a cause (bad entry, batch imports, systems aging out, sloppy transfer) and a
cost. Cleaning it is a reconciliation: back up first, know what you're looking for (a checklist),
then use the tools — conditional formatting to light up blanks, Remove Duplicates, Split to break
apart combined fields, TRIM to kill stray spaces, LEN to catch IDs that are the wrong length,
COUNTIF to count the values outside the allowed range, LEFT/RIGHT/MID to pull pieces out of a
code, CONCATENATE to glue pieces together, VLOOKUP to match one list to another, and a pivot
table or a quick chart to spot the outlier your eyes would miss. The pitfalls are all about
discipline: document what you fix, fix the source not just the symptom, don't clean only part of
the data, don't chase interesting rabbit holes, and budget the time. Data moves around as .csv
files, and anything you find yourself doing every time should become a script that runs where the
data lives.

## 🃏 Flashcards

**Q:** Name the five types of dirty data.
**A:** Duplicate, outdated, incomplete, incorrect/inaccurate, and inconsistent.

**Q:** What's the difference between incomplete and incorrect data?
**A:** Incomplete = important fields are missing. Incorrect = the data is complete but wrong.

**Q:** What is inconsistent data, and what commonly causes it?
**A:** Different formats representing the same thing (e.g., "NY" and "New York"); caused by data stored incorrectly or errors during transfer.

**Q:** What is a misfielded value?
**A:** A value entered in the wrong field — e.g., "Spain" in the city column. Often correctly formatted, so it's easy to miss.

**Q:** Why should you back up data before cleaning?
**A:** If the program crashes or a change breaks the dataset, you can restore the saved version — the reading duplicates the tab before running Remove duplicates.

**Q:** What does TRIM do?
**A:** Removes leading, trailing, and repeated spaces from a text string.

**Q:** What's the difference between LEFT, RIGHT, and MID?
**A:** LEFT returns N characters from the start of a string, RIGHT from the end, MID a segment from the middle (starting position + length).

**Q:** How would you make CONCATENATE put a space between two fields?
**A:** Add a `" "` string as its own argument: `=CONCATENATE(D2," ",E2)`.

**Q:** What does `=COUNTIF(I2:I72,"<100")` return?
**A:** The number of cells in I2:I72 whose value is less than 100 — a quick way to count out-of-range values.

**Q:** How can LEN help clean data?
**A:** It returns character count; pair it with conditional formatting ("is not equal to 6") to flag values of the wrong length, like a 7-digit ID.

**Q:** What is a delimiter?
**A:** A character that marks the beginning or end of a data item — the comma in a .csv, used by Split to break text into columns.

**Q:** What is data mapping and why does it matter?
**A:** Matching fields from one data source to another; it's critical for data migration, integration, and merging datasets.

**Q:** In `=VLOOKUP(A2,'Sheet 2'!A1:B31,2,FALSE)`, what do the 2 and FALSE mean?
**A:** Return the value from the 2nd column of the range; FALSE = exact match only.

**Q:** Which analyst tasks cannot be automated?
**A:** Communicating with team/stakeholders and presenting findings. Cleaning and exploration are partially automatable; modeling can be fully automated.

**Q:** What does "clean data where it lives" mean?
**A:** Run cleaning (e.g., a script) directly in the storage location so the whole team benefits and nobody repeats the steps.

**Q:** Who is a data engineer vs. a data warehousing specialist?
**A:** Data engineer transforms data into a useful format and builds reliable infrastructure; data warehousing specialist develops processes to store and organize data.

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** write a cleaning checklist for the NYC payroll CSV *before* charting — dataset size, distinct agencies/titles (categories), Nulls per column, inconsistent title casing/whitespace (TRIM equivalents), negative or absurd pay values (COUNTIF-style range checks in pandas). Log every fix in a `CLEANING_NOTES.md` — the "document your errors" pitfall, done as an audit workpaper.
- **flask-analytics-app:** the CSV upload path is exactly the download/upload flow from this module — add validation on import (required columns, field length, allowed ranges) so dirty rows are rejected at the door. That's "fix the source, not the symptom."
- **Reusable script:** the "clean where it lives" idea = one Python function (`clean_payroll(df)`) that does the TRIM / de-dup / date-format / type-cast pass, run on every refresh instead of by hand. Same instinct as the payroll import macro.
- **Spreadsheet muscle memory:** LEN + conditional formatting for ID length, Split for "Last, First," VLOOKUP with FALSE, TRIM before every lookup — I've done all of these on payroll files; now I can name them in an interview.
- **Interview line:** "Data cleaning is reconciliation. For 20 years I found the duplicate check, the outdated rate, the missing tax status, the keyed-wrong amount, and the inconsistent code — that's the five types of dirty data. Now I do it with LEN, TRIM, COUNTIF, pivots, and Python instead of a red pen."
