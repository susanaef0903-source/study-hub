# Google Data Analytics — Course 5, Module 2: Format and Adjust Data

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 2 readings + module 2 glossary (convert data in spreadsheets, from one type to another, strings in spreadsheets, manipulate strings with SQL, merge text strings, import & combine data, transform data with SQL, advanced spreadsheet tips)

## 🎯 What this module is about (one sentence)

Even clean data can be in the *wrong shape* — numbers stored as text, dates stored as strings,
first and last names in separate columns when you need one — so this module is about
**converting** data from one type or format to another and **combining** it (strings, columns,
tables), in both spreadsheets and SQL, before you analyze it.

**Sue's note:** this is the "why won't this column SUM?" module. Every GL export where the
amounts came in as text with a leading apostrophe, every 401(k) file where the SSN lost its
zeros, every time you built `LASTNAME, FIRSTNAME` from two HR columns — that's this module.
You've done all of it with Text-to-Columns and CONCATENATE; now you learn the SQL names
(`CAST`, `CONCAT`) and the pattern behind them.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Convert / format data** | Change data from one type or format to another (text → date, text → number, number → percent) so it behaves correctly in formulas and analysis; do it early, and keep an **entire column in one format** | The GL export where half of column D is real numbers and half is "text that looks like a number." Nothing totals until you convert the whole column — consistency is the rule you already live by. |
| **String → date** | Turn text like `20240115` or `1/15/24` into an actual date value the tool understands (Excel: DATEVALUE and text-to-date tricks; Sheets: date format menu) | Hire dates coming in from the ATS as text. Until they're real dates, DATEDIF, sorting by date, and "who's eligible on the 1st?" all break. |
| **String → number** | Text that *resembles* a number isn't one — convert it so it adds up and works in formulas (VALUE, multiply by 1, Paste Special, etc.) | Amounts pasted from a PDF or a vendor file that won't SUM. You've fixed this a hundred times with `=VALUE()` or the little green triangle. |
| **Number → percentage** | Format numbers to display as percentages (Excel percent format; Sheets `TO_PERCENT`) | Employer match rate 0.04 shown as 4%; 401(k) deferral percentages on the census. |
| **Currency format** | Apply the `$` shortcut so budget/revenue columns display as money | Formatting the Gross and Net columns before the register goes to the controller. |
| **`CONVERT` function** (spreadsheets) | `=CONVERT(value, "from_unit", "to_unit")` converts units of measurement — `=CONVERT(B2, "F", "C")`, `=CONVERT(D2, "mph", "m/s")` | Less common in payroll, but same shape as converting hours to minutes or annual salary to hourly — a formula that changes the *unit* without changing the *thing measured*. |
| **Lock data (Paste values only)** | A converted cell that still holds a formula will change if its source changes; **Copy → Paste special → Paste values only** freezes it as a plain value | Freezing a calculated accrual before month-end close so no one's later edit to the source silently rewrites a posted number. You've been burned by a live formula in a "final" file. |
| **String** | A sequence of characters — text; can contain letters, numbers, spaces, punctuation | Employee names, addresses, pay codes, and — annoyingly — sometimes SSNs and dollar amounts that *should* be numbers. |
| **`LEN`** | Returns the number of characters in a string: `=LEN(C2)` → 19 | The classic SSN check: `LEN` should be 9 (or 11 with dashes). Anything else = a leading zero got dropped or a character snuck in. |
| **`FIND`** | Returns the position of a character/substring inside a string: `=FIND(" ", C3)` → 11 (the space is the 11th character). **Case sensitive** | Finding where the comma sits in `Rivera, Susan` so you can split last from first — the prep step before LEFT/RIGHT. |
| **`LEFT` / `RIGHT`** | Return the first/last N characters: `=LEFT(D2, 10)` → date part of `2016-01-01 00:00:01`; `=RIGHT(C2, 8)` → the time part | `=LEFT(A2, 3)` to pull the department prefix off a cost-center code; `=RIGHT(SSN, 4)` for "last four" on a report. |
| **Concatenation** | Joining two or more text strings into one longer string | Building `LASTNAME, FIRSTNAME` or `EMPID-PAYPERIOD` as a unique key. |
| **`CONCATENATE`** (spreadsheets) | `=CONCATENATE(item1, " ", item2)` — the `" "` adds a space between items; add as many items as needed, comma-separated | `=CONCATENATE(B2, ", ", A2)` for last-comma-first; `=CONCATENATE(EmpID, "-", CheckDate)` for a reconciliation key. |
| **`CONCAT`** (SQL) | `CONCAT(first_name, ' ', last_name) AS full_name` — join fields; use `AS` to alias because SQL doesn't know what to call the new column | Same full-name build, in the query instead of a helper column. Also used to **generate a unique identifier** per row. |
| **`CONCAT_WS`** | "CONCAT With Separator" — `CONCAT_WS('.', 'www', 'your_company', 'com')` puts the separator between *every* piece | Building `dept.location.paycode` account strings without typing the dot three times. |
| **`\|\|` operator** (BigQuery) | Another way to concatenate: `book_name \|\| ' - ' \|\| edition`. Not universal — Microsoft SQL Server uses `+` instead | Different payroll systems, different report-writer syntax — same idea, check which dialect you're in. |
| **`IMPORTRANGE`** (Sheets) | `=IMPORTRANGE(spreadsheet_url, "Tab!A2:B6")` — pull a range from another spreadsheet into this one | The reading's own example is payroll: import retirement-contribution data into the year-end salary/bonus sheet to figure out who's eligible for company match. |
| **`INSERT INTO ... SELECT`** (SQL) | SQL has no import function; instead copy rows from one table into another: `INSERT INTO dest SELECT * FROM source WHERE condition` | Populating a "bonus-eligible" table from the employee master with `WHERE status = 'Active' AND hire_date < '2026-01-01'`. |
| **`CAST`** (SQL) | `CAST(expression AS typename)` — convert one data type to another: number → string, string → INT, date → string, date → DATETIME. ANSI standard, works across databases | `CAST(gross_pay AS NUMERIC)` when the upload read a dollar column as text. Type conversion = "text that should be a number." |
| **`SAFE_CAST`** (BigQuery) | Same syntax as CAST, but returns **NULL** instead of an error when a value can't be converted | The row where someone typed "N/A" in the hours column: CAST kills the whole query; SAFE_CAST gives you a NULL you can filter and investigate. |
| **`COERCION` / `UNIX_DATE`** | Specialized conversions: COERCION for big numbers; UNIX_DATE returns days since Jan 1, 1970 (useful for comparing dates across time zones) | Days-since-epoch is just a serial date — same trick Excel uses (days since 1/1/1900) for date math. |
| **`ROUND`** (SQL — the module 2 glossary term) | Returns a number rounded to a set number of decimal places: `ROUND(AVG(...), 2)` | Rounding to cents. Every payroll calc ends in `ROUND(x, 2)`. |
| **`AVG` / `COUNT(*)` / `GROUP BY` / `LIMIT`** | Average of a column; count of rows; collapse rows into groups; cap results at N rows | AVG = average hourly rate; COUNT(*) = headcount; GROUP BY department = subtotals; LIMIT 10 = "top ten." |
| **Advanced spreadsheet tips** | A resource list: keyboard shortcuts (Sheets and Excel), full function lists, "23 must-know formulas," essential Excel skills for analysis (pivot tables, conditional formatting) | Bookmark, don't memorize. Ctrl+Shift+L, Ctrl+;, Alt+= — you already know half of these from 20 years of month-end. |

