# Google Data Analytics — Course 4, Module 3: Data Cleaning with SQL

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 3 readings + module 3 glossary

## 🎯 What this module is about (one sentence)

Same cleaning discipline as module 2, but when the data lives in a database instead of a
spreadsheet — you use SQL (Standard SQL in BigQuery for this program) to find duplicates,
fix types, fill Nulls, trim strings, and build unique keys, and you learn how to decide when SQL
beats a spreadsheet.

**Sue's note:** SQL is a reconciliation you write down instead of clicking through. Every query is
a documented, re-runnable audit step — which is exactly what an auditor wants and exactly what
you couldn't get from a spreadsheet full of manual fixes. The rule for choosing the tool is one
sentence: **where the data lives decides.**

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **SQL (Structured Query Language)** | The language used to talk to databases; the primary way analysts extract data | The report writer behind every payroll system's "custom report" screen — you've been generating SQL through a GUI for years. |
| **SQL dialect** | A database product's own variant of SQL (MySQL, SQL Server, PostgreSQL, SQLite, BigQuery) — small syntax differences | ADP vs. Paychex vs. Workday report builders: same idea, slightly different buttons. Learn one well and the others are an adjustment. |
| **Standard SQL** | The common dialect that works with most databases with minimal changes; the one this program teaches | Learn GAAP first, then the company-specific chart of accounts. |
| **BigQuery** | Google Cloud's data warehouse for querying, filtering, and aggregating large datasets; where you practice SQL in this program | A giant, hosted version of the payroll history database — you can query 10 years of checks in seconds. |
| **Sandbox account** | Free BigQuery tier: no payment info, max 12 projects, quotas, and **no INSERT/UPDATE of records** — fine for all Course 4 activities | Read-only access to the payroll history: you can look and report, you can't post. |
| **Free-of-charge trial** | $300 credit for 90 days; asks for payment info but doesn't auto-charge; standard limits | Full-access login — but they want a card on file. |
| **Project / Dataset / Table** | BigQuery's hierarchy: a project holds datasets, a dataset holds tables (e.g., `customer_data.customer_address`) | Company → ledger → account. Or: payroll system → pay group → register. |
| **Schema** | The column names and data types of a table; BigQuery can auto-detect or you can edit it as text (JSON) | The file layout spec you'd get from a carrier: field name, type, length, position. |
| **Auto detect vs. edit-as-text schema** | Auto detect guesses types from the data; edit as text lets you force a type (e.g., STRING instead of FLOAT for `purchase_price`) — and set **Header rows to skip = 1** | Telling the import "SSN is text, not a number" so leading zeros survive. You've fought this exact battle. |
| **Explorer pane / SQL Workspace / Navigation pane** | Explorer: your projects, starred public datasets, + ADD button. SQL Workspace: where you write and run queries, with query history. Navigation: moves between GCP tools | Left panel = the tree of companies and reports; main panel = the report designer; history = your saved report log. |
| **Public datasets** | `bigquery-public-data` — free datasets (e.g., `noaa_lightning`, `austin_311`) to star and query; each table has Schema / Details / Preview tabs | The BLS or Census tables you'd pull for benchmarks — already loaded and queryable. |
| **DISTINCT** | Keyword added to SELECT to return only non-duplicate values | `COUNT(DISTINCT employee_id)` = true headcount, not number of paychecks. |
| **CAST / Typecasting** | Converts data from one type to another (STRING → FLOAT, STRING → DATE) | The "$1,250.00" text field that has to become a number before you can total it; the date-as-text column from the import. |
| **Float** | A number that contains a decimal | Pay rate 23.75, hours 37.5 — never store money as an integer of dollars. |
| **COALESCE** | Returns the first non-null value in a list | "Use the override rate if there is one, otherwise the standard rate" — `COALESCE(override_rate, standard_rate)`. |
| **CONCAT** | Adds strings together — often to build a unique key | Employee ID + pay period end date = a unique check key when the source has no check number. |
| **Substring** | A subset of a text string (SQL: `SUBSTR`) | Pulling the department segment out of a GL account string; the last 4 of an SSN. |
| **Spreadsheet vs. SQL** | Spreadsheets: smaller data, manual entry, charts in the same tool, spellcheck, solo work. SQL: larger data, tables across a database, prep for other software, fast, collaborative, tracks everyone's queries | A department's timesheet summary → spreadsheet. Five years of company-wide payroll history → SQL. |

