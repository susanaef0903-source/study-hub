# Google Data Analytics — Course 5, Module 3: Aggregate Data for Analysis (JOINs, Aliases, Subqueries, VLOOKUP)

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 3 readings (Use JOINs effectively, Secret identities: aliases, SQL functions and subqueries, VLOOKUP core concepts, three step-by-step guides) + module 3 glossary + Course 5 glossary

> *(this is the SQL module that shows up in every data analyst interview — JOINs are THE question)*

## 🎯 What this module is about (one sentence)

Real answers almost never live in one table (or one spreadsheet), so this module is about
combining data — JOINs and subqueries in SQL, VLOOKUP in spreadsheets — and about
aggregating what you combined (COUNT, AVG, GROUP BY, HAVING, CASE) into a summary a
stakeholder can use.

**Sue's note:** you have been joining tables for 20 years without calling it that. Every time you
matched a timesheet export to the employee master by employee ID, or VLOOKUP'd a pay rate
into a hours file, that was a JOIN. This module just gives you the SQL words for it — and those
words are exactly what interviewers ask about.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **JOIN** | Combine rows from two or more tables based on a related column (a primary/foreign key). Lives in the FROM clause: `FROM a JOIN b ON a.key = b.key` | Matching the timesheet file to the employee master on employee ID so hours and pay rate end up on the same row. |
| **Primary / foreign key** | The ID that uniquely identifies a row in one table (primary) and shows up in another table to point back to it (foreign) | Employee ID is the primary key on the master file and the foreign key on every timesheet, deduction, and W-2 record. |
| **INNER JOIN** (default; plain `JOIN`) | Return only rows where the key exists in **both** tables | Only employees who have hours this period. Someone on the master with no timesheet drops out — and someone with hours but no master record drops out too. |
| **LEFT JOIN** (LEFT OUTER JOIN) | All rows from the left (first) table, plus matches from the right; no match → NULL | **"Keep every employee even if no hours."** The register shows all 200 people; the ones without a timesheet show blank hours — which is exactly the exception list you want. |
| **RIGHT JOIN** | All rows from the right (second) table, plus matches from the left. Rarely used — most people flip the table order and use LEFT JOIN | Same as above but starting from the timesheet file: every timesheet, even ones whose employee ID isn't on the master (a terminated employee still clocking in? a typo?). |
| **FULL OUTER JOIN** (FULL JOIN) | All rows from **both** tables, NULLs wherever there's no match. Can be a big pull | The full reconciliation view: employees with no hours AND hours with no employee, on one report. |
| **ON** | The matching rule for a JOIN | "Match on employee ID," "match on cost center code." |
| **Aliasing** (`AS`) | Temporary nickname for a table or column so queries are shorter and readable. `FROM long_table_name AS t` or `SELECT col AS friendly_name`. AS is optional in most databases but makes it clearer | Calling `payroll_2026_q3_final_v2` just `pay` in your formulas — or renaming the column "REG_HRS_QTY" to "Regular Hours" on the report. |
| **Subquery** (inner / nested query) | A SELECT inside another query, always in parentheses. Can sit in SELECT, FROM, or WHERE | A helper worksheet: first total hours per department on a side tab, then pull that total into the main report. |
| **Aggregation** | Gathering many separate pieces into one summarized whole (SUM, COUNT, AVG, MIN, MAX) | Going from 4,000 timesheet lines to "total OT hours by department." |
| **GROUP BY** | Group rows with the same value into summary rows so aggregate functions run per group | The subtotal lines on a payroll register — one row per department instead of one per check. |
| **HAVING** | Filter *after* grouping (WHERE filters individual rows *before* grouping) | "Show only departments whose total OT is over 100 hours" — a filter on a subtotal, not on a line. |
| **CASE ... WHEN ... THEN ... ELSE ... END** | If/else logic inside a query — creates categories/labels | Bucketing employees: hours < 30 → "Part-time," 30–40 → "Full-time," > 40 → "Overtime." |
| **COUNT / COUNT DISTINCT** | COUNT = number of rows; COUNT DISTINCT = number of unique values | COUNT of checks vs. COUNT DISTINCT of employee IDs — the difference is who got two checks. |
| **CAST** | Convert a column's data type (e.g., number → string) so two keys can match | Employee ID stored as text in one system and as a number in the other — nothing matches until you convert one. |
| **LIMIT** | Cap the number of rows a query returns | "Show me the top 10" — sanity-check a query before pulling 100k rows. |
| **VLOOKUP** | Spreadsheet function: search a value in the first column of a range, return the value from another column in that row. `VLOOKUP(search_key, range, index, is_sorted)` | What you've done in Excel for years: look up the pay rate for employee 4471 from the master tab. |
| **MATCH** | Spreadsheet function returning the *position* of a lookup value in a range | The other half of INDEX/MATCH — the more flexible cousin of VLOOKUP when the lookup column isn't on the left. |
| **VALUE** | Spreadsheet function converting a text string that looks like a number into an actual number | Fixing an export where the hours column came in as text and SUM returns 0. |
| **Absolute reference** (`$A$2:$D$500`) | A locked cell reference that doesn't shift when you copy the formula | The `$` you put on the lookup table range so the VLOOKUP doesn't drift as you fill down. |

