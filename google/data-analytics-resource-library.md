# Google Data Analytics — Resource Library (Courses 1–3 official links)

**Platform:** Coursera (Google Data Analytics) | **Compiled:** Aug 2026 | **Source:** "Resources and citations" readings from Course 1 Module 4, Course 2 Module 4, and Course 3 Module 5

## 🎯 What this file is

Not a study guide — a **curated link shelf**. These are the two "resources and citations"
readings Google hands out at the end of Course 1 and Course 2. Instead of keeping two PDFs
on the Desktop, the links worth going back to live here, sorted by what they're actually
useful for. (Full APA citations are in the original PDFs; this keeps only the useful targets.)

## 📚 Worth revisiting, by purpose

### When I want SQL practice ideas
- **SQL Cheat Sheet** (Towards Data Science, J. Lee) — the course's recommended quick reference (the PDF version now lives inside my [sql-reference-guide](sql-reference-guide.md))
- **W3Schools SQL tutorial** — https://www.w3schools.com/sql/default.asp — free, interactive, good for 10-minute drills

### When I'm building dashboards (nyc-payroll-explorer!)
- **Real-world BI dashboard examples** — https://www.tableau.com/learn/articles/business-intelligence-dashboards-examples
- **Looker dashboard requirements-gathering worksheet** — a literal intake form for asking stakeholders what they need *before* building. This is the "requisition form" habit from payroll applied to dashboards.
- **Tableau Dashboard Showcase** — https://www.tableau.com/data-insights/dashboard-showcase
- **Tableau Public "Viz of the Day"** — https://public.tableau.com/app/discover/viz-of-the-day — daily inspiration
- **Tableau Filter Actions help** — how dashboard click-to-filter works

### When I need spreadsheet help fast
- **Google Sheets cheat sheet** — https://support.google.com/a/users/answer/9300022
- **Keyboard shortcuts:** [Sheets](https://support.google.com/docs/answer/181110) | [Excel](https://support.microsoft.com/en-us/office/keyboard-shortcuts-in-excel-1798d9d5-842a-42b8-9c99-9b7213f0040f)
- **Formula parse errors in Sheets** (Ben Collins) — https://www.benlcollins.com/spreadsheets/formula-parse-error/ — the "why is my formula broken" page
- **How to correct a #VALUE! error** (Microsoft) — the Excel equivalent
- **COUNTIF docs:** [Sheets](https://support.google.com/docs/answer/3093480?hl=en) | [Excel](https://support.microsoft.com/en-us/office/countif-function-e0de10c6-f885-4e71-abb4-1f464816df34)
- **Differences between Sheets and Excel** — https://support.google.com/a/users/answer/9331278?hl=en

### When I need a public dataset to practice on (Course 3)
- **Google Dataset Search** — https://datasetsearch.research.google.com — the Google of datasets
- **Google Cloud Public Datasets** + **BigQuery public data** — practice SQL on real data at scale
- **Kaggle datasets** — https://www.kaggle.com — plus the [Kaggle Progression System](https://www.kaggle.com/progression) for building an online presence
- **Data.gov / US Census Bureau** — open government data (payroll-adjacent: CPS Labor Force Statistics!)
- **Global Health Observatory (WHO)**, **NOAA Public Datasets**, **UNICEF State of the World's Children**, **Stanford Open Policing Project** — themed practice sets

### When I want data to flow in automatically (Course 3)
- **Google Sheets dynamic imports:** [IMPORTRANGE](https://support.google.com/docs/answer/3093340) (sheet→sheet), [IMPORTHTML](https://support.google.com/docs/answer/3093339) (tables from web pages), [IMPORTDATA](https://support.google.com/docs/answer/3093335) (CSV from a URL)
- These are the spreadsheet version of what pandas' read_sql/read_csv does in my flask app

### When I'm ready to network (Course 3, Module 5)
- **Data Elixir newsletter** — https://dataelixir.com
- **Meetup: data analytics** — https://www.meetup.com/topics/data-analytics/ — NYC is loaded with these
- **Women in Analytics** — https://www.womeninanalytics.com/about
- **KDnuggets lists:** [events](https://www.kdnuggets.com/meetings/index.html) | [societies & groups](https://www.kdnuggets.com/websites/societies.html)
- **Tableau Community** — https://community.tableau.com/s/ + the "How we do data" webinar series
- **Data Science Association** / **Digital Analytics Association** — free-membership professional orgs

### When I need the big-picture story (interviews!)
- **The Data Life Cycle** (Strategic Finance magazine — an *accounting* publication!) — https://sfmagazine.com/post-entry/july-2018-the-data-life-cycle/
- **Data-driven vs data-informed vs data-inspired** (Towards Data Science) — good vocabulary for interviews
- **PepsiCo's customer-first marketing / anticipating intent** (Think with Google) — a "data trials and triumphs" case study
- **The Quant Crunch** (IBM) — the report on demand for data skills in the job market
- **Anna Leach TEDx: "Beyond the numbers: A data analyst journey"** — https://www.youtube.com/watch?v=t2oOFs4WgI0
- **Why sketching ideas fixes team communication** (Jason Fried, Inc.) — stakeholder alignment
- **Occam's Razor blog** (Avinash Kaushik) — limitations of data / analytics thinking

### Open datasets to practice on
- **World Bank Open Data** — https://data.worldbank.org/
- **Kaggle** — https://www.kaggle.com/
- **World Happiness Report**, **Census Population & Housing State Data** — used in the Course 2 visualization lessons

## 💡 How I'll actually use this

- Pull the Looker requirements worksheet before adding the next feature to **nyc-payroll-explorer** — write down what question the dashboard answers first.
- The Strategic Finance data-life-cycle article is my bridge line: accounting publications already talk about data this way — "I'm not switching fields, I'm switching tools."
- Weekly habit: one W3Schools SQL drill + one Viz of the Day for chart ideas for **flask-analytics-app**.