### The junior analyst's decision: spreadsheet or SQL? (exam favorite!)
1. **Where does the data live?** Database → SQL. Spreadsheet → spreadsheet (pivot + formulas + filters).
2. Business task in the reading: "How many users joined since Feb 15, 2020?" In a spreadsheet: pivot table, filters, several steps. In SQL: one query.

```sql
SELECT
  COUNT(DISTINCT user_id) AS count_of_unique_users
FROM
  table
WHERE
  join_date >= '2020-02-15'
```

*(Payroll version: "How many distinct employees were paid after the acquisition date?" — one query, and `DISTINCT` keeps the bonus-run second check from double-counting anyone.)*

| Spreadsheets | SQL databases |
|---|---|
| Smaller datasets | Larger datasets |
| Enter data manually | Access tables across a database |
| Create graphs/visualizations in the same program | Prepare data for further analysis in another program |
| Built-in spellcheck and other handy functions | Fast and powerful functionality |
| Best when working solo | Great for collaboration; tracks queries run by all users |

### SQL dialects
- Some database products have their own SQL variant; dialects differ by company and can change if the company switches databases.
- Most analysts **start with Standard SQL** and adjust — it works with a majority of databases with a small number of syntax changes.
- Resources named in the reading: LearnSQL "What Is a SQL Dialect," Software Testing Help "SQL vs MySQL vs SQL Server," Datacamp "SQL Server, PostgreSQL, MySQL... what's the difference?" (note the reading's correction: SQLite **does** support window functions), SQL Tutorial "What is SQL."
- Non-BigQuery alternatives offered: MySQL, Microsoft SQL Server, PostgreSQL, SQLite.

### BigQuery setup, condensed
- **Sandbox:** go to the sandbox docs page → log in with a Google account → "Go to BigQuery" → pick country, accept terms → SQL Workspace with an auto-created project. Free, no card, 12-project cap, no INSERT/UPDATE.
- **Free trial:** BigQuery page → "Try BigQuery free" → log in → country/org/terms → billing info → "START MY FREE TRIAL." $300 / 90 days; no auto-charge afterward.
- **Moving between tiers:** upgrade keeps your projects; trial → sandbox after expiry does **not** (sandbox starts from scratch).
- **Console anatomy:** Navigation pane (GCP tools) → Explorer pane (projects, + ADD, star `bigquery-public-data`) → SQL Workspace (write/run queries; personal and project history).
- **Add a public dataset:** + ADD → Public Datasets → Marketplace → search (e.g., "noaa lightning") → View dataset. Tables show Schema / Details / Preview tabs and a Query button.

### Uploading your own CSV to BigQuery (both readings)
1. Explorer → three-dot Actions next to project → **Create dataset** → Dataset ID `customer_data` (Multi-region US, Google-managed key defaults).
2. Open the dataset → **+ CREATE TABLE** → Source: **Upload** → Browse to the CSV → format **CSV**.
3. Table name (`customer_address` / `customer_purchase`).
4. Schema: **Auto detect** (easy path) — or **Edit as text** and paste a JSON array of `{name, type, mode, description}` when auto-detect picks the wrong type (the store-transactions file forces `purchase_price` to STRING instead of FLOAT).
5. If you edited the schema as text: Advanced options → **Header rows to skip = 1**, or you'll get parsing errors (BigQuery tries to type the header row).
6. Create table → check the **Schema** and **Preview** tabs to confirm.

Types seen in the schema: `DATETIME`, `INTEGER`, `STRING`, `FLOAT`; mode `NULLABLE`.

## 🗣️ Teach it to a friend

SQL is how you talk to a database, and the rule for when to use it is simple: if the data lives
in a database, use SQL; if it lives in a spreadsheet, use the spreadsheet. Databases have
"dialects" — MySQL, SQL Server, PostgreSQL, BigQuery all speak slightly differently — but you
learn Standard SQL first and adjust, the way you'd learn standard accounting and then a
company's specific system. In this course you practice in BigQuery, Google's cloud data
warehouse: a free sandbox account lets you query public datasets and upload your own CSVs
(you define the table's schema — the column names and types — either by letting BigQuery guess
or by typing it out when it guesses wrong). The cleaning toolkit in SQL mirrors the spreadsheet
one: `DISTINCT` de-duplicates, `CAST` fixes a column that's the wrong type, `COALESCE` fills a
Null with a fallback, `CONCAT` glues fields into a unique key, and `SUBSTR` pulls a piece out of a
string. The payoff over a spreadsheet: bigger data, one query instead of ten clicks, and every
step is written down and re-runnable — which is what makes it auditable.

## 🃏 Flashcards

**Q:** What single question decides whether a junior analyst uses a spreadsheet or SQL?
**A:** Where does the data live? Database → SQL; spreadsheet → spreadsheet.

**Q:** What is a SQL dialect, and which one does this program teach?
**A:** A database product's own variant of SQL; the program teaches Standard SQL, which works with most databases with minor syntax changes.

**Q:** Name four SQL database platforms besides BigQuery mentioned as alternatives.
**A:** MySQL, Microsoft SQL Server, PostgreSQL, SQLite.

**Q:** What does DISTINCT do?
**A:** Added to a SELECT statement, it returns only non-duplicate entries — e.g., `COUNT(DISTINCT user_id)`.

**Q:** What is typecasting, and which SQL function does it?
**A:** Converting data from one type to another; `CAST` (e.g., a STRING to a FLOAT or DATE).

**Q:** What does COALESCE return?
**A:** The first non-null value from a list of values — a way to supply a fallback for Nulls.

**Q:** Why would you use CONCAT during cleaning?
**A:** To join strings into a new text string — commonly to build a unique key from several fields.

**Q:** What is a float?
**A:** A number that contains a decimal (e.g., 7.30).

**Q:** What are the limits of a BigQuery sandbox account?
**A:** Max 12 projects, quotas on data processed, and no inserting or updating records — but no payment info required and it covers all Course 4 activities.

**Q:** What does the BigQuery free trial give you, and does it auto-charge?
**A:** $300 credit for 90 days; it asks for payment info but does not automatically charge when the trial ends.

**Q:** Name the three main BigQuery console components.
**A:** Navigation pane, Explorer pane, and SQL Workspace.

**Q:** When uploading a CSV with an edit-as-text schema, what Advanced option must you set?
**A:** Header rows to skip = 1 — otherwise BigQuery tries to apply the schema to the title row and throws parsing errors.

**Q:** Why edit a schema as text instead of using Auto detect?
**A:** When auto-detect picks the wrong type for a field — e.g., forcing `purchase_price` to STRING instead of FLOAT.

**Q:** Give three advantages of SQL databases over spreadsheets.
**A:** Handle larger datasets, access tables across a database, fast and powerful functionality, good for collaboration and tracking queries run by all users. (Spreadsheets win for small data, manual entry, built-in charts, and solo work.)

**Q:** What tabs describe a table in BigQuery's SQL Workspace?
**A:** Schema (column names), Details (metadata like creation date), and Preview (first rows).

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** the NYC payroll data is big enough that "where the data lives" says database. Load the CSV into BigQuery (or SQLite locally) and rewrite the module 2 checks as SQL: `COUNT(DISTINCT ...)` for true headcount vs. row count, `CAST` the pay columns that arrive as text, `COALESCE(ot_hours, 0)` only *after* confirming blank means zero, `CONCAT(agency, '-', title)` as a grouping key. Save the queries in the repo — a documented, re-runnable audit trail.
- **flask-analytics-app:** the app already talks to a database — practice `DISTINCT`, `CAST`, and `COALESCE` in its queries instead of cleaning in pandas after the fact ("clean where it lives," from module 2).
- **BigQuery sandbox:** set it up (no card needed), star `bigquery-public-data`, and practice the upload flow with a small payroll-shaped CSV, deliberately editing the schema as text so an ID column stays STRING and keeps its leading zeros — the exact conversion bug I've fixed in real life.
- **Job hunt:** job posts say "SQL required" — I can now say Standard SQL in BigQuery, explain dialects, and describe cleaning with DISTINCT/CAST/COALESCE/CONCAT in plain terms.
- **Interview line:** "Choosing between a spreadsheet and SQL comes down to where the data lives. When I reconciled a department's hours, that was a spreadsheet job; five years of company-wide payroll history is a database job — and writing it in SQL means every cleaning step is documented and re-runnable, which is what an auditor actually wants."
