# Google Data Analytics — Course 5, Module 4: Perform Data Calculations (SQL Math, Temp Tables, Pivot Tables, SUMIFS/COUNTIFS, Validation)

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 4 readings (Embed simple calculations with SQL, Work with temporary tables, Elements of a pivot table, Use pivot tables in analysis, Functions with multiple conditions, Types of data validation, Your intermediate guide to SQL) + module 4 glossary + Course 5 glossary

> *(the "coming up next" reading is skipped — nothing to study there)*

## 🎯 What this module is about (one sentence)

This module is the calculator part of analysis: doing arithmetic directly in SQL, parking
intermediate results in temporary tables, summarizing with pivot tables and multi-condition
functions (SUMIFS/COUNTIFS), and validating the data before you trust any of the numbers.

**Sue's note:** this is the payroll register in disguise. Calculated columns are gross = hours ×
rate. Temp tables are the scratch worksheet you build the register from. Pivot tables are the
department summary at the bottom. SUMIFS is "total OT for Finance in Q2." Data validation is
the edit checks the payroll system runs before it lets a batch post. You've done every one of
these — just with different names.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Calculations in SQL** | Use `+ - * /` (and `%`) right in the SELECT to make a new column, named with AS: `Small_Bags + Large_Bags + XLarge_Bags AS Total_Bags_Calc` | `hours * rate AS gross_pay`, `gross - taxes - deductions AS net_pay` — computed on the fly instead of stored. |
| **Verifying a stored total** | Recompute a total column from its parts and compare (`_Calc` suffix convention) | Re-adding the components of gross to prove the system's gross column is right — a footing check. |
| **Percentages in SQL** | `(part / whole) * 100 AS pct` — parentheses force the division first | `(ot_hours / total_hours) * 100 AS ot_pct` by department. |
| **Division-by-zero guard** | Filter out zero denominators: `WHERE Total_Bags <> 0` | An employee with zero total hours can't have an OT percentage — exclude or handle before you divide. |
| **Modulo (`%`)** | Returns the remainder of a division | Even/odd pay periods, "every 3rd employee" for audit sampling, or splitting minutes into hours and remainder. |
| **Underscores in names** | Use `Total_Bags` not `Total Bags` — spaces confuse servers; underscores stay readable | Column headers you'd never let through a payroll import file anyway. |
| **Temporary table** | A table that exists only during the session and is dropped when it ends; a holding area for pre-processing, staging, or a filtered subset | A scratch worksheet: filter the register down to one department once, then run five calculations off the filtered copy instead of re-filtering each time. |
| **`WITH ... AS (...)`** (BigQuery way) | Named subquery = temp table for the rest of the query | Name the scratch tab, then reference it by name. |
| **`SELECT ... INTO`** (SQL Server / MySQL, *not* BigQuery) | Store a query's result in a new temp table | Same idea, different dialect. |
| **`CREATE TEMP TABLE` / `DROP TABLE`** | User-managed temp table with defined columns; drop it when done | Building your own worksheet with defined columns, then deleting it at period close so it doesn't clutter the workbook. |
| **Drop vs delete** | DROP removes rows *and* the table definition; DELETE removes rows but keeps the structure | Deleting the rows off a scratch tab vs. deleting the tab. |
| **Local vs global temp table** | Local = only your session sees it; global = all users, deleted when every connection closes | Your personal scratch tab vs. a shared workbook tab. You'll almost always use local. |
| **Pivot table** | Spreadsheet tool to sort, reorganize, group, count, total, or average data — without changing the source. Four parts: rows, columns, values, filters | The payroll register summary: rows = department, values = SUM of gross and COUNT of checks, filter = this pay period. |
| **Rows / Columns / Values / Filters** | Rows group horizontally; columns group vertically; values are what you measure (SUM, AVERAGE, COUNT); filters limit what's included | Rows = department, columns = pay period, values = SUM of gross, filter = exclude terminated employees. |
| **Calculated field** | A new field in a pivot table computed from other fields | "Average cost per check" = SUM of gross ÷ COUNT of checks, computed inside the pivot. |
| **Summary table** | A table that summarizes statistical information about data — often what a pivot table produces | The one-page department roll-up you hand the controller. |
| **SUMIF → SUMIFS** | `SUMIF(range, criterion, sum_range)` = one condition; `SUMIFS(sum_range, crit_range1, crit1, [crit_range2, crit2, ...])` = many (up to 127) | SUMIF: total travel expense. SUMIFS: total OT **for Finance** **in Q2** **for hourly employees**. |
| **COUNTIF → COUNTIFS** | `COUNTIF(range, criterion)` = one condition; `COUNTIFS(crit_range1, crit1, [crit_range2, crit2, ...])` = many | COUNTIF: days an employee was absent. COUNTIFS: how many Finance employees had OT over 10 hours this period. |
| **Argument-order gotcha** | SUMIF puts `sum_range` **last**; SUMIFS puts it **first** | The number-one reason a SUMIFS returns 0 — swap the arguments and it works. |
| **SUMPRODUCT** | Multiplies arrays element-by-element and sums the products | Gross payroll in one cell: `=SUMPRODUCT(hours_range, rate_range)` — no helper column. |
| **Array** | A collection of values in spreadsheet cells | A whole column of hours treated as one thing. |
| **Profit margin** | Cents of profit per dollar of sale, as a percentage | Not payroll, but the same math as "benefit cost as % of gross." |
| **Data validation process** | Checking and rechecking data quality so it's complete, accurate, secure, and consistent | The pre-transmit checklist before a payroll batch goes to the bank. |
| **Data security** | Protecting data from unauthorized access or corruption | SSNs and bank accounts — locked files, role-based access, no emailing spreadsheets. |
| **Types of data validation** (six) | Data type, data range, data constraint, data consistency, data structure, code validation — see table below | The edit checks in every payroll system, one by one. |

