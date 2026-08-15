# Google Data Analytics — Course 2, Module 2: Make Data-Driven Decisions

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 2 readings

## 🎯 What this module is about (one sentence)

How data actually feeds decisions — data-driven vs. data-inspired, quantitative vs. qualitative,
big vs. small data — and how to package it for people via reports and dashboards.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data-driven decision** | The data alone drives the call (like an A/B test winner) | Choosing a pay schedule because the error-rate numbers clearly say biweekly beats semi-monthly. |
| **Data-inspired decision** | Data plus experience, feelings, and harder-to-measure context | Picking a new payroll vendor: you look at the cost numbers AND what your team says about the demo. The numbers alone don't decide. |
| **Quantitative data** | Objective, measurable — numbers, quantities, ranges | Gross pay, headcount, OT hours. The *what*. |
| **Qualitative data** | Subjective, descriptive — qualities and characteristics | Exit-interview comments, open-ended survey answers. The *why*. |
| **Metric** | A single quantifiable type of data used for measurement | Cost-per-hire, error rate per pay run, days-to-close — you've tracked metrics your whole career. |
| **ROI** | Profit vs. investment — was it worth the money? | Same ROI you calculated to justify new HRIS software: (savings − cost) ÷ cost. |
| **Report** | A static snapshot of data given to stakeholders periodically | The monthly payroll register you emailed leadership. Fixed as of a date. |
| **Dashboard** | A tool that monitors *live, incoming* data | If the payroll register updated itself in real time and execs could filter it — that's a dashboard. |
| **Pivot table** | Summarization tool that sorts, groups, counts, totals, averages | You've built these in Excel: sum wages by department by quarter. Same term, same tool. |
| **Big data** | Large, complex datasets over long periods; lives in databases, gets queried | The state's entire unemployment-insurance wage file. Too big for Excel. |
| **Small data** | Specific metrics over a short, well-defined period; fine in a spreadsheet | One quarter's 941 reconciliation workbook. |
| **Algorithm** | A process or set of rules followed for a specific task | The steps your payroll system runs to compute withholding — written rules, executed the same way every time. |

### Data-driven horror stories (know these examples)
- **New Coke (1985):** 200,000 taste tests said people preferred it — but the data was *incomplete*
  (it never asked how people felt about classic Coke disappearing). Data-driven ≠ safe if the data misses the point.
- **Mars Climate Orbiter (1999):** $125M lost because one team used pounds and the other newtons.
  The data was 100% accurate — the *interpretation/assumptions* were wrong. (Payroll version: one file in hours, one in decimal days. Always confirm units.)
- **PepsiCo (triumph):** centralized data in one cloud hub + external sources = data-inspired win.

### The four Vs of big data
**Volume** (how much), **Variety** (what kinds), **Velocity** (how fast it's processed), and the
sometimes-fourth **Veracity** (quality and reliability).

### Report vs. dashboard (exam favorite)
Report = static, periodic. Dashboard = live, self-updating. And a dashboard only auto-updates
if the *data structure stays the same* — change the structure, and you must redesign the dashboard first.

### Dashboard-building process
1. Identify stakeholders and how they'll use it → 2. Design (clear header, short descriptions,
most important info at top) → 3. Optional mockups → 4. Pick visualizations to fit the story
(line/bar for change over time, pie/donut for parts of a whole) → 5. Add filters.

## 🗣️ Teach it to a friend

Numbers tell you *what* happened; words tell you *why*. A data-driven decision follows the numbers
directly — great when the data is complete, dangerous when it isn't (ask Coca-Cola). A data-inspired
decision uses the same numbers but leaves room for experience and things that are hard to measure.
Once you've decided what to track, a report is a printed snapshot and a dashboard is a live window —
the dashboard saves everyone time because it updates itself, as long as nobody changes the shape
of the data underneath it. And "big data" just means data too large and messy for a spreadsheet,
judged by the Vs: volume, variety, velocity, veracity.

## 🃏 Flashcards

**Q:** What's the difference between data-driven and data-inspired decision-making?
**A:** Data-driven uses data alone to arrive at the decision; data-inspired also weighs experiences, feelings, and hard-to-measure qualities alongside the data.

**Q:** Quantitative vs. qualitative — which gives the "what" and which gives the "why"?
**A:** Quantitative = the what (objective numbers); qualitative = the why (subjective descriptions).

**Q:** What's the difference between a report and a dashboard?
**A:** A report is a static collection of data given periodically; a dashboard monitors live, incoming data.

**Q:** When does a dashboard stop auto-updating with new data?
**A:** When the data *structure* changes — the dashboard design must be updated before live data flows again.

**Q:** What went wrong with the New Coke launch, in data terms?
**A:** The decision was data-driven but the data was incomplete — it never measured how customers felt about replacing classic Coke.

**Q:** What lesson does the Mars Climate Orbiter teach analysts?
**A:** Accurate data can still produce wrong decisions if teams interpret it with different assumptions (pounds vs. newtons) — communicate and confirm units/definitions.

**Q:** Name the four Vs of big data.
**A:** Volume, Variety, Velocity, Veracity (quality/reliability — the "sometimes fourth" V).

**Q:** What is a pivot table?
**A:** A data summarization tool used to sort, reorganize, group, count, total, or average data.

## 💡 How I'll actually use this

- nyc-payroll-explorer IS a dashboard in this vocabulary: live filters over a big public dataset. In interviews, describe it that way — "I built a dashboard over ~5M rows of NYC payroll data; a spreadsheet couldn't hold it, so it lives in a database and gets queried."
- flask-analytics-app charts = reports vs. dashboard distinction: static rendered charts are reports; add filter controls and they become dashboard views.
- Steal the dashboard design tips directly: clear header, one-line description under each chart, most important number at the top.
- Interview line: "Payroll taught me the Mars Orbiter lesson early — a file in hours read as dollars will wreck a pay run. Verifying units and definitions is second nature."
