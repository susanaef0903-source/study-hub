# Google Data Analytics — Course 1, Module 3: Set Up Your Toolbox

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 3 readings

## 🎯 What this module is about (one sentence)

Hands-on basics of the three core tools — spreadsheets, SQL queries (SELECT/FROM/WHERE),
and planning a data visualization.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Attribute** | A characteristic of the data — labels a *column* | The column headers on your payroll register: Employee ID, Gross Pay, Dept. |
| **Observation** | All the attributes for one item — a *row* | One employee's line on that register. |
| **SELECT / FROM / WHERE** | The skeleton of every SQL query: which columns, which table, which rows | "Give me Name and Gross Pay (SELECT), from the March register (FROM), for Dept 200 only (WHERE)." The report request, written yourself. |
| **Syntax** | The required structure/grammar of a language | Like the exact IRS form layout — right info in the wrong box still gets rejected. |
| **String** | Text data, in single quotes in SQL ('Chavez') | An employee's last name or a job code — anything that isn't math-able. |
| **LIKE and % wildcard** | Pattern matching: `WHERE last_name LIKE 'Ch%'` finds Chavez *and* Chen | Filtering the register for every cost center starting with "42". |
| **AND / OR / NOT, <>, <=** | Combine conditions in WHERE; `<>` means "not equal" | "Everyone earning ≤ $30,000 AND not a temp (<>'INT')" — exactly the audit pulls you used to request from IT. |
| **SELECT \*** | Grab every column | Printing the full register when you only needed two columns — legal, but slow and wasteful on big tables. Use sparingly. |
| **Comment (-- or /* */)** | Notes in the query the database ignores | The sticky note on the workpaper explaining *why* you filtered that way — for future-you and reviewers. |
| **Alias (AS)** | A temporary nickname for a column or table, for that query only | Calling "field1" → "last_name" so the output makes sense; doesn't rename anything in the system. |
| **Semicolon ;** | Optional statement terminator (ANSI standard) | The period at the end of the sentence — some databases require it, some shrug. |
| **Formula vs. sorting in spreadsheets** | =C2+C3+C4 to compute; Data → Sort range to organize | Second nature after 20 years of Excel — the course version is Google Sheets, same moves. |
| **Data visualization** | The graphical representation of data | Turning the OT-by-department table into the one bar chart the CFO actually looks at. |

### Planning a visualization (3 steps)
1. **Explore the data for patterns** — what jumps out (e.g., sales cluster in the northeast)?
2. **Plan your visuals** — match chart to question: line = trend over time, map = by location,
   donut/pie = segments, bar = comparisons
3. **Create your visuals** — iterate; expect to try several formats before one lands

### Viz toolkit ladder
- **Spreadsheets** (Excel/Sheets): quick bar, pie, line — plus maps, waterfall, funnel
- **Tableau**: interactive dashboards, pulls from almost any system; Tableau Public is free
- **Python**: Matplotlib (the flexible foundation), Seaborn (polished stats charts fast),
  Plotly (interactive, click/zoom/hover) — a *library* is pre-written code for a task
- **R**: visualization via Posit (formerly RStudio)

## 🗣️ Teach it to a friend

SQL sounds intimidating but a basic query is three lines of plain English: SELECT the columns
you want, FROM the table where they live, WHERE the rows meet your condition. It's a Mad Lib.
Want everyone named Tony? `WHERE first_name = 'Tony'`. Want every last name starting with
"Ch"? `LIKE 'Ch%'` — the % is a wildcard. Stack conditions with AND. Leave comments with `--`
so future-you knows what the query was for, and nickname ugly column names with AS. The
spreadsheet half is stuff you already do — labels in row 1 (attributes), one record per row
(observations), sort, and formulas. And when it's time to show results, match the chart to the
question: lines for trends, bars for comparisons, maps for geography, donuts for shares of a whole.

## 🃏 Flashcards

**Q:** What three clauses form the skeleton of every basic SQL query, and what does each do?
**A:** SELECT (which columns), FROM (which table), WHERE (which rows/conditions).

**Q:** In a table, what's an attribute vs. an observation?
**A:** Attribute = a column label (a characteristic); observation = a row (all the attributes for one item).

**Q:** Write a WHERE clause that finds all last names starting with "Ch".
**A:** `WHERE last_name LIKE 'Ch%'` — the % wildcard matches one or more characters.

**Q:** What does <> mean in SQL?
**A:** "Does not equal" (e.g., `WHERE jobCode <> 'INT'` excludes interns).

**Q:** Why should you use SELECT * with caution?
**A:** It returns every column — on wide tables that's a huge amount of data and can make queries run slowly. Select only what you need.

**Q:** Two ways to write a comment in SQL?
**A:** `-- comment` (two dashes) or `/* comment */`. (# works in some databases but not all — MySQL doesn't recognize it.)

**Q:** What does an alias (AS) do, and does it rename the column in the database?
**A:** It gives a column or table a temporary, easier name for the duration of that query only — the database is unchanged.

**Q:** Which Python library gives you polished statistical charts quickly, and which one makes interactive charts?
**A:** Seaborn (built on Matplotlib) for polished stats charts; Plotly for interactive graphs and dashboards.

## 💡 How I'll actually use this

- The reading's big example is literally an Employee table with jobCode and salary, filtering
  `salary <= 30000 AND jobCode <> 'INT'` for pay-equity flags — I can rebuild that exact query
  against nyc-payroll-explorer's data as a portfolio piece.
- flask-analytics-app: add `--` comments and AS aliases to my existing queries so the repo reads
  like professional work, not homework.
- Next chart I build, run the 3-step plan first (pattern → plan → create) instead of jumping
  straight to the default bar chart.
- Interview line: "SQL's WHERE clause is the filter dialog I always wished my payroll system had —
  I just write it myself now."