### Types of data validation (exam favorite!)

| # | Type | Purpose | Reading's example | Limitation | Payroll version |
|---|---|---|---|---|---|
| 1 | **Data type** | Value matches the field's type | School grade must be numeric | 13 passes as a number but isn't a valid grade → also need range | Hours must be a number, not "forty" |
| 2 | **Data range** | Value falls within an acceptable min–max | Grade between 1 and 12 | 11.5 is in range but half-grades don't exist → also need constraint | Hours 0–80 per week |
| 3 | **Data constraint** | Value meets specific conditions/criteria (type, length, format...) | Grade must be a whole number | 13 is a whole number but not a valid grade → also need range | SSN exactly 9 digits; deduction code from the approved list |
| 4 | **Data consistency** | Value makes sense next to related data | Ship date can't be before production date | Consistent can still be wrong | Term date can't be before hire date; net ≤ gross |
| 5 | **Data structure** | Data follows a required structure/format | Web page must follow a prescribed structure | Structure right, content still wrong | The ACH file layout: correct record lengths, but a wrong account number still goes through |
| 6 | **Code validation** | The application code actually performs checks 1–5 on user input | Problems: multiple types allowed, no range checks, unterminated strings | Can't anticipate every input | Testing that the timekeeping system actually rejects a 400-hour week instead of assuming it does |

Key point from the reading: no single check is enough — type + range + constraint together catch what any one misses. As a junior analyst you may not run all six, but you should **ask if and how the data was validated** before working with it.

### Embedding calculations in SQL — the avocado walk-through
```sql
-- 1. Verify a stored total by recomputing it
SELECT
  Date,
  Region,
  Small_Bags,
  Large_Bags,
  XLarge_Bags,
  Total_Bags,
  Small_Bags + Large_Bags + XLarge_Bags AS Total_Bags_Calc
FROM `your-project.avocado_data.avocado_prices`;

-- 2. Percentage of the total, guarding against division by zero
SELECT
  Date,
  Region,
  Total_Bags,
  Small_Bags,
  (Small_Bags / Total_Bags) * 100 AS Small_Bags_Percent
FROM `your-project.avocado_data.avocado_prices`
WHERE Total_Bags <> 0;
```
- Query 1 is a footing check: does the stored `Total_Bags` equal the sum of its parts? Add `_Calc` to the new column and compare side by side.
- Query 2 crashed with "division by zero" the first time — the `WHERE Total_Bags <> 0` line is the fix. Expect this every time you divide by a column.
- Payroll version of the pair: `reg_pay + ot_pay + other_pay AS gross_calc` next to the stored `gross`, then `(ot_pay / gross) * 100 AS ot_pct WHERE gross <> 0`.

### Temporary tables — three ways to make one
```sql
-- BigQuery: WITH (a named subquery that acts like a temp table)
WITH long_trips AS (
  SELECT *
  FROM existing_table
  WHERE tripduration >= 60
)
SELECT COUNT(*) FROM long_trips;

-- SQL Server / MySQL (NOT BigQuery): SELECT ... INTO
SELECT *
INTO AfricaSales
FROM GlobalSales
WHERE Region = "Africa";

-- User-managed (BigQuery: CREATE TEMP TABLE; others: CREATE TABLE)
CREATE TEMP TABLE table_name (
  column1 datatype,
  column2 datatype
);
-- ... use it ...
DROP TABLE table_name;
```
- What temp tables are for: **pre-processing** (hold values across a series of calculations), **staging** (collect results of several queries to query or merge later), and **filtered subsets** (filter once, reuse many times, fewer commands = cleaner).
- Auto-deleted at session end, but **drop them yourself** when done — on a busy database cleanup may not be immediate.
- Each database has its own syntax; the course focuses on BigQuery's `WITH`. My flask app is on SQLite, which supports both `WITH` and `CREATE TEMP TABLE`.