### Convert in spreadsheets — the four scenarios (from "Convert data in spreadsheets")
1. **String → date** — Excel functions or text-to-date without a formula; Sheets: change date format
2. **String → number** — so values add up and work in formulas without errors
3. **Combining columns** — merge text from two or more cells without losing data (Excel: two methods; Sheets: split or combine)
4. **Number → percentage** — Excel percentage format; Sheets `TO_PERCENT`
- **Pro tip:** many columns, many formats — but each **whole column** should be one format. Consistency is key.
- Same functions work again and again — bookmark the help pages.

### From one type to another — the demo (from "Step-by-step: From one type to another")
1. **Check and change data type:** select Budget ($) and Box Office Revenue ($) → click `$` currency shortcut → formatted as money
2. **CONVERT units:** `=CONVERT(B2, "F", "C")` in F2 → drag fill handle to F193. Practice: `=CONVERT(D2, "mph", "m/s")` (check: 8.5248)
3. **Lock data:** if a reference value changes, the calculated value changes too. Copy the formula column → **Paste special → Paste values only** → the cell now holds a value, not a function, and won't move.

### Strings in spreadsheets — the Citi Bike demo (from "Step-by-step: Strings in spreadsheets")
Start-time strings look like `2016-01-01 00:00:01` (19 chars; date is 10 chars, space at position 11, time is 8 chars).
| Goal | Formula | Result |
|---|---|---|
| How long is the string? | `=LEN(C2)` | 19 |
| Where's the space? | `=FIND(" ", C3)` | 11 |
| Pull the time | `=RIGHT(C2, 8)` | `00:00:01` |
| Pull the date | `=LEFT(D2, 10)` | `2016-01-01` |
- Double-click the fill handle to fill the column; add a header (Time / Date)
- Insert a column left first if you need a place for the new substring (then watch — your source column letter shifts)
- `FIND` is case sensitive — enter the substring exactly

