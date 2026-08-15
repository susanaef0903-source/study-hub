# Google Data Analytics — Course 2, Module 4: Always Remember the Stakeholder

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 4 readings

## 🎯 What this module is about (one sentence)

The people side of analytics: knowing your stakeholders, communicating for your audience,
being honest about what the data can't say, and running meetings people don't dread.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Stakeholders** | People who invested time, interest, and resources in your project | Everyone who ever waited on your payroll numbers: CFO, department heads, auditors, employees. |
| **Executive team** | High-level strategy folks; want the headline first, details in an appendix | Presenting to the CFO: lead with "payroll costs up 4%, driven by OT in two departments" — not with the reconciliation steps. |
| **Customer-facing team** | Interacts with customers; may come with specific asks — let the data tell the story, not their hopes | Like a manager pushing you to "show" their department is understaffed. Report what the hours data actually says. |
| **Data science team** | Analysts, scientists, engineers you collaborate with | Like splitting year-end: you take W-2s, a colleague takes 1099s, then you reconcile — divided analysis, shared story. |
| **Illusion of agreement** | Everyone *thinks* they agree, but each pictured something different | "Run me a comp report" — you deliver base pay, they wanted total rewards. Kill it early with a quick sketch/description before building. |
| **Change-log** | Chronological file listing modifications made to a project | The amendment history on a payroll run, or an audit trail — a running record of what changed and when. |
| **The four audience questions** | Who is my audience? What do they know? What do they need to know? How do I best communicate it? | You already switch registers between explaining a garnishment to an employee vs. the DOL. Same skill, now formalized. |
| **Limitations of data** | Incomplete, misaligned, or dirty data can mislead — say so up front | "Certification records only go back two years" = "our timekeeping system only has data since the 2019 conversion." Disclose it. |
| **Misaligned data** | Teams measure the same metric with different business rules | One department counts headcount including temps, another doesn't — so "headcount" never matches. Standardize definitions early. |
| **Dirty data** | Data with errors: incorrect, duplicated, corrupted, incomplete | Duplicate employee records after an HRIS migration. Clean before analyzing, and track the fixes you make. |
| **Reframing** | Restating a problem, then redirecting it toward a resolution | "Payroll is always late" → "How do we move timesheet approval earlier so payroll starts sooner?" |
| **Turnover rate** | The rate at which employees voluntarily leave | Your bread and butter — you've computed this for HR dashboards for years. |

### Data storytelling best practices (Avinash Kaushik's list — quiz bait)
1. **Compare the same types of data** — don't mix metrics in one chart.
2. **Visualize with care** — start the Y-axis at 0; a 0.01% drop looks huge if you zoom in.
3. **Leave out needless graphs** — if a table tells it at a glance, use the table.
4. **Test for statistical significance** — looking different isn't the same as being different.
5. **Pay attention to sample size** — small samples let a few oddballs skew everything.

### Working with stakeholders — the five habits
Discuss goals · feel empowered to say "no" (with context) · plan for the unexpected ·
know your project · start with words AND visuals · communicate often.

### Lead great meetings
**Before:** set the objective, organize/visualize the data, send an agenda ahead of time
(start/end time, location, objectives, pre-reads). **During:** intros, present the data, discuss
observations → interpretations → implications, take notes, summarize next steps. **After:**
send a recap with next steps, distribute notes, ask for feedback.

## 🗣️ Teach it to a friend

An analyst's findings only matter if the right people understand and trust them. So before you
open a spreadsheet, figure out who you're serving: executives want the answer first and the math
in an appendix; frontline teams want their hypothesis confirmed — and your job is to report what
the data says, not what they hoped. Before communicating anything, ask four questions: who's my
audience, what do they know, what do they need to know, how do I best deliver it? Show a quick
sketch early so everyone's picturing the same deliverable — most project churn comes from the
illusion of agreement. And always name your data's limitations out loud: incomplete history,
teams that define the metric differently, uncleaned errors. Saying "here's what this data can't
tell us" builds more trust than pretending it's perfect.

## 🃏 Flashcards

**Q:** Name the three common stakeholder groups a data analyst works with.
**A:** The executive team, the customer-facing team, and the data science team.

**Q:** How should you present to executives?
**A:** Lead with the headline answers to their questions; keep details in an appendix or project docs — their time is limited.

**Q:** What is the "illusion of agreement" and how do you prevent it?
**A:** When people assume they're aligned but each interpreted the plan differently; prevent it by starting with a description AND a quick visual of what you're building.

**Q:** What is a change-log?
**A:** A file containing a chronologically ordered list of modifications made to a project.

**Q:** What are the four audience questions to answer before communicating?
**A:** Who is your audience? What do they already know? What do they need to know? How can you best communicate it?

**Q:** What should you do when your dataset is incomplete?
**A:** You can still use it, but be up front about the limits of the analysis (and look for an alternate source to fill the gap).

**Q:** Why should a chart's Y-axis usually start at 0?
**A:** Zooming in exaggerates tiny changes — a 0.01% drop can look like a cliff. Y-axis at 0 shows the honest scale.

**Q:** What belongs in a meeting agenda?
**A:** Start/end time, location (incl. remote info), objectives, and background material/data to review beforehand — shared ahead of time.

**Q:** What is reframing?
**A:** Restating a problem or challenge, then redirecting it toward a potential resolution.

## 💡 How I'll actually use this

- This module is my strongest interview material: 20 years of managing stakeholders (CFOs, auditors, DOL, anxious employees) IS this skill set. Line to use: "I've spent two decades translating the same payroll numbers for executives, regulators, and employees — the four audience questions were my daily routine before I knew data analytics named them."
- Apply Kaushik's rules to every chart in flask-analytics-app and nyc-payroll-explorer: Y-axis at 0, no needless graphs, one metric type per chart. Do a quick audit pass this week.
- Add a CHANGELOG.md to both repos — it's the course's own recommended tool and it makes the projects look professionally maintained.
- Add a "Limitations of the data" section to nyc-payroll-explorer's README (NYC payroll data quirks: agency naming inconsistencies, fiscal-year boundaries, missing hourly rates for some titles). Disclosing limits reads as senior-level judgment.