### Pivot tables — the four parts and a worked example
From the reading: a department store analyst wanted total sales and product count per department, and which department earned the most.
- **Rows:** department (grouped, sorted **descending by SUM of sales**)
- **Values (as columns):** `price` summarized by SUM; `product_id` summarized by COUNTA
- Result: Toys on top at $3,045.95 / 49 products — answered without touching the raw data.

Setup habit: Insert → Pivot table → **New sheet**, so raw data and analysis stay separate and calculations live in one place. Filters work like normal sheet filters (e.g., only movies under $10M revenue). Values can be SUM, AVERAGE, COUNT/COUNTA, and calculated fields.

*Payroll version:* rows = department, values = SUM of gross + COUNT of checks, sorted descending by gross → the department cost ranking the CFO asks for every quarter, in about 30 seconds.

### SUMIFS / COUNTIFS — syntax side by side (from the fuel-product table)
Table columns: A Product, B Region, C Quarter, D Sales.
```
=SUMIF(A2:A8, "ProductA", D2:D8)                              → all ProductA sales
=SUMIFS(D2:D8, A2:A8, "ProductA", B2:B8, "East", C2:C8, "Q1")   → ProductA, East, Q1 only
=COUNTIF(A2:A8, "ProductA")                                   → # of ProductA transactions
=COUNTIFS(A2:A8, "ProductA", B2:B8, "East", C2:C8, "Q2")        → # ProductA/East/Q2 transactions
```
- **SUMIFS: sum_range first**, then criteria pairs. **SUMIF: sum_range last.** Memorize this.
- **COUNTIFS** has no sum_range — just criteria pairs, same order as SUMIFS.
- Square brackets in docs = optional; the ellipsis = repeat as many pairs as needed (up to 127).
- Related multi-condition tools the reading points to: `IFS`, `IF` with `AND/OR/NOT`, VLOOKUP and INDEX/MATCH with multiple criteria.
- SQL equivalent of SUMIFS: `SELECT SUM(sales) FROM t WHERE product = 'ProductA' AND region = 'East' AND quarter = 'Q1'` — same conditions, different syntax.

### Your intermediate guide to SQL
The reading is a wrapper for a downloadable PDF ("Your-Intermediate-Guide-to-SQL") that
goes deeper on functions already covered and adds new ones. Grab it from the course page and
file it next to my [sql-reference-guide](sql-reference-guide.md) — the two together are my SQL
desk reference.

### Glossary terms not covered above (module 4 + Course 5 glossary)

| Term | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **GROUP BY** | SQL clause that groups rows with the same values into summary rows | The subtotal-by-department line; SQL's version of a pivot table's Rows box. |
| **Underscores** | Lines used to connect text characters (in names) | `net_pay`, not `net pay`. |
| **Aggregation** | Collecting many separate pieces into a whole | Register lines → department totals. |
| **LIMIT** | Caps rows returned | "Top 10 highest gross" — `ORDER BY gross DESC LIMIT 10`. |

## 🗣️ Teach it to a friend

SQL will do math for you: put `hours * rate AS gross` right in the SELECT and it computes a new
column on the fly — and always guard a division with `WHERE denominator <> 0`. When a
calculation has several steps, park the middle results in a temporary table (in BigQuery,
`WITH name AS (...)`) — it's a scratch worksheet that disappears when you log off. Pivot tables
are the spreadsheet way to summarize: drag department into Rows, gross into Values as SUM,
and you have a register summary without touching the raw data. When a plain SUMIF or COUNTIF
isn't enough because you have two or more conditions, use SUMIFS/COUNTIFS — just remember
SUMIFS wants the sum range *first*. And before you trust any of it, validate: is each value the
right type, in range, meeting the field's constraints, consistent with related fields, in the
right structure — and does the input code actually enforce all that?

## 🃏 Flashcards

**Q:** How do you add a calculated column in SQL?
**A:** Put the arithmetic in the SELECT and alias it: `Small_Bags + Large_Bags + XLarge_Bags AS Total_Bags_Calc`.