### CONCAT family in SQL (from "Manipulate strings with SQL")
| Function / operator | Use | Example | Result |
|---|---|---|---|
| `CONCAT` | Join strings into a new string | `CONCAT('Google', '.com')` | `Google.com` |
| `CONCAT_WS` | Join with a separator between each piece | `CONCAT_WS('.', 'www', 'google', 'com')` | `www.google.com` |
| `\|\|` | Join with the operator (BigQuery) | `'Google' \|\| '.com'` | `Google.com` |
- Microsoft SQL Server: `SELECT 'Google' + '.com'` — `||` doesn't work there. Always check the dialect.
- Full-name pattern: `SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM customers;`

### Merge text strings to gain insights — the full query (from the step-by-step)
```sql
SELECT
  usertype,
  CONCAT(start_station_name, " to ", end_station_name) AS route,
  COUNT(*) AS num_trips,
  ROUND(AVG(CAST(tripduration AS INT64) / 60), 2) AS duration
FROM
  `bigquery-public-data.new_york.citibike_trips`
GROUP BY
  start_station_name, end_station_name, usertype
ORDER BY
  num_trips DESC
LIMIT 10
```
- `CONCAT` builds a readable **route** column ("A to B") from two station columns
- `COUNT(*)` counts rows = trips; `CAST(tripduration AS INT64)` makes seconds a number (BigQuery uses 64-bit → `INT64`), `/ 60` = minutes, `AVG` averages per route, `ROUND(..., 2)` = 2 decimals, `AS duration` names it
- `GROUP BY` every non-aggregated column; `ORDER BY num_trips DESC LIMIT 10` = the top-ten routes
- Gotcha: BigQuery has both `new_york` and `new_york_citibike` datasets, each with a `citibike_trips` table — they're **not identical**; the video uses `new_york` (scroll to it; it doesn't appear in search)
- Payroll version: `CONCAT(agency, " / ", title) AS role, COUNT(*) AS headcount, ROUND(AVG(base_salary), 2) AS avg_salary ... GROUP BY agency, title ORDER BY headcount DESC LIMIT 10`

