# SQL Reference Guide — keep this open while writing queries

**Platform:** LaGuardia CC "Data, Databases & SQL" (PostgreSQL/pgAdmin) + Google Data Analytics | **Compiled:** Aug 2026 | **Source:** the 8 course cheat-sheet/lesson PDFs from the SQL Desktop folder + the Google course SQL cheat sheet

## 🎯 What this guide is (one sentence)

Every syntax pattern from the course PDFs, organized by the *task* I'm trying to do —
so when I'm mid-query in pgAdmin or my flask-analytics-app I can jump straight to the
section I need instead of digging through eight PDFs.

**Course dialect:** PostgreSQL (dvdrental database, students/marks tables, weblinks practice table).
Nearly everything here is standard SQL; Postgres-only bits are flagged.

## 🧭 Query anatomy (the order you WRITE vs the order SQL RUNS)

```sql
SELECT   column, SUM(other) AS total   -- 5. pick/compute columns
FROM     table_a                       -- 1. get the table
JOIN     table_b ON a.id = b.a_id      -- 2. combine tables
WHERE    condition                     -- 3. filter ROWS (before grouping)
GROUP BY column                        -- 4. collapse into groups
HAVING   SUM(other) > 100              -- 6. filter GROUPS (after grouping)
ORDER BY total DESC                    -- 7. sort
LIMIT    10;                           -- 8. cap the output
```

That run-order explains the two rules that trip everyone up:
- **WHERE can't see aggregates** (they don't exist yet) → filter aggregates with HAVING.
- **ORDER BY can see aliases** (it runs last) — and in Postgres, so can GROUP BY.

---

## 1️⃣ Selecting (SELECT, DISTINCT, aliases)

```sql
SELECT * FROM film;                          -- all columns (exploring only)
SELECT title, rental_rate FROM film;         -- name your columns (better)
SELECT DISTINCT rating FROM film;            -- unique values only
SELECT name AS city_name FROM city;          -- rename a column in the output
SELECT c.name, co.name
FROM city AS c JOIN country AS co ON ...;    -- table aliases keep joins readable
```

- `SELECT DISTINCT` = "give me the list of different values" — great for a quick data-quality scan.
- Always alias computed columns (`SUM(amount) AS total_paid`) or you get useless names.
- Be specific with columns instead of `SELECT *` — faster, clearer, and the join sections below get much easier to read.

## 2️⃣ Filtering rows (WHERE)

```sql
SELECT name FROM city WHERE rating > 3;
SELECT name FROM city WHERE name != 'Berlin' AND name != 'Madrid';
SELECT name FROM city WHERE population BETWEEN 500000 AND 5000000;  -- inclusive!
SELECT name FROM city WHERE country_id IN (1, 4, 7, 8);
SELECT name FROM city WHERE name LIKE 'P%' OR name LIKE '%s';
SELECT name FROM city WHERE name LIKE '_ublin';                     -- _ = exactly 1 char
SELECT name FROM city WHERE rating IS NOT NULL;
```

**Operators:** `=` `!=` (or `<>`) `<` `>` `<=` `>=` `BETWEEN low AND high` `IN (list)` `LIKE pattern` `IS NULL / IS NOT NULL`

**Combining:** `AND` (all must be true), `OR` (at least one true), `NOT` (exclude). Use
parentheses to control evaluation: `WHERE (a OR b) AND c`.

