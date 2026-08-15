# Google Data Analytics — Course 3, Module 3: Databases, BigQuery & Metadata

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 3 readings

## 🎯 What this module is about (one sentence)

How data lives in databases, how to talk to it professionally with SQL, and why the
*data about the data* (metadata) matters as much as the data itself.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Primary key** | A column where every value is unique — the row's ID | The employee ID on a payroll record. No two employees share one. |
| **Foreign key** | A column that points to another table's primary key | The employee ID *also* appearing on each timesheet row — it links the timesheet back to the employee. |
| **Normalized database** | Each table holds only related data, no repeats | You never stored an employee's address on every paystub — it lives once, in the personnel file. Same idea. |
| **Redundancy** | The same data stored in two+ places | Two copies of a W-4 in two folders — which one is current? That's why databases avoid it. |
| **Schema** | The blueprint of how data is organized | The chart of accounts, but for a database: what tables exist and what columns they hold. |
| **Metadata** | Data about data | The label on the folder: who created this file, when, what's in it. Not the paystubs themselves — the cover sheet. |
| **Metadata repository** | A database that stores metadata | A master index of all the folder labels. |
| **Data governance** | Formal management of a company's data assets | The controls you already know from audits — but applied to data instead of dollars. |
| **CSV file** | Plain text file, values separated by commas | The export format every payroll system produces. You've handled thousands. |
| **BigQuery** | Google's cloud data warehouse for querying huge datasets with SQL | Like your accounting system's reporting module, but it can handle billions of rows. |

### The three types of metadata (exam favorite!)
1. **Descriptive** — identifies the data (title, description) → *the folder label*
2. **Structural** — how it's organized, what collection it belongs to → *the table of contents*
3. **Administrative** — technical source (when created, by what device) → *the audit trail*

## 🗣️ SQL best practices (from the field guide)

- **CAPITALIZE clause starters** (`SELECT`, `FROM`, `WHERE`) and functions (`SUM()`); lowercase column names
- **snake_case for columns** (`total_tickets`, never `total tickets` — spaces break SQL)
- **CamelCase for tables** (`TicketsByOccasion`)
- **Single quotes for strings** (`'US'`); double quotes only when the string has an apostrophe (`"Shepherd's pie"`)
- **⚠️ BigQuery is CASE-SENSITIVE for data**: `'us'` ≠ `'US'` in BigQuery (MySQL/PostgreSQL don't care). This trips people up.
- **Name your computed columns** (`SUM(x) AS total_x`) or SQL names them `f0`, `f1`...
- **Comment your queries** with `--` (works in every dialect; `#` doesn't)
- **Keep lines ≤ 100 characters**, indent for readability

## 🗣️ Teach it to a friend

A database is a set of filing cabinets (tables). Each drawer of records has one ID stamp
that makes every record findable (primary key), and records in other drawers reference
that stamp instead of copying the whole file (foreign key) — so nothing is stored twice
(normalization). SQL is how you ask the cabinets questions, and metadata is the labeling
system that tells you what's in each drawer, who filed it, and when — without it, you have
a room full of unlabeled paper.

## 🃏 Flashcards

**Q:** What's the difference between a primary key and a foreign key?
**A:** A primary key uniquely identifies each row in its own table; a foreign key is that same value appearing in *another* table to link them.

**Q:** Metadata is defined as...?
**A:** Data about data.

**Q:** Name the three types of metadata.
**A:** Descriptive (identifies it), Structural (how it's organized), Administrative (technical source).

**Q:** Which is case-sensitive about data values: BigQuery or MySQL?
**A:** BigQuery ('us' ≠ 'US'). MySQL, PostgreSQL, and SQL Server are not.

**Q:** Why should you never use spaces in SQL column names, and what do you use instead?
**A:** Spaces cause syntax errors; use snake_case (total_tickets).

**Q:** What does a normalized database avoid?
**A:** Redundancy — the same data stored in multiple places.

**Q:** In a SQL query, what do SELECT, FROM, and WHERE each do?
**A:** SELECT = which columns; FROM = which table; WHERE = which rows qualify.

## 💡 How I'll actually use this

- My flask-analytics-app already does SELECT/FROM/WHERE/GROUP BY against SQLite — same skills, smaller scale than BigQuery.
- Next BigQuery lab: practice on the public datasets (bigquery-public-data), remember the case-sensitivity gotcha.
- Interview line: "I managed data governance before I knew the term — payroll audit trails, DOL reporting records, and document retention *are* metadata management."