### Import & combine — spreadsheets vs. SQL (from "Import and combine data")
| Task | Spreadsheets | SQL |
|---|---|---|
| Import data | `=IMPORTRANGE(spreadsheet_url, range_string)` — include the tab name if the file has multiple tabs | No import function — use `INSERT INTO dest SELECT ... FROM source WHERE ...` |
| Combine strings | `=CONCATENATE(item1, " ", item2)` | `SELECT CONCAT(field1, " ", field2) AS alias FROM table` |
- Reading's SQL example: `INSERT INTO customer_promotion SELECT * FROM customers WHERE total_sales = 0 AND postal_code = '12345'`
- Always alias a CONCAT column with `AS` — otherwise SQL has no header name for it

### CAST — what converts to what (from "Transform data with SQL")
| Starting type | CAST can convert to |
|---|---|
| **Numeric** | Integer, Numeric, Big number, Floating integer, String |
| **String** | Boolean, Integer, Numeric, Big number, Floating integer, String, Bytes, Date, Datetime, Time, Timestamp |
| **Date** | String, Date, Datetime, Timestamp |
```sql
SELECT CAST(MyCount AS STRING) FROM MyTable       -- number → string
SELECT CAST(MyVarcharCol AS INT) FROM MyTable     -- string → integer (whole number)
SELECT CAST(MyDate AS STRING) FROM MyTable        -- date → string
SELECT CAST(MyDate AS DATETIME) FROM MyTable      -- date → datetime (YYYY-MM-DD hh:mm:ss)
SELECT SAFE_CAST(MyDate AS STRING) FROM MyTable   -- same, but NULL instead of an error on failure
```
- The reading's metaphor: converting data yourself is like being a driver who can change a flat tire — you don't wait for someone else.
- Other dialects: SQL Server has `CAST` and `CONVERT`; MySQL has its own CAST functions — same idea, check syntax.

## 🗣️ Teach it to a friend

Clean data can still be the wrong *type* — a number stored as text won't add up, a date stored
as text won't sort, and a first name and last name in two columns won't print on a mailing
label. So before analyzing, you convert and combine. In a spreadsheet you use the format menu
(currency, percent, date), `CONVERT` for units, and string functions: `LEN` tells you how long a
string is, `FIND` tells you where a character sits, and `LEFT`/`RIGHT` pull pieces off either end
— that's how you split `2016-01-01 00:00:01` into a date and a time. To glue strings together
you use `CONCATENATE` in a spreadsheet or `CONCAT` in SQL (with `" "` for a space, and `AS` to
name the new column). To bring data in from elsewhere: `IMPORTRANGE` in Sheets, or
`INSERT INTO ... SELECT` in SQL. And to change types in SQL, `CAST(column AS TYPE)` — or
`SAFE_CAST` if you'd rather get a NULL than have the whole query fail. One last habit: after
converting with a formula, paste as values so the result stops moving.

## 🃏 Flashcards

**Q:** Name four common conversions you make in a spreadsheet before analysis.
**A:** String → date, string → number, combining columns, number → percentage. (Best practice: keep every column in one consistent format.)

**Q:** What does `=CONVERT(B2, "F", "C")` do?
**A:** Converts the value in B2 from Fahrenheit to Celsius — CONVERT changes units of measurement (also e.g. `"mph"` → `"m/s"`).

**Q:** Why "lock" data after converting it with a function, and how?
**A:** A formula's result changes if its reference cells change. Copy → Paste special → Paste values only replaces the function with a fixed value.

**Q:** What do LEN, FIND, LEFT, and RIGHT each return?
**A:** LEN = number of characters in a string; FIND = position of a substring (case sensitive); LEFT = the first N characters; RIGHT = the last N characters.

**Q:** For the string `2016-01-01 00:00:01`, what do `LEN`, `FIND(" ", ...)`, `LEFT(...,10)`, and `RIGHT(...,8)` return?
**A:** 19; 11; `2016-01-01`; `00:00:01`.

