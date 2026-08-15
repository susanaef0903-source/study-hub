# Google Data Analytics — Course 4, Module 1: Data Integrity & The Importance of Integrity

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 1 readings

> *(guide grows as more module 1 readings are added)*

## 🎯 What this module is about (one sentence)

Before you analyze anything, you have to be able to trust the data — this module covers how
data integrity gets broken (and protected), how to check that your data actually answers the
business question, and what to do when the data is missing, thin, or wrong.

**Sue's note:** this module is your home turf. Data integrity is what you've been doing for 20
years under other names: reconciliations, certified payroll reports, audit prep. Different
vocabulary, same discipline.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data integrity** | The accuracy, completeness, consistency, and trustworthiness of data throughout its lifecycle | Why a certified payroll report can be certified at all: every number traces back, nothing's missing, nothing was altered on the way. |
| **Data replication** (integrity risk) | Copying data creates versions — a partial or stale copy can get treated as the real thing | Two copies of the payroll register floating around, and someone reconciles against the outdated one. Which version is the version of record? |
| **Data transfer** (integrity risk) | Moving data between systems can silently corrupt it (e.g., dates imported as text) | Every payroll conversion you've lived through: the 401(k) file loads, but SSNs lost their leading zeros. The transfer "worked" — and broke the data. |
| **Data manipulation** (integrity risk) | Editing data can introduce errors — like deleting a "duplicate" that was actually unique | Deleting what looks like a duplicate paycheck that was really a legitimate second check (bonus run + regular run, same employee, same date). |
| **Data constraint** | A rule that determines whether a value is valid (type, range, mandatory, unique, pattern...) | Payroll system edits: SSN must be 9 digits, pay rate can't be negative, deduction codes must come from the approved list. You've set these up. |
| **Cross-field validation** | Multiple fields must satisfy a condition together | Gross − taxes − deductions must equal net. If the pieces don't add to the total, something's wrong. The oldest payroll check there is. |
| **Accuracy / Completeness / Consistency** | Data matches reality / nothing's missing / it's the same at every point of entry | The three questions of every reconciliation: Are the numbers right? Is every employee in the file? Does HR's record match payroll's record? |
| **Well-aligned objective** | The data you have can actually answer the business question being asked | Being asked "what's our overtime cost trend?" and having only current-quarter data. You'd flag that mismatch before reporting — that's alignment judgment. |
| **Proxy data** | Substitute data used when the real data doesn't exist yet | Budgeting next year's benefits cost using this year's rates plus a trend factor — a stand-in until the real renewal numbers arrive. |
| **Population vs. sample** | The whole group you care about vs. the subset you actually measure | A full payroll audit checks every check (population); a DOL or 401(k) audit tests a pulled sample of employees and trusts it represents the rest. |
| **Margin of error** | How far the sample's result may differ from the true population result | The auditor's tolerance: sample testing found no errors, so the population error rate is likely within ± some small range. |
| **Confidence level** | How often you'd get similar results if you re-ran the survey (95% is standard) | How much you trust a spot-check: "if we pulled 30 different files 100 times, we'd reach the same conclusion 95 times." |
| **Confidence interval** | Sample result ± margin of error = range where the true answer likely sits | "Average OT is 4.2 hrs/week, give or take 0.5" — you report the range, not false precision. |
| **Statistical significance** | Whether a result is real or just random chance | Is this quarter's overtime spike a real trend, or just two people covering a vacation? You've made that judgment call — stats formalizes it. |

### The three ways integrity gets compromised (exam favorite!)
1. **Replication** — copying creates conflicting versions → *two payroll registers, which is current?*
2. **Transfer** — moving between systems corrupts data → *dates become text, SSNs lose zeros*
3. **Manipulation** — editing introduces errors → *deleting a "duplicate" that was real*

### The data-issue decision tree (from the reading)
- **Data has errors?** → Can you fix it or get a corrected dataset? Do that. If not, can you omit the wrong data and still have enough? Analyze without it.
- **Not enough data?** → Can you use proxy data? Use it (most common workaround). Can you collect more? Do a preliminary analysis now, finish after collecting. Neither? Modify the business objective.
- **Wrong data because requirements were misunderstood?** → Restate the requirements — communicate.
- ⚠️ Errors in data can be a warning sign the whole source isn't reliable. Use judgment — same instinct as an audit red flag.

