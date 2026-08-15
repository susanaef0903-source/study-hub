# Google Data Analytics — Course 3, Module 1: Data Types & Structures

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 1 readings

## 🎯 What this module is about (one sentence)

How data comes in different formats and shapes (wide vs. long, structured vs. unstructured),
how to pick the right data for the question, and how to reshape it with transformations and
filter it with Boolean logic.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **First-party data** | Data you collected yourself with your own resources | Your own payroll register — you ran the payroll, you own the numbers. |
| **Second-party data** | Data another group collected directly, then sold to you | Salary survey data you bought straight from the firm that surveyed the companies. |
| **Third-party data** | Data sold by a provider who didn't collect it themselves | A benefits broker reselling benchmark data they got from somewhere else — check it twice. |
| **Internal vs. external data** | Inside your company's systems vs. outside it | HR's wage records by department (internal) vs. BLS national average wages (external). |
| **Continuous data** | Measured; can take almost any numeric value | Hours worked: 37.25, 40.5 — anything on the clock. |
| **Discrete data** | Counted; limited set of values | Headcount. You can't have 42.7 employees. |
| **Nominal data** | Categories with no built-in order | Pay type: hourly, salaried, contractor. No one comes "first." |
| **Ordinal data** | Categories with a set order or scale | Performance ratings: exceeds, meets, needs improvement — the order means something. |
| **Structured data** | Organized in rows and columns; easy to search and analyze | Every payroll register, GL export, and timesheet you've ever touched. |
| **Unstructured data** | No easy rows-and-columns organization | The pile of emailed PTO requests, scanned doctor's notes, and voicemails behind those records. |
| **Wide data** | One row per subject, many columns for its attributes | One row per employee: Jan gross, Feb gross, Mar gross... across the columns. |
| **Long data** | Multiple rows per subject, one observation per row | Pay history detail: one row per employee *per pay period*. Same info, stacked tall. |
| **Data model** | A diagram of how data elements relate to each other | The org chart, but for your data — who connects to whom and how. |
| **Data transformation** | Changing data's format, structure, or values | Reformatting the old system's export so it loads into the new payroll system during a conversion. You've lived this. |
| **Boolean data** | Only two possible values: true or false | The "Active?" or "Exempt?" checkbox on an employee record. |

### The three levels of data modeling (exam favorite!)
1. **Conceptual** — high-level view, business requirements, no technical details → *the idea on the whiteboard*
2. **Logical** — relationships, entities, how records are uniquely identified — but no actual table names → *the process narrative*
3. **Physical** — the real thing: table names, column names, data types → *the actual chart of accounts, built*

Two common modeling techniques you might see: **ERD** (Entity Relationship Diagram — boxes and lines showing how entities relate) and **UML** (a more detailed system diagram). As a junior analyst you read these; you don't design them.

## 🗣️ Wide vs. long, and when to use each

- **Wide** is easier to *read* and great for charts comparing a few attributes — analysts convert long → wide more often than the reverse.
- **Long** is better for *storing* lots of observations (e.g., 60 years of interest rates per bank) and for advanced statistical work — most Python/pandas and SQL work prefers long.
- Transformation goals to remember: organization, compatibility, migration, merging, enhancement, comparison. (Mario the plumber merging two customer databases = compatibility + merging + de-duplication.)

## 🗣️ Boolean logic in 30 seconds

- **AND** = both conditions must be true. `Grey AND Pink` → only the grey-and-pink pair qualifies.
- **OR** = either condition works. `Grey OR Pink` → grey pairs, pink pairs, and both.
- **NOT** = subtract a condition. `Grey AND NOT Pink` → grey shoes with zero pink.
- Parentheses group conditions: `(Grey OR Pink) AND Waterproof`.
- Payroll version you already run in your head: "employees who are **hourly AND active AND NOT on leave**" — that's a Boolean statement.

## 🗣️ Teach it to a friend

Data comes in shapes. A payroll summary with one row per employee and a column for every
month is *wide* — easy to eyeball. The same numbers stacked as one row per employee per
month is *long* — easier for software to crunch. Neither is wrong; you *transform* between
them depending on the question. Before any of that, you pick the right data: did you collect
it yourself (first-party) or buy it (second/third-party)? Is it measured (continuous) or counted
(discrete)? And when you filter it, you use the same AND/OR/NOT logic you'd use telling a temp
which files to pull: "active employees, hourly OR salaried, but NOT terminated."

## 🃏 Flashcards

**Q:** What's the difference between wide data and long data?
**A:** Wide = one row per subject with many columns of attributes. Long = multiple rows per subject, one observation (e.g., one time point) per row.

**Q:** Which direction do analysts transform more often — long to wide, or wide to long — and why?
**A:** Long to wide, because wide data is easier to read and chart.

**Q:** First-party vs. second-party vs. third-party data?
**A:** First-party = you collected it yourself. Second-party = collected directly by another group, then sold. Third-party = sold by a provider who didn't collect it themselves.

**Q:** Continuous vs. discrete data — which is measured and which is counted?
**A:** Continuous is measured (can be almost any value, like 40.25 hours); discrete is counted (limited values, like 12 employees).

**Q:** Nominal vs. ordinal data?
**A:** Both are qualitative categories, but ordinal has a set order (satisfaction ratings); nominal does not (pay types).

**Q:** Name the three levels of data modeling from least to most detailed.
**A:** Conceptual (business view), logical (entities and relationships, no table names), physical (actual table names, columns, data types).

**Q:** What does `IF (Color="Grey") AND (Color=NOT "Pink")` return?
**A:** Only items that are grey AND have no pink — NOT subtracts the exception.

**Q:** Give two examples of unstructured data.
**A:** Any two of: emails, social media posts, videos, audio files, satellite images, PDFs, open-ended survey answers.

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** the NYC payroll dataset is *long* (one row per employee per fiscal year). When I want a chart comparing agencies year over year, I'll pivot it wide — now I know the vocabulary for what I've been doing.
- **flask-analytics-app:** my SQL `WHERE` clauses are Boolean statements — `WHERE status = 'active' AND dept != 'temp'` is AND/NOT logic. Truth tables explain why a misplaced OR returns too many rows.
- Interview line: "I've done data transformation for years — every payroll system conversion is reformatting, standardizing field names, merging, and de-duplicating. This module gave me the official terms for it."