**Q:** What is concatenation, and how do you add a space between the joined values?
**A:** Joining two or more text strings into one. Add `" "` as an item: `=CONCATENATE(A2, " ", B2)` or `CONCAT(first_name, ' ', last_name)`.

**Q:** Why alias a CONCAT column with `AS`?
**A:** SQL uses field names as headers, but a CONCAT result has no field name — `AS full_name` gives it a readable header.

**Q:** CONCAT vs. CONCAT_WS vs. `||`?
**A:** CONCAT joins strings; CONCAT_WS ("with separator") inserts a separator between each piece; `||` is BigQuery's concatenation operator. In Microsoft SQL Server use `+` instead of `||`.

**Q:** How do you import a range from another Google Sheet?
**A:** `=IMPORTRANGE(spreadsheet_url, range_string)` — e.g. `"Sheet1!A2:B6"`, including the tab name if there are multiple tabs.

**Q:** SQL has no import function. How do you move rows from one table to another?
**A:** `INSERT INTO destination_table SELECT columns FROM source_table WHERE condition`.

**Q:** What is the syntax of CAST, and give one example.
**A:** `CAST(expression AS typename)` — e.g., `SELECT CAST(MyVarcharCol AS INT) FROM MyTable` turns a string into an integer.

**Q:** What's the difference between CAST and SAFE_CAST?
**A:** Same syntax; CAST returns an error when a conversion fails, SAFE_CAST returns NULL instead.

**Q:** What does UNIX_DATE return?
**A:** The number of days since January 1, 1970 — used to compare and work with dates across time zones.

**Q:** In `ROUND(AVG(CAST(tripduration AS INT64)/60), 2)`, what does each part do?
**A:** CAST makes tripduration an integer (64-bit in BigQuery); `/60` converts seconds to minutes; AVG averages per group; ROUND keeps 2 decimal places.

**Q:** What does ROUND do in SQL (module 2 glossary)?
**A:** Returns a number rounded to a certain number of decimal places.

**Q:** In the Citi Bike CONCAT query, why is the `new_york` vs. `new_york_citibike` dataset distinction important?
**A:** Both have a `citibike_trips` table but they're not identical; the lesson uses `new_york`, which you must scroll to (it doesn't appear in search).

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** the NYC payroll CSV lands with pay columns as text and agency/title strings that need cleanup. Plan: `SAFE_CAST(regular_gross_paid AS NUMERIC)` in the load query (so bad rows become NULLs I can list, not a failed query), `CONCAT(agency_name, " / ", title_description) AS role` for a readable grouping column, and a top-ten roles query modeled exactly on the Citi Bike one — `COUNT(*)`, `ROUND(AVG(...), 2)`, `GROUP BY`, `ORDER BY ... DESC LIMIT 10`.
- **flask-analytics-app:** add a "data types" check to the upload step: run LEN/pattern checks on ID columns (SSN-style leading-zero loss), try a numeric cast on amount columns, and surface a "N rows couldn't convert" message — the SAFE_CAST idea in Python. Also a saved query showing string concatenation building a display name.
- **Spreadsheet habits I'll keep:** LEFT/RIGHT/FIND to split date-time strings, `=SORT(FILTER())` from module 1 for live views, and **Paste values only** before any file gets called "final" — a rule I already follow for accruals; now I know the course name for it.
- **Job hunt / interview line:** *"Type conversion and string cleanup are most of what payroll data prep is — amounts that import as text, employee names in three different formats, IDs that lose leading zeros. I've fixed those in Excel for 20 years with VALUE, LEN, LEFT/RIGHT, and CONCATENATE; in Course 5 I moved the same fixes into BigQuery with CAST, SAFE_CAST, and CONCAT, and I use them in my NYC payroll project."*
- **Bookmarks (from the advanced tips reading):** Sheets keyboard shortcuts + function list, Excel shortcuts + function list, "Essential Excel Skills for Analyzing Data" (pivot tables, conditional formatting). Skim once, save, don't memorize.