### Sample size rules of thumb
- **Never below 30** (Central Limit Theorem: 30 is the smallest sample whose average starts representing the population's average)
- **95% confidence level** is the standard; 90% works in some cases
- Want **higher confidence**, **smaller margin of error**, or **more significance**? → **larger sample**
- Bigger samples cost more — stakes decide: drug safety needs a big sample; "do residents like the new library?" doesn't. (Payroll version: a wage-theft investigation samples deep; a survey about the new timesheet UI doesn't.)

### Date formats: the classic integrity trap
12/10/20 is **October 12** in DD/MM/YY countries and **December 10** in the US (MM/DD/YY).
A global dataset with mixed formats = quietly broken analysis. Always confirm the format
before trusting a date column — like confirming whether a pay period is check date or period-end date.

## 🗣️ Teach it to a friend

Data integrity means the data is accurate, complete, consistent, and trustworthy — think of a
payroll register you'd be willing to certify and sign. Integrity gets broken three main ways:
copying data (now there are two versions and one is stale), transferring data between systems
(dates turn into text, leading zeros vanish), and hand-editing data (someone deletes a
"duplicate" that was actually real). Before analyzing, you also check *alignment* — does this
data actually answer the question being asked, the way you'd never answer an overtime question
with a file that's missing half the year. And when data is missing or thin, you either
substitute proxy data, collect more, sample properly (never fewer than 30, aim for 95%
confidence), or — last resort — renegotiate the question. It's a reconciliation mindset applied
to every dataset.

## 🃏 Flashcards

**Q:** What are the three main ways data integrity can be compromised?
**A:** Replication (conflicting copies), transfer (corruption moving between systems), and manipulation (errors introduced by editing).

**Q:** What is a data constraint? Give two examples.
**A:** A criterion that determines whether a value is valid — e.g., data type (must be a date), data range (10–20), mandatory (can't be blank), unique (no duplicates), regex pattern (###-###-####).

**Q:** What is cross-field validation?
**A:** A check where multiple fields must satisfy a condition together — e.g., percentages across fields must add up to 100% (or gross − deductions = net).

**Q:** What is proxy data and when do you use it?
**A:** Substitute data standing in for data you don't have — the most common workaround when there's no time to collect real data (e.g., use a similar city's commuter data).

**Q:** You have too little data. Name two options.
**A:** Combine proxy data with the actual data, or adjust the analysis to fit what you have and state the limitation in the report.

**Q:** What's the minimum recommended sample size, and why?
**A:** 30 — per the Central Limit Theorem, it's the smallest sample size where the sample average starts to represent the population average.

**Q:** Define margin of error and confidence interval.
**A:** Margin of error = how much the sample result may differ from the true population result. Confidence interval = sample result ± margin of error (the range the truth likely falls in).

**Q:** Data only partially aligns with the business objective. What are your options?
**A:** Modify the objective, or add data constraints so the subset of data that remains aligns with the objective (e.g., limit to students with consistent weekly sessions).

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** run integrity checks on the NYC payroll dataset before charting — date format consistency, negative pay rates, duplicate employee rows, cross-field check (base + OT pay behaving sensibly). Write the checks as documented steps, like an audit workpaper.
- **flask-analytics-app:** add simple data constraints on input (type, range, mandatory) so bad rows are rejected at entry instead of cleaned later — cheaper to prevent than to fix, same as payroll edits.
- **Spreadsheet skills from this module:** VLOOKUP and DATEDIF for the activation-to-first-use pattern — the same lookup-and-date-math I did constantly for service-date and eligibility calculations. DAYS360 even exists specifically for 360-day accounting years.
- **Interview line:** "I've enforced data integrity for 20 years — certified payroll reports, DOL audits, benefit reconciliations. Replication, transfer, and manipulation risks are just new names for version control on the payroll register, conversion file errors, and unauthorized journal edits."