**Q:** Your percentage query fails with "division by zero." Fix?
**A:** Filter out zero denominators: `WHERE Total_Bags <> 0`.

**Q:** Why use underscores instead of spaces in column names?
**A:** Spaces can confuse servers and applications; underscores avoid the problem and stay readable.

**Q:** What is a temporary table, and when does it disappear?
**A:** A database table that exists only temporarily on the server; automatically deleted when the SQL session ends (but drop it yourself as good practice).

**Q:** How do you create a temp table in BigQuery? In SQL Server/MySQL?
**A:** BigQuery: `WITH new_table AS (SELECT ... )` (or `CREATE TEMP TABLE`). SQL Server/MySQL: `SELECT ... INTO new_table FROM ...` (not supported in BigQuery).

**Q:** Name three uses of temporary tables.
**A:** Pre-processing (holding values across calculations), staging (collecting results of multiple queries), and storing a filtered subset you'll reuse.

**Q:** DROP TABLE vs deleting a temp table?
**A:** DROP removes the rows and the table definition (columns); DELETE removes rows but keeps the structure.

**Q:** Local vs global temporary tables?
**A:** Local: visible only to the user/connection that created it. Global: available to all users, deleted when all connections using it close.

**Q:** What are the four parts of a pivot table?
**A:** Rows, columns, values, filters.

**Q:** What is a calculated field?
**A:** A new field within a pivot table that carries out calculations based on the values of other fields.

**Q:** SUMIF vs SUMIFS syntax?
**A:** `SUMIF(range, criterion, sum_range)` — one condition, sum_range last. `SUMIFS(sum_range, criteria_range1, criterion1, [criteria_range2, criterion2, ...])` — many conditions, sum_range first.

**Q:** COUNTIFS syntax?
**A:** `COUNTIFS(criteria_range1, criterion1, [criteria_range2, criterion2, ...])`.

**Q:** How many conditions can SUMIFS take?
**A:** Up to 127.

**Q:** What does SUMPRODUCT do?
**A:** Multiplies arrays element by element and returns the sum of those products.

**Q:** Name the six types of data validation.
**A:** Data type, data range, data constraint, data consistency, data structure, code validation.

**Q:** Value 13 passes data-type validation for school grades (1–12). What else is needed?
**A:** Data range validation.

**Q:** Value 11.5 passes range validation for grades. What else is needed?
**A:** Data constraint validation (must be a whole number).

**Q:** What is data consistency validation? Give the reading's example.
**A:** Checking data makes sense in the context of related data — a shipping date can't be earlier than the production date.

**Q:** What does code validation check?
**A:** That the application code systematically performs the other validations on user input (common gaps: multiple types allowed, no range checks, poorly defined string endings).

**Q:** What does the modulo operator (%) return?
**A:** The remainder when one number is divided by another.

**Q:** What is the data validation process (glossary)?
**A:** Checking and rechecking data quality so it is complete, accurate, secure, and consistent.

## 💡 How I'll actually use this

- **flask-analytics-app (SQL query page):** add saved example queries that compute a column (`amount * qty AS line_total`), a percentage with a `WHERE denominator <> 0` guard, and a `WITH` temp table that filters once and aggregates after. SQLite supports `WITH` and `CREATE TEMP TABLE`, so this ports directly. Then add input validation on the upload path that maps to the six types — type, range, constraint, consistency — and document which ones the code enforces (that's "code validation" for my own app).
- **nyc-payroll-explorer:** the dataset has base salary, regular hours, OT hours, and OT pay — recompute a `gross_calc` and compare to the stored total (footing check), compute `ot_pct` by agency with the zero guard, and build the agency summary as a `WITH` temp table feeding the chart. Add a pivot-style summary view (rows = agency, values = SUM of pay, COUNT of employees) — the payroll register roll-up as a web page.
- **Spreadsheet side:** the next time I open a payroll-style workbook, rebuild the department summary as a pivot (rows = dept, values = SUM gross + COUNT checks, sorted descending) and replace any helper-column sums with SUMIFS/SUMPRODUCT. Faster, and it demonstrates the same skill in the tool most hiring managers still live in.
- **Job hunt:** the six validation types are an interview story waiting to happen — "here's how a payroll system validates a timesheet, type/range/constraint/consistency, and here's the time the code validation was missing and a 400-hour week posted." Concrete, memorable, and it shows I think about data quality before analysis.
- **Interview line:** "Calculated columns, temp tables, and pivot summaries are the payroll register — gross = hours × rate, a scratch worksheet to build it, and a department roll-up at the bottom. I've built that report a thousand times; now I build it in SQL."
