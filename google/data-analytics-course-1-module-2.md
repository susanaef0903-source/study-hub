# Google Data Analytics — Course 1, Module 2: The Wonderful World of Data

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 2 readings

## 🎯 What this module is about (one sentence)

The data *life cycle* (how data is born, used, and retired), how it's different from the data
*analysis process*, and the core toolbox — spreadsheets, databases/SQL, and visualization tools.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data life cycle** | Plan → Capture → Manage → Analyze → Archive → Destroy: the whole life of a piece of data | An employee record's life: set up on hire, updated each pay run, used for reports, archived at termination, destroyed after the retention period. |
| **Plan (life cycle)** | Decide what data is needed, how it's managed, who's responsible | Designing the new-hire packet: what fields do we collect, who owns the file? |
| **Capture** | Collect data from various sources | Time clock punches, W-4s, direct deposit forms coming in. |
| **Manage** | Care for the data — where and how it's stored | The HRIS and the locked filing cabinet. |
| **Archive / Destroy** | Long-term storage of relevant data; secure removal when done | Document retention schedules — keep payroll records the required years, then shred. You've lived this compliance rule. |
| **Data analysis process (six phases)** | Ask → Prepare → Process → Analyze → Share → Act — how one *project* runs | A single audit engagement, versus the life cycle which is like the record-retention policy. **Don't mix them up — quiz favorite!** |
| **Database** | A collection of data stored in a computer system | The back end of your payroll system — the part the vendor never let you touch directly. |
| **Query / Query language / SQL** | A request for data from a database; SQL is the language you write it in | Instead of asking IT for a report and waiting three days, you write the report request yourself in SQL. |
| **Spreadsheet** | A digital worksheet | Excel. Twenty years of Excel. |
| **Formula vs. Function** | Formula = instructions you write to calculate (=A2*B2); Function = preset command (=SUM(A2:A10)) | Formula is your custom OT calc; function is the built-in SUM you use to tie out the register. |
| **Stakeholders** | People who invest time/resources in a project and care about its outcome | The CFO, HR director, and department heads waiting on your numbers. |
| **Visualization tools (Tableau, Looker)** | Software that turns numbers into charts and dashboards | The executive dashboard version of your monthly headcount report — drag-and-drop (Tableau) or wired straight to the database (Looker). |

### Spreadsheets vs. databases (know this table)

| Spreadsheets | Databases |
|---|---|
| Accessed through a software app | Accessed using a query language |
| Rows and columns, data in cells | Data organized by rules and relationships |
| Limited amount of data | Huge amounts of data |
| Manual data entry | Strict, consistent data entry |
| Generally one user at a time | Multiple users |
| Controlled by the user | Controlled by a database management system |

You don't pick one forever — analysts use both (query the database, export to a spreadsheet, or
graduate a too-big spreadsheet into a database).

### Life cycle variations (skim-level awareness)
Different industries reshuffle the stages: US Fish & Wildlife (Plan/Acquire/Maintain/Access/
Evaluate/Archive), USGS (adds Publish/Share), finance (Capture→Qualify→Transform→Utilize→
Report→Archive→**Purge** — finance explicitly purges, of course), Harvard (8 stages, ends at
Interpretation, never destroys). The universal principle: **govern data so it's accurate, secure,
and available.**

## 🗣️ Teach it to a friend

Think of data like an employee file. It has a whole life: you plan what goes in it, capture the
paperwork, manage and store it, use it for decisions, archive it when the person leaves, and
eventually shred it. That's the data life cycle. Separately, any one *project* using that data
follows the six analysis phases (ask through act) — a project is a trip; the life cycle is the
car's whole existence. For tools: a spreadsheet is a notebook you control yourself, great for
smaller jobs; a database is the office records room — much bigger, shared, with strict rules —
and SQL is how you ask the records room for exactly the file you need. Tableau and Looker turn
whatever you find into pictures executives can absorb in ten seconds.

## 🃏 Flashcards

**Q:** Name the six stages of the data life cycle, in order.
**A:** Plan, Capture, Manage, Analyze, Archive, Destroy.

**Q:** How is the data life cycle different from the data analysis process?
**A:** The life cycle (plan→destroy) is how data itself is managed over its lifetime; the analysis process (ask→act) is how an analyst runs one analysis project. They are not interchangeable.

**Q:** What is a query?
**A:** A request for data or information from a database.

**Q:** Spreadsheet vs. database: which supports multiple simultaneous users and huge amounts of data?
**A:** Database (spreadsheets are generally one user and limited data).

**Q:** What's the difference between a formula and a function in a spreadsheet?
**A:** A formula is a set of instructions you write to perform a calculation; a function is a preset command that performs a task automatically (like SUM).

**Q:** Who are stakeholders?
**A:** People who invest time and resources into a project and are interested in its outcome.

**Q:** What's the key feature difference between Tableau and Looker?
**A:** Tableau uses drag-and-drop to build interactive dashboards; Looker communicates directly with a database.

**Q:** What universal data-management principle applies no matter which life-cycle model a company uses?
**A:** Govern how data is handled so it is accurate, secure, and available.

## 💡 How I'll actually use this

- flask-analytics-app already demonstrates the spreadsheet→database graduation: CSV data loaded
  into SQLite, queried with SQL, charted for the "share" phase. That's this whole module in one repo.
- nyc-payroll-explorer's dataset is too big for comfortable Excel work — perfect interview example
  of *why* databases beat spreadsheets at scale.
- Retention schedules, secure storage, archive-then-destroy: I managed the payroll data life cycle
  for years under IRS/DOL rules. That's a governance talking point, not just a course concept.
- Watch for the quiz trap: life cycle stages vs. analysis phases share the word "analyze" but
  nothing else.
