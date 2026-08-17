# Google Data Analytics — Resource Library (Courses 1–5 official links)

**Platform:** Coursera (Google Data Analytics) | **Compiled:** Aug 2026 | **Source:** "Resources and citations" readings from Course 1 Module 4, Course 2 Module 4, Course 3 Module 5, Course 4 Module 6, and Course 5 Module 4

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

## 📚 Course 4 — Process Data from Dirty to Clean

*(from the Course 4 Module 6 "resources and citations" reading; sorted by what it's useful for)*

### When I need to size a sample or state a margin of error (Module 1)
- **Sample size calculators:** [SurveyMonkey](https://www.surveymonkey.com/mp/sample-size-calculator/) | [Raosoft](http://www.raosoft.com/samplesize.html) — inputs: population, confidence level, margin of error → minimum sample
- **Margin of error calculators:** [Good Calculators](https://goodcalculators.com/margin-of-error-calculator/) | [CheckMarket](https://www.checkmarket.com/sample-size-calculator/#sample-size-margin-of-error-calculator) — inputs: population, sample size, confidence level
- **Central Limit Theorem** (Investopedia) — https://www.investopedia.com/terms/c/central_limit_theorem.asp — why 30 is the floor
- **Sample size formula** (Statistics Solutions) — https://www.statisticssolutions.com/dissertation-resources/sample-size-calculation-and-sample-size-justification/sample-size-formula/
- **Power analysis, statistical significance & effect size** (MEERA, U. Michigan) — https://meera.snre.umich.edu/power-analysis-statistical-significance-effect-size

### When I need date math or lookups in a spreadsheet (Module 1)
- **VLOOKUP:** [Sheets](https://support.google.com/docs/answer/3093318?hl=en) | [Excel](https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1)
- **DATEDIF:** [Sheets](https://support.google.com/docs/answer/6055612?hl=en) | [Excel](https://support.microsoft.com/en-us/office/datedif-function-25dba1a4-2812-480b-84dd-8b32a451b35c) — service-date / eligibility math
- **DAYS360** (Excel) — https://support.microsoft.com/en-us/office/days360-function-b9a509fd-49ef-407e-94df-0cbda5718c2a — the 360-day accounting year, on purpose

### When I need proxy data or a practice dataset (Module 1)
- **Kaggle datasets** — https://www.kaggle.com/datasets — CSV, JSON, SQLite, BigQuery formats; screen for duplicates and Nulls first
- Course-mentioned Kaggle sets: credit card customers, trending YouTube videos, U.S. wildfire data, Google Analytics 360 sample

### When I need to explain why dirty data matters (Module 2 — interview ammo)
- **Dirty data: what is it costing you?** (DemandGen) — https://www.demandgen.com/dirty-data-what-is-it-costing-you/
- **Research finds obsolete or dirty data is widespread** (DQ Global) — https://www.dqglobal.com/blog/obsolete-or-dirty-data/
- **Hospitals battle duplicate medical records** (SearchHealthIT) — https://searchhealthit.techtarget.com/feature/Hospitals-battle-duplicate-medical-records-with-technology
- **Seizing opportunity in data quality** (MIT Sloan Management Review, T. Redman) — https://sloanreview.mit.edu/article/seizing-opportunity-in-data-quality/

### When I'm cleaning in a spreadsheet (Module 2)
- **10 Google Workspace tips to clean up data** — https://support.google.com/a/users/answer/9604139?hl=en
- **Top ten ways to clean your data** (Excel) — https://support.microsoft.com/en-us/office/top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19
- **Change the case of text in Excel** — https://support.microsoft.com/en-us/topic/change-the-case-of-text-in-excel-adc65f5b-958f-46a2-4d23-ab4d5faf48a8

### When I want to automate the cleaning (Module 2 — flask-analytics-app!)
- **Automating scientific data analysis with Python, part 1** (Towards Data Science, P. Grant) — https://towardsdatascience.com/automating-scientific-data-analysis-part-1-c9979cd0817e
- **Automating big-data analysis** (MIT News) — https://news.mit.edu/2016/automating-big-data-analysis-1021
- **10 of the best options for workflow automation software** (TechnologyAdvice) — https://technologyadvice.com/blog/information-technology/top-10-workflow-automation-software/

### When I'm picking or setting up a SQL environment (Module 3)
- **What is a SQL dialect, and which one should you learn?** (LearnSQL) — https://learnsql.com/blog/what-sql-dialect-to-learn/
- **SQL Server, PostgreSQL, MySQL... what's the difference?** (DataCamp) — https://www.datacamp.com/community/blog/sql-differences
- **SQL vs MySQL vs SQL Server** (Software Testing Help) — https://www.softwaretestinghelp.com/sql-vs-mysql-vs-sql-server/
- **What is SQL** (SQL Tutorial) — https://www.sqltutorial.org/what-is-sql/
- **SQLite window functions** — https://sqlite.org/windowfunctions.html — my flask app runs on SQLite, so this one is directly usable
- **BigQuery sandbox** — https://cloud.google.com/bigquery/docs/quickstarts/quickstart-cloud-console#about-bigquery-sandbox — free tier, no credit card
- **Automobile data set** (UCI ML Repository) — https://archive.ics.uci.edu/ml/datasets/Automobile — the "clean data using SQL" practice set
- **Stack Overflow** — https://stackoverflow.com/ — the course's official answer for debugging SQL

### When I'm verifying and documenting a clean (Module 4)
- **Sheets functions:** [IMPORTRANGE](https://support.google.com/docs/answer/3093340?hl=en) | [QUERY](https://support.google.com/docs/answer/3093343?hl=en) | [FILTER](https://support.google.com/docs/answer/3093197?hl=en) — pull, slice, and view data without editing the source
- **Paste links to source cells instead of values** (Professor Excel) — https://professor-excel.com/how-to-paste-cell-links/ — the Excel version of IMPORTRANGE
- **Markdown basic writing and formatting syntax** (GitHub Docs) — https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax — for the CHANGELOG.md in every repo

## 📚 Course 5 — Analyze Data to Answer Questions

*(from the Course 5 Module 4 "resources and citations" reading; sorted by what it's useful for)*

### When I'm setting up or refreshing a SQL environment (Module 1)
- **BigQuery sandbox** — https://cloud.google.com/bigquery/docs/quickstarts/quickstart-cloud-console#about-bigquery-sandbox — free tier; **BigQuery docs** — https://cloud.google.com/bigquery/docs
- Getting-started pages for MySQL, Microsoft SQL Server, PostgreSQL, and SQLite are all linked from the reading — SQLite is the one my flask app runs on

### When I need to sort/filter in a spreadsheet (Module 1)
- **Sheets:** [Sort & filter your data](https://support.google.com/docs/answer/3540681?co=GENIE.Platform%3DDesktop&hl=en) | [SORT function](https://support.google.com/docs/answer/3093150?hl=en) | [FILTER function](https://support.google.com/docs/answer/3093197?hl=en) | [Sort & filter video](https://www.youtube.com/watch?v=VcRBHXBMKBU)
- **Excel:** [Sort data in a range or table](https://support.microsoft.com/en-us/office/sort-data-in-a-range-or-table-62d0b95d-2a90-4610-a6ae-2e545c4a4654) | [SORT](https://support.microsoft.com/en-us/office/sort-function-22f63bd0-ccc8-492f-953d-c20e8e44b86c) | [SORTBY](https://support.microsoft.com/en-us/office/sortby-function-cd2d7a62-1b93-435c-b561-d6a35134f28f) | [FILTER](https://support.microsoft.com/en-us/office/filter-function-f4f7cb66-82eb-4767-8f7c-4877ad80c759) | [GCFLearnFree: sorting data video](https://www.youtube.com/watch?v=Ep5q1cUhQas)

### When I'm converting types or combining text (Module 2)
- **Text → number / date:** [Excel text→number (Ablebits)](https://www.ablebits.com/office-addins-blog/2018/07/18/excel-convert-text-to-number/) | [Excel text→date (Ablebits)](https://www.ablebits.com/office-addins-blog/2015/03/26/excel-convert-text-date/) | [Sheets date format (Ablebits)](https://www.ablebits.com/office-addins-blog/google-sheets-change-date-format/) | [Sheets text→numbers (Productivity Spot)](https://productivityspot.com/convert-text-to-numbers-google-sheets/)
- **Combine / split cells:** [Excel: combine text from two or more cells](https://support.microsoft.com/en-us/office/combine-text-from-two-or-more-cells-into-one-cell-81ba0946-ce78-42ed-b3c3-21340eb164a6) | [Sheets: split or combine text cells (TechRepublic)](https://www.techrepublic.com/article/how-to-split-or-combine-text-cells-with-google-sheets/)
- **Percentages:** [Excel: format numbers as percentages](https://support.microsoft.com/en-us/office/format-numbers-as-percentages-de49167b-d603-4450-bcaa-31fba6c7b6b4) | [Sheets TO_PERCENT](https://support.google.com/docs/answer/3094284?hl=en)
- **SQL CAST/type conversion:** [BigQuery conversion rules](https://cloud.google.com/bigquery/docs/reference/standard-sql/conversion_rules) | [CAST and CONVERT (T-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-ver15) | [MySQL cast functions](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html) | [SQL type casting (RudderStack)](https://www.rudderstack.com/guides/how-to-sql-type-casting/)
- **SQL strings:** [W3Schools SQL keywords reference](https://www.w3schools.com/sql/sql_ref_keywords.asp) | [CONCAT()](https://www.w3schools.com/sql/func_sqlserver_concat.asp) | [CONCAT_WS()](https://www.w3schools.com/sql/func_sqlserver_concat_ws.asp) | [SQL Server functions list](https://www.w3schools.com/sql/sql_ref_sqlserver.asp)

### When I want spreadsheet power-user tricks (Module 2)
- **Sheets:** [function list](https://support.google.com/docs/table/25273) | [keyboard shortcuts](https://support.google.com/docs/answer/181110) | [Ben Collins: 18 formula tips & techniques](https://www.benlcollins.com/spreadsheets/google-sheets-formulas-techniques/) | [20 Sheets formulas you must know (Automate.io)](https://automate.io/blog/google-spreadsheet-formulas/)
- **Excel:** [Exceljet 222 shortcuts](https://exceljet.net/keyboard-shortcuts) | [Exceljet 500 formula examples](https://exceljet.net/formulas) | [Exceljet function list](https://exceljet.net/excel-functions) | [11 advanced Excel skills (Learn to Code With Me)](https://learntocodewith.me/posts/excel-skills/)
- **Stack Overflow:** [home](https://stackoverflow.com/) | [how do I search?](https://stackoverflow.com/help/searching) | [tags](https://stackoverflow.com/tags) — the course's official debugging answer, again

### When I need JOIN / alias / subquery practice (Module 3 — interview prep!)
- **JOINs:** [W3Schools SQL Joins](https://www.w3schools.com/sql/sql_join.asp) (quick reminder) | [Essential SQL: SQL Joins – the ultimate guide](https://www.essentialsql.com/sql-joins/) (thorough) | [SQL Join types explained in visuals (Data School)](https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/) (Venn diagrams) | [SQL JOINs: bringing data together one join at a time (TDS)](https://towardsdatascience.com/sql-join-8212e3eb9fde) (has sample data to follow along) | [Dofactory SQL JOIN](https://www.dofactory.com/sql/join) (JOINs + aliasing)
- **Aliases:** [W3Schools SQL aliases](https://www.w3schools.com/sql/sql_alias.asp) | [SQL Tutorial: SQL alias](https://www.sqltutorial.org/sql-alias/) | [SAS: using column aliases](https://documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/sqlproc/p0aymxwsvbt5wcn1lncugwjtf758.htm)
- **Functions & subqueries:** [Mode: writing subqueries in SQL](https://mode.com/sql-tutorial/sql-sub-queries/) (interactive, with practice problems) | [w3resource: SQL subqueries](https://www.w3resource.com/sql/subqueries/understanding-sql-subqueries.php) | [W3Schools CASE](https://www.w3schools.com/sql/sql_case.asp) | [W3Schools MySQL IF()](https://www.w3schools.com/sql/func_mysql_if.asp) | [W3Schools HAVING (mirror)](http://www-db.deis.unibo.it/courses/TW/DOCS/w3schools/sql/sql_having.asp.html)
- **VLOOKUP:** [Excel VLOOKUP function (Microsoft)](https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1) | [Excel Campus VLOOKUP tutorial video](https://www.youtube.com/watch?v=d3BYVQ6xIE4) | [Exceljet: 23 things you should know about VLOOKUP](https://exceljet.net/things-you-should-know-about-vlookup) | [GCFGlobal: how to use VLOOKUP](https://edu.gcfglobal.org/en/excel-tips/how-to-use-excels-vlookup-function/1/) | [VLOOKUP in Excel vs Sheets (InfoInspired)](https://infoinspired.com/sheets-vs-excel-formula/vlookup-formula-in-excel-and-google-sheets/)
- **Pivot table (Excel):** [Create a PivotTable to analyze worksheet data](https://support.microsoft.com/en-us/office/create-a-pivottable-to-analyze-worksheet-data-a9a84538-bfe9-40a9-a8e9-f99134456576)

### When I need multi-condition formulas (Module 4)
- [Excel IFS function (Exceljet)](https://exceljet.net/excel-functions/excel-ifs-function) | [VLOOKUP with multiple criteria (Exceljet)](https://exceljet.net/formula/vlookup-with-multiple-criteria) | [INDEX and MATCH with multiple criteria (Exceljet)](https://exceljet.net/formula/index-and-match-with-multiple-criteria) | [Using IF with AND, OR, NOT (Microsoft)](https://support.microsoft.com/en-us/office/using-if-with-and-or-and-not-functions-d895f58c-b36c-419e-b1f2-5c193a236d97)

### When I'm building pivot tables (Module 4 — payroll register summaries)
- **Calculate:** Excel [Calculate values in a PivotTable](https://support.microsoft.com/en-us/office/calculate-values-in-a-pivottable-11f41417-da80-435c-a5c6-b0185e59da77) | [Exceljet calculated field example](https://exceljet.net/pivot-table/pivot-table-calculated-field-example) | [Power Spreadsheets: calculated fields step-by-step](https://powerspreadsheets.com/pivottable-calculated-fields/) — Sheets [Create & use pivot tables](https://support.google.com/docs/answer/1272900) | [InfoInspired: all about calculated fields](https://infoinspired.com/google-docs/spreadsheet/all-about-calculated-field-in-pivot-table-in-google-sheets/) | [Ben Collins: pivot tables in Sheets, beginner's guide](https://www.benlcollins.com/spreadsheets/pivot-tables-google-sheets/)
- **Sort:** Excel [Sort data in a PivotTable or PivotChart](https://support.microsoft.com/en-us/office/sort-data-in-a-pivottable-or-pivotchart-e41f7107-b92d-44ef-861f-24430830450a) | [Tutorials Point: sorting data](https://www.tutorialspoint.com/excel_pivot_tables/excel_pivot_tables_sorting_data.htm) | [Exceljet: sort a pivot table by value](https://exceljet.net/lessons/how-to-sort-a-pivot-table-by-value) — Sheets [Customize a pivot table](https://support.google.com/docs/answer/7572895) | [InfoInspired: sort pivot columns in custom order](https://infoinspired.com/google-docs/spreadsheet/pivot-table-columns-in-custom-order-in-google-sheets/) | [1-minute ascending/descending guide (Medium)](https://medium.com/actiondesk/pivot-table-ascending-descending-order-in-google-sheets-and-excel-1-minute-ultimate-beginners-8f9f4c560492)
- **Filter:** Excel [Filter data in a PivotTable](https://support.microsoft.com/en-us/office/filter-data-in-a-pivottable-cc1ed287-3a97-4e95-b377-ddfafe79fa8f) | [For Dummies: filter Excel pivot table data](https://www.dummies.com/article/technology/software/microsoft-products/excel/how-to-filter-excel-pivot-table-data-152376) — Sheets [InfoInspired: filter multiple values](https://infoinspired.com/google-docs/spreadsheet/filter-multiple-values-in-pivot-table-sheets/)
- **Format:** Excel [Design the layout and format of a PivotTable](https://support.microsoft.com/en-us/office/design-the-layout-and-format-of-a-pivottable-a9600265-95bf-4900-868e-641133c05a80) — Sheets [Create and edit pivot tables (group data)](https://support.google.com/a/users/answer/9308944#group_data_in_a_pivot_table)

### When I'm working with temporary tables (Module 4 — flask-analytics-app scratch tables)
- [BigQuery DDL: temporary tables](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#temporary_tables) | [BigQuery "temp tables" via WITH (Pascal Landau)](https://www.pascallandau.com/bigquery-snippets/use-temporary-tables-with-named-subquery/) | [Intro to temporary tables in SQL Server ({coding}Sight)](https://codingsight.com/introduction-to-temporary-tables-in-sql-server/) | [SQL Server temporary tables (SQLServerTutorial.net)](https://www.sqlservertutorial.net/sql-server-basics/sql-server-temporary-tables/) | [Table variables vs temporary tables (Redgate)](https://www.red-gate.com/hub/product-learning/sql-prompt/choosing-table-variables-temporary-tables)

### When I need a practice dataset for calculations (Module 4)
- **Avocado prices** (Justin Kiggins, Kaggle, ODbL) — https://www.kaggle.com/neuromusic/avocado-prices — the module's calculation dataset; **Kaggle datasets** — https://www.kaggle.com/datasets
- [BigQuery: introduction to loading data](https://cloud.google.com/bigquery/docs/loading-data) — how to get a CSV into BigQuery
- **Connected Sheets** (BigQuery data inside Google Sheets) — the reading links Google's "Get started with BigQuery data in Google Sheets" and the product announcement; pivot on millions of rows without exporting

## 💡 How I'll actually use this

- Pull the Looker requirements worksheet before adding the next feature to **nyc-payroll-explorer** — write down what question the dashboard answers first.
- The Strategic Finance data-life-cycle article is my bridge line: accounting publications already talk about data this way — "I'm not switching fields, I'm switching tools."
- Weekly habit: one W3Schools SQL drill + one Viz of the Day for chart ideas for **flask-analytics-app**.
- Course 4 add: start a `CHANGELOG.md` (Markdown syntax link above) in **nyc-payroll-explorer** and **flask-analytics-app**, and use the SQLite window-functions page the next time I need a running total or rank in the flask app.
- Course 5 add: work through the Mode subquery tutorial and the Data School JOIN visuals before any SQL interview — those two plus the timesheet-to-master story are my JOIN answer. Bookmark the pivot "Sort" links for the next payroll-style summary; bookmark the Pascal Landau `WITH` article for the flask app's scratch tables.