**String rules (the #1 error source):**
- **Single quotes for text**: `WHERE title = 'Inception'`. Numbers and booleans: no quotes. Dates usually quoted: `'2005-05-29'`.
- Apostrophe inside a string → double it: `WHERE last_name = 'O''Brien'`.
- `NULL` is never `= NULL` — always `IS NULL` / `IS NOT NULL`.
- BigQuery compares strings **case-sensitively** ('us' ≠ 'US'); PostgreSQL/MySQL comparisons with `=` on `LIKE` are case-sensitive in Postgres too — `ILIKE` is the Postgres case-insensitive version.

## 3️⃣ Sorting & limiting (ORDER BY, LIMIT)

```sql
SELECT name, price FROM products ORDER BY price DESC;   -- ASC is the default
SELECT * FROM products ORDER BY category ASC, price DESC;
SELECT * FROM products LIMIT 10;                         -- first 10 rows
SELECT * FROM products ORDER BY id LIMIT 10 OFFSET 20;   -- rows 21-30 (pagination)
```

- Top-5 pattern: `ORDER BY total DESC LIMIT 5`.
- `LIMIT` without `ORDER BY` = arbitrary rows. Sort first if "top" or "first" matters.

## 4️⃣ Grouping & aggregating (COUNT, SUM, AVG, MIN, MAX, GROUP BY, HAVING)

**The five aggregate functions:** `COUNT()` (how many), `SUM()` (total), `AVG()` (average), `MIN()`/`MAX()` (smallest/largest).

```sql
SELECT COUNT(*) FROM city;                        -- all rows, NULLs included
SELECT COUNT(rating) FROM city;                   -- non-NULL ratings only
SELECT COUNT(DISTINCT country_id) FROM city;      -- how many different countries
SELECT MIN(population), MAX(population) FROM country;
SELECT ROUND(AVG(amount), 2) FROM payment;        -- ROUND(number, decimals)

-- Summary by category = GROUP BY:
SELECT country_id, SUM(population) AS total_pop
FROM city
GROUP BY country_id;

-- Filter the groups themselves = HAVING:
SELECT country_id, AVG(rating) AS avg_rating
FROM city
GROUP BY country_id
HAVING AVG(rating) > 3.0;
```

- **Every non-aggregated column in SELECT must appear in GROUP BY.**
- `COUNT(*)` counts rows; `COUNT(column)` skips NULLs — aggregates ignore NULLs except `COUNT(*)`.
- WHERE filters rows *before* grouping; HAVING filters *after*. You can use both in one query.

## 5️⃣ Joining tables

All joins follow one shape:

```sql
SELECT city.name, country.name
FROM city
INNER JOIN country ON city.country_id = country.id;
```

| Join | Returns | When I'd use it |
|---|---|---|
| **INNER JOIN** (or just `JOIN`) | Only rows that match in **both** tables | Employees that have timesheets — drop everyone else |
| **LEFT JOIN** | **All** left rows + matches from right (NULL if none) | All employees, with timesheets *if they exist* — find who's missing one! |
| **RIGHT JOIN** | All right rows + matches from left | Same idea, flipped (rarer — most people re-order and use LEFT) |
| **FULL OUTER JOIN** | Everything from both sides, NULLs where no match | Reconciliation: what's in either system, matched or not |
| **CROSS JOIN** | Every combination (Cartesian product) | Rare on purpose; usually an accident (see mistakes list) |
| **Self join** | Table joined to itself with two aliases (`FROM emp a JOIN emp b ON ...`) | Employee ↔ manager relationships |

- The unmatched-side columns come back as **NULL** — so "find left rows with no match" is `LEFT JOIN ... WHERE right.id IS NULL`.
- Alias your tables (`FROM film f JOIN inventory i ON f.film_id = i.film_id`) — required reading-speed for multi-joins.
- Filter early: a `WHERE` alongside your JOIN shrinks the result set and speeds things up.

## 6️⃣ Stacking result sets (UNION, INTERSECT, EXCEPT)

Joins add *columns*; set operations stack *rows*. Both queries must return the same number of columns with compatible types.

```sql
SELECT name FROM cycling WHERE country = 'DE'
UNION            -- stack + remove duplicates  (UNION ALL keeps duplicates)
SELECT name FROM skating WHERE country = 'DE';
```

- `INTERSECT` → only rows appearing in **both** results.
- `EXCEPT` (a.k.a. `MINUS` in Oracle) → rows in the first result but **not** the second. Perfect for "who's in system A but missing from system B".

## 7️⃣ Subqueries (a query inside a query)

A subquery can live in SELECT, FROM, or WHERE. Must be wrapped in parentheses; goes on the right side of the comparison; **no ORDER BY inside a subquery** (sort in the outer query instead).

```sql
-- Single value: compare against a number you don't know yet
SELECT film_id, title, rental_rate
FROM film
WHERE rental_rate > (SELECT AVG(rental_rate) FROM film);

-- Multiple values: use IN
SELECT film_id, title
FROM film
WHERE film_id IN (SELECT i.film_id
                  FROM rental r
                  INNER JOIN inventory i ON r.inventory_id = i.inventory_id
                  WHERE r.rental_date BETWEEN '2005-05-29' AND '2005-05-30');

-- Correlated: subquery references the outer row (runs per-row, can't run alone)
SELECT * FROM city main_city
WHERE population > (SELECT AVG(population) FROM city avg_city
                    WHERE avg_city.country_id = main_city.country_id);

-- EXISTS: "at least one match exists"
SELECT name FROM country
WHERE EXISTS (SELECT * FROM city WHERE country_id = country.id);
```

**WITH (CTE)** — a named subquery that keeps big queries readable:

```sql
WITH high_rentals AS (
  SELECT * FROM film WHERE rental_rate > 2.98
)
SELECT * FROM high_rentals WHERE rating = 'PG';
```

## 8️⃣ If-then logic (CASE)

```sql
SELECT title,
  CASE
    WHEN rental_rate < 1 THEN 'budget'
    WHEN rental_rate < 3 THEN 'standard'
    ELSE 'premium'
  END AS price_tier
FROM film;
```

## 9️⃣ Dates & math (EXTRACT, operators, ROUND)

**EXTRACT** (PostgreSQL) pulls one unit from a date/timestamp: `EXTRACT(unit FROM date_column)`.
Units: `day` (1–31), `dow` (0=Sunday…6=Saturday), `doy`, `week`, `month` (1–12), `quarter` (1–4), `year`, `hour`, `minute`, `second`, `epoch`.

```sql
SELECT EXTRACT(day FROM payment_date) FROM payment;

-- Monthly totals — the report pattern I'll reuse forever:
SELECT SUM(amount), EXTRACT(month FROM payment_date) AS month
FROM payment
GROUP BY month
ORDER BY SUM(amount);
```

**Math on columns:** `+  -  *  /  %` work right in SELECT: `SELECT amount * 1.0825 AS with_tax FROM payment;`
- ⚠️ **Integer ÷ integer truncates** (`4/2=2` but `5/2=2`, not 2.5) — multiply by `1.0` or cast to force decimals.
- `ROUND(number, decimals)`: `SELECT ROUND(amount, 1) FROM payment;`
- Postgres extras: `^` power, `|/` square root, `!` factorial.

## 🔟 Changing data (INSERT, UPDATE, DELETE) — the "handle with care" section

```sql
-- Insert one row (name the columns — always):
INSERT INTO weblinks (url, name) VALUES ('www.google.com', 'Google');

-- Insert several rows at once:
INSERT INTO weblinks (url, name)
VALUES ('www.amazon.com', 'Amazon'),
       ('www.ign.com', 'IGN'),
       ('www.cuny.edu', 'CUNY');

-- Insert from another table:
INSERT INTO table SELECT col1, col2 FROM other_table WHERE condition;

-- Update matching rows:
UPDATE weblinks
SET description = 'Website for all your shopping needs'
WHERE name = 'Amazon';

-- Delete matching rows:
DELETE FROM weblinks WHERE id = 3;
```

⚠️ **UPDATE or DELETE without a WHERE hits EVERY row in the table.** `UPDATE weblinks SET description = 'x';` overwrites all descriptions; `DELETE FROM weblinks;` empties the table. Habit from the course: write the `WHERE` first, or run it as a `SELECT` first to see which rows you're about to touch.

- Columns you skip in an INSERT get NULL (or their DEFAULT). A `serial` id column fills itself — and keeps counting even after deletes.

## 1️⃣1️⃣ Creating & changing tables (DDL)

```sql
CREATE TABLE weblinks (
  id          serial PRIMARY KEY,          -- serial = auto-numbering (Postgres)
  url         VARCHAR(255) NOT NULL,
  name        VARCHAR(255) NOT NULL,
  description VARCHAR(255)                  -- nullable
);

CREATE TABLE copy_table (LIKE weblinks);    -- copies structure only, NOT the data

ALTER TABLE t ADD column_name datatype;     -- add a column
ALTER TABLE t DROP COLUMN c;                -- remove a column
ALTER TABLE t1 RENAME TO t2;                -- rename table
ALTER TABLE t1 RENAME c1 TO c2;             -- rename column

TRUNCATE TABLE t;   -- remove all rows, keep the table
DROP TABLE t;       -- remove the whole table
```

**Constraints** (set the rules once, the database enforces them forever):
`PRIMARY KEY` (unique row ID), `FOREIGN KEY (c) REFERENCES other(c)` (must exist in the other table), `NOT NULL`, `UNIQUE`, `DEFAULT value`, `CHECK (condition)`.

**Views** — save a query as a virtual table: `CREATE VIEW v AS SELECT c1, c2 FROM t;` (query it like a table; `DROP VIEW v;` to remove).
**Indexes** — speed up lookups on busy columns: `CREATE INDEX idx_name ON t(c1);`

## 1️⃣2️⃣ Getting a CSV into PostgreSQL

1. Create a table whose columns match the CSV, then either:
   - **pgAdmin GUI:** right-click the table → **Import/Export Data** → Import tab → pick the file, Format CSV, Header on, Delimiter `,` → OK.
   - **COPY command:**
     ```sql
     COPY students (id, name, age)
     FROM 'C:/Users/YourName/Desktop/students.csv'
     DELIMITER ',' CSV HEADER;
     ```
     (Forward slashes even on Windows.)
2. Verify with `SELECT * FROM students;`

## 1️⃣3️⃣ Breaking a flat CSV into real tables (normalization recipe)

Kaggle-style flat files repeat the same values thousands of times. The course recipe (from the salaries-dataset guide):

1. **Stage it:** load the whole CSV into one `raw_` table.
2. **Spot the categorical columns** (job_title, location, size...) — those become **dimension tables**.
3. **Build each dimension:** `CREATE TABLE jobs (job_id SERIAL PRIMARY KEY, job_title TEXT, ...);` then
   `INSERT INTO jobs (job_title, job_category) SELECT DISTINCT job_title, job_category FROM raw_salaries;`
4. **Build the central fact table** with `INT REFERENCES` foreign keys to each dimension.
5. **Fill it by joining the raw table back to the dimensions** on the text values, selecting the new IDs.

Payroll framing: the raw CSV is a check register with the employee's name/department typed on every line; normalization moves those to the employee master and department list, leaving the register to carry just IDs and amounts.

## 🚨 Common mistakes checklist (from the course + my own graded assignments)

1. **Missing WHERE on UPDATE/DELETE** → whole table changed. Run it as a SELECT first.
2. **Double quotes on strings** → use `'single quotes'`; `"double"` means an identifier in Postgres.
3. **`= NULL`** → returns nothing. Use `IS NULL`.
4. **Aggregate in WHERE** (`WHERE COUNT(*) > 5`) → error. Move it to HAVING.
5. **Column in SELECT missing from GROUP BY** → error (or nonsense in some dialects).
6. **Forgetting `ON` in a join** (or `FROM t1, t2` with no WHERE) → accidental cross join, millions of rows.
7. **Integer division** silently truncating money math → cast to numeric/multiply by 1.0.
8. **BETWEEN is inclusive** on both ends — check your date boundaries (a `BETWEEN '05-29' AND '05-30'` cuts off at midnight on the 30th).
9. **Spaces in column names** break queries → snake_case (`total_pay`, never `total pay`).
10. **ORDER BY inside a subquery** → not allowed; sort in the outer query.

## 🔑 Key concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **SELECT / FROM / WHERE** | Which columns, from which table, which rows qualify | "Give me name and gross pay, from the payroll register, for dept 40 only" |
| **DISTINCT** | Unique values only | The list of departments that appear on this run — not one line per employee |
| **GROUP BY + aggregate** | Collapse rows into per-category totals | The payroll summary page: total gross by department, headcount by location |
| **HAVING** | Filter on the *totals*, not the rows | "Only show departments whose OT total exceeds $10K" |
| **JOIN** | Match rows across tables on a shared key | Matching timesheets to the employee master by employee ID |
| **LEFT JOIN + IS NULL** | Keep everything from one side, flag the gaps | The exception report: employees with *no* timesheet this week |
| **UNION / EXCEPT** | Stack two lists / subtract one list from another | Merging two location registers / finding who's in ADP but not in the GL |
| **Subquery** | Use one query's answer inside another | "Who earns above average?" — you need the average first; the subquery fetches it inline |
| **CASE** | If-then buckets inside a query | The earnings-code buckets: regular vs OT vs bonus columns on one report |
| **EXTRACT** | Pull month/quarter/year out of a date | Turning check dates into pay periods for the quarterly 941 rollup |
| **INSERT / UPDATE / DELETE** | Add, change, remove rows | New-hire entry, rate change, purging a duplicate record — with the same "audit before you post" discipline |
| **Constraints** | Rules the database enforces automatically | The system refusing a duplicate employee ID or a blank SSN field — validation built into the filing cabinet |

## 🗣️ Teach it to a friend

Every SQL query is a report request written in a fixed order: what columns (SELECT),
from which filing cabinet (FROM), matched to which other cabinets (JOIN ... ON the shared
ID), keeping which records (WHERE), subtotaled how (GROUP BY), keeping which subtotals
(HAVING), sorted (ORDER BY), and capped (LIMIT). Reading data can't break anything, so
experiment freely — the only sharp knives are UPDATE and DELETE, which change real
records and will hit *every* row unless you aim them with a WHERE. And when a question
needs an answer you don't have yet ("above average?"), you nest a mini-query in
parentheses to fetch that number inline — that's a subquery.

## 🃏 Flashcards

**Q:** WHERE vs HAVING?
**A:** WHERE filters rows before grouping; HAVING filters groups after aggregation. Aggregates only work in HAVING.

**Q:** INNER JOIN vs LEFT JOIN?
**A:** INNER keeps only matches in both tables; LEFT keeps all left-table rows and fills NULLs where the right table has no match.

**Q:** How do you find rows in table A with no match in table B?
**A:** `LEFT JOIN B ON ... WHERE B.key IS NULL`.

**Q:** COUNT(*) vs COUNT(column)?
**A:** COUNT(*) counts all rows; COUNT(column) skips NULLs in that column.

**Q:** What happens if you run DELETE (or UPDATE) without WHERE?
**A:** It hits every row in the table — deletes everything / overwrites the column everywhere.

**Q:** UNION vs UNION ALL?
**A:** Both stack results; UNION removes duplicates, UNION ALL keeps them (and is faster).

**Q:** Three rules for subqueries?
**A:** Parentheses required; placed on the right of the comparison; no ORDER BY inside (sort in the outer query).

**Q:** Single or double quotes for text values in SQL?
**A:** Single quotes ('US'). Escape an internal apostrophe by doubling it ('O''Brien').

**Q:** How do you get the month out of a timestamp in PostgreSQL?
**A:** `EXTRACT(month FROM date_column)` — units include day, dow, week, month, quarter, year.

**Q:** What does `CREATE TABLE copy (LIKE original);` copy?
**A:** Only the structure/schema — not the data.

## 💡 How I'll actually use this

- **flask-analytics-app**: the monthly-totals pattern (`EXTRACT month + GROUP BY + SUM`) is exactly the summary endpoint I want; SQLite's version of EXTRACT is `strftime('%m', col)` — same idea, different spelling.
- **nyc-payroll-explorer**: LEFT JOIN + IS NULL is the "agencies with no OT records" exception report; CASE is how I bucket pay bands; HAVING drives "only agencies over $1M total".
- Keep practicing on **dvdrental** in pgAdmin — it's installed, and the film/rental/payment tables behave like a mini payroll system (transactions + master tables).
- Interview line: "I've written exception reports my whole career — SQL's LEFT JOIN ... IS NULL is the same audit, just automated."