### JOIN cheat sheet (exam + interview favorite!)

**Setup — two tiny tables:**

`employees` (the master)

| emp_id | name  | dept    |
|---|---|---|
| 1 | Ana   | Finance |
| 2 | Ben   | HR      |
| 3 | Carla | Finance |

`timesheets` (this week's hours)

| emp_id | hours |
|---|---|
| 1 | 40 |
| 3 | 45 |
| 9 | 20 |  ← emp_id 9 is not on the master (typo? terminated employee?)

Query skeleton — only the JOIN word changes:

```sql
SELECT
  e.emp_id,
  e.name,
  t.hours
FROM employees AS e
<JOIN TYPE> timesheets AS t
  ON e.emp_id = t.emp_id
```

| JOIN type | What comes back | Rows in the example | Payroll meaning |
|---|---|---|---|
| **INNER JOIN** | Only IDs in both tables | Ana 40, Carla 45 | Employees who worked *and* are on the master |
| **LEFT JOIN** | Every employee; hours or NULL | Ana 40, **Ben NULL**, Carla 45 | Full roster — Ben has no timesheet (chase him) |
| **RIGHT JOIN** | Every timesheet; name or NULL | Ana 40, Carla 45, **NULL 20 (id 9)** | Every timesheet — id 9 has no master record (investigate) |
| **FULL OUTER JOIN** | Everything from both, NULLs where unmatched | Ana 40, Ben NULL, Carla 45, NULL 20 | The full reconciliation: both exception types on one report |

**Rules of thumb**
- `JOIN` alone means `INNER JOIN` — the default and the most common.
- LEFT vs RIGHT is just table order; **most analysts always use LEFT and put the "keep all of these" table first.**
- The join key (emp_id) doesn't have to appear in the SELECT — it's just the matching rule.
- NULLs in the result of a LEFT/RIGHT/FULL join are your exception list — that's often the whole point of the query.
- Key data types must match. If one table stores the ID as a string and the other as a number, `CAST(start_station_id AS STRING)` first (this is exactly what bit the course's Citi Bike example).

### Aliases: the AS habit
```sql
SELECT
  employees.name AS employee_name,
  departments.name AS department_name
FROM `your-project.employee_data.employees` AS employees
INNER JOIN `your-project.employee_data.departments` AS departments
  ON employees.department_id = departments.department_id
```
- Table alias: `FROM table AS alias` — column alias: `SELECT column AS alias`.
- If a database refuses `AS`, just leave a space: `FROM table alias`. Both work; `AS` is more readable.
- Table aliases pay off the moment two tables both have a column called `name` — `employees.name` vs `departments.name` removes the ambiguity.

### Subqueries: three places they live (worked example)

A subquery is a SELECT in parentheses inside another query. The three spots:

**1. In SELECT — add a computed column (compare each row to the overall average):**
```sql
SELECT
  station_id,
  num_bikes_available,
  (SELECT AVG(num_bikes_available)
   FROM `bigquery-public-data.new_york.citibike_stations`) AS avg_num_bikes_available
FROM `bigquery-public-data.new_york.citibike_stations`;
```
*Payroll version:* each employee's hours next to the department average — same query shape.

**2. In FROM — build a helper table, then join to it:**
```sql
SELECT
  station_id,
  name,
  number_of_rides AS number_of_rides_starting_at_station
FROM (
  SELECT
    CAST(start_station_id AS STRING) AS start_station_id_str,
    COUNT(*) AS number_of_rides
  FROM `bigquery-public-data.new_york.citibike_trips`
  GROUP BY CAST(start_station_id AS STRING)
) AS station_num_trips
INNER JOIN `bigquery-public-data.new_york.citibike_stations`
  ON station_id = start_station_id_str
ORDER BY number_of_rides DESC;
```
*Payroll version:* subquery = "count of checks per employee ID" (a side tab); outer query joins that to the master to get names. The subquery table gets an alias (`station_num_trips`) just like a real table.

**3. In WHERE — filter by a list another query produces:**
```sql
SELECT station_id, name
FROM `bigquery-public-data.new_york.citibike_stations`
WHERE station_id IN (
  SELECT CAST(start_station_id AS STRING)
  FROM `bigquery-public-data.new_york.citibike_trips`
  WHERE usertype = 'Subscriber'
);
```
*Payroll version:* "show me employees whose ID appears in the garnishment file" — `WHERE emp_id IN (SELECT emp_id FROM garnishments)`.

**Subquery rules (from the reading)**
- Must be in parentheses.
- Can return one or more columns.
- If it returns **more than one row**, use it only with multi-value operators like `IN` (not `=`).
- Can't be nested inside a `SET` command (the part of UPDATE that assigns values).
- Why bother: one trip to the database instead of several, and the logic stays in one readable place.

### The big one: subqueries + JOIN + GROUP BY + CASE + HAVING together
The "Use subqueries to aggregate data" step-by-step builds this — worth reading slowly once, because it's basically an interview take-home in miniature:
```sql
SELECT
  Warehouse.warehouse_id,
  CONCAT(Warehouse.state, ': ', Warehouse.warehouse_alias) AS warehouse_name,
  COUNT(Orders.order_id) AS number_of_orders,
  (SELECT COUNT(*) FROM `your-project.warehouse_orders.orders`) AS total_orders,
  CASE
    WHEN COUNT(Orders.order_id) / (SELECT COUNT(*) FROM `your-project.warehouse_orders.orders`) <= 0.20
      THEN 'Fulfilled 0-20% of Orders'
    WHEN COUNT(Orders.order_id) / (SELECT COUNT(*) FROM `your-project.warehouse_orders.orders`) > 0.20
     AND COUNT(Orders.order_id) / (SELECT COUNT(*) FROM `your-project.warehouse_orders.orders`) <= 0.60
      THEN 'Fulfilled 21-60% of Orders'
    ELSE 'Fulfilled more than 60% of Orders'
  END AS fulfillment_summary
FROM `your-project.warehouse_orders.warehouse` AS Warehouse
LEFT JOIN `your-project.warehouse_orders.orders` AS Orders
  ON Orders.warehouse_id = Warehouse.warehouse_id
GROUP BY Warehouse.warehouse_id, warehouse_name
HAVING COUNT(Orders.order_id) > 0
```
Read it as a payroll report: LEFT JOIN keeps every warehouse (every department); COUNT per group is the subtotal; the subquery is the grand total; CASE labels each department's share; HAVING drops departments with zero activity. Swap warehouses for departments and orders for checks and you've written a payroll-volume report.

### VLOOKUP core concepts (the spreadsheet JOIN)
`=VLOOKUP(search_key, range, index, is_sorted)`
- **search_key** — what to look for (a value or a cell reference).
- **range** — the block to search; the search happens in the **first column** of the range, so the key column must be on the **left** of what you want back (rearrange columns if not, or use INDEX/MATCH).
- **index** — which column of the range to return, counting from 1. Range `B2:D10`, want column D → index 3. Out of bounds → `#VALUE!`.
- **is_sorted** — `FALSE` = exact match (**use this**); `TRUE` (the default if omitted!) = approximate match, requires ascending sort. Set it explicitly every time.
- Returns only the **first** match. Duplicate keys → silently returns the first one (the same "which of the two checks?" trap as duplicates in a JOIN).
- `#N/A` = no match found — the VLOOKUP version of the NULL you get from a LEFT JOIN. Same exception meaning.
- Two classic uses: **populating** a sheet (pull product info by ID) and **merging** two sheets (attendance into grades). Both are LEFT JOINs.

### Glossary terms not covered above (module 3 + Course 5 glossary)

| Term | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data aggregation** | Gathering data from multiple sources and combining it into a single, summarized collection | Pulling time, benefits, and tax files together into one payroll summary. |
| **OUTER JOIN** (glossary wording) | Combines RIGHT and LEFT JOIN to return all matching records in both tables — i.e., FULL OUTER JOIN | The both-sides reconciliation view. |
| **ORDER BY** | Sort the results of a query | Register sorted by department, then last name. |
| **ROUND** | SQL function that rounds to a set number of decimal places | Rounding computed pay to cents — `ROUND(hours * rate, 2)`. |

## 🗣️ Teach it to a friend

Most questions need two tables, so SQL has JOIN: you name a matching column (like
employee ID) and it lines the rows up. INNER JOIN keeps only rows found in both tables;
LEFT JOIN keeps everything from the first table and fills blanks (NULL) where the second has
no match — that's how you get "every employee, even the ones with no hours." RIGHT JOIN
is the mirror image and almost nobody uses it; FULL OUTER JOIN keeps everything from both
sides. Aliases (`AS`) are nicknames so you don't retype long table names. A subquery is a
query inside a query — in SELECT to add a comparison column, in FROM to build a helper table
you then join to, or in WHERE to filter by a list. And VLOOKUP is the spreadsheet version of
a LEFT JOIN: find this key in the first column of that range, give me column N, exact match
(FALSE), and #N/A when it's not there.

## 🃏 Flashcards

**Q:** What are the four types of JOIN?
**A:** INNER, LEFT, RIGHT, FULL OUTER.

**Q:** Which JOIN is the default when you write just `JOIN`?
**A:** INNER JOIN — returns only records with matching values in both tables.

**Q:** LEFT JOIN returns what?
**A:** All records from the left (first) table and only the matching records from the right table; unmatched rows get NULL for the right-table columns.

**Q:** Why is RIGHT JOIN rarely used?
**A:** Because you can get the same result by swapping the table order and using LEFT JOIN — most people standardize on LEFT.

**Q:** What does FULL OUTER JOIN return, and what's the caution?
**A:** All records from both tables (NULL where there's no match). It can be a very large data pull.

**Q:** Where does the JOIN clause live in a query, and what does ON do?
**A:** JOIN is part of the FROM clause; ON specifies how the tables are matched (`ON a.key = b.key`).

**Q:** What is aliasing and what keyword does it use?
**A:** Temporarily naming a table or column to make queries easier to read and write; uses `AS` (which can be omitted in most databases).

**Q:** What is a subquery, and where can it appear?
**A:** A query nested inside a larger query, enclosed in parentheses; usually in the SELECT, FROM, or WHERE clause.

**Q:** A subquery returns multiple rows. What operator must you use it with?
**A:** A multiple-value operator such as IN — not `=`.

**Q:** Name one place a subquery cannot be nested.
**A:** Inside a SET command (used with UPDATE).

**Q:** WHERE vs HAVING?
**A:** WHERE filters individual rows before grouping; HAVING filters groups after GROUP BY (e.g., `HAVING COUNT(order_id) > 0`).

**Q:** What does CASE do?
**A:** Adds if/else conditional logic to a query — `CASE WHEN condition THEN label ... ELSE default END AS new_column`.

**Q:** VLOOKUP syntax and what each part means?
**A:** `VLOOKUP(search_key, range, index, is_sorted)` — value to find; block to search (first column is searched); column number to return (1-based); FALSE = exact match, TRUE = approximate.

**Q:** In VLOOKUP, where must the search column be relative to the return column?
**A:** To the left — the range's first column is searched, and the return column must be inside the range.

**Q:** VLOOKUP returns #N/A. What does that mean? What about #VALUE!?
**A:** #N/A = no match found. #VALUE! = the index is outside 1..number of columns in the range.

**Q:** If you omit is_sorted in VLOOKUP, what happens?
**A:** It defaults to TRUE (approximate match) — so always type FALSE for exact matches.

**Q:** COUNT vs COUNT DISTINCT?
**A:** COUNT counts rows; COUNT DISTINCT counts unique values in a range.

**Q:** Two tables' join keys are different data types (INT64 vs STRING). What do you do?
**A:** Convert one with CAST — e.g., `CAST(start_station_id AS STRING)` — so the ON condition can match.

**Q:** What is an absolute reference in a spreadsheet?
**A:** A cell reference locked with `$` (e.g., `$A$2:$D$500`) so rows/columns don't shift when the formula is copied.

## 💡 How I'll actually use this

- **flask-analytics-app (SQL query page):** the app already runs SQLite queries from a page — add a second table (a small `departments` or `categories` lookup) and ship three saved example queries: an INNER JOIN, a LEFT JOIN that surfaces the NULL rows, and a FROM-subquery that aggregates then joins. Label them so a visitor (or hiring manager) sees I know the difference, not just that I can SELECT *.
- **nyc-payroll-explorer:** the NYC payroll dataset has agency name repeated on every row — build an `agencies` lookup and JOIN to it, then a subquery-in-SELECT that shows each employee's base salary next to their agency average. That's the "compare each row to the group average" pattern from this module, on real data.
- **Spreadsheet muscle memory → SQL:** every VLOOKUP I've written is a LEFT JOIN. Every "#N/A means someone's missing from the master" is a NULL from a LEFT JOIN. When an interviewer asks about joins, I explain it with the timesheet-to-master example first, then the SQL — that's a story only someone who has actually run payroll can tell.
- **Job hunt (SQL joins are THE interview topic):** be ready to (1) draw the four Venn diagrams, (2) explain INNER vs LEFT with the "keep every employee even if no hours" line, (3) say why I default to LEFT over RIGHT, (4) explain WHERE vs HAVING, and (5) write a subquery from memory. Practice the warehouse query above until I can rebuild it without looking — it exercises every one of those.
- **Interview line:** "I've been doing joins for twenty years in Excel — VLOOKUP from the timesheet file to the employee master, chasing every #N/A. In SQL that's a LEFT JOIN with a WHERE ... IS NULL, and the exception list is the same list I used to build by hand."
