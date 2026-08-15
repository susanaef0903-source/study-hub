# Google Data Analytics — Course 2, Module 3: Spreadsheet Magic

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 3 readings

## 🎯 What this module is about (one sentence)

The spreadsheet as a professional analyst's tool: formulas vs. functions, cell references,
error messages and how to fix them, plus why context and a scope of work keep the analysis honest.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Formula** | A set of instructions you write yourself: `=B2+C2+D2` | The gross-to-net math you've typed into Excel a thousand times. |
| **Function** | A *preset* command: `=SUM(B2:E2)`, `=AVERAGE()`, `=MIN()`, `=MAX()`, `=COUNTIF()` | SUM across a pay register instead of adding cells one by one. You know these — now you know the official distinction. |
| **Cell reference / range** | A cell (`A2`) or block of cells (`B2:E4`) used in a formula | Pointing at "the OT hours column, rows 2 through 400" instead of retyping numbers. |
| **Relative vs. absolute reference** | `A2` shifts when copied; `$A$2` never moves; `$A2`/`A$2` are mixed (F4 toggles) | Locking the tax-rate cell with `$` so dragging the formula down 500 employee rows doesn't wander off the rate. Classic payroll workbook trick. |
| **Fill handle** | The little corner box/circle you drag to copy a formula down | How you extended a formula down the whole register. Excel = green square, Sheets = blue circle. |
| **Header (and freezing it)** | First row that labels each column — freeze it so it stays visible | Frozen header row on a 2,000-line payroll export. You already do this. |
| **Sorting vs. filtering** | Sorting rearranges into meaningful order; filtering shows only rows meeting criteria and hides the rest | Sort by last name for the audit binder; filter to just "terminated in Q3" for the COBRA list. |
| **Order of operations** | Parentheses control what calculates first: `=(B2+C2)/2` ≠ `=B2+C2/2` | Same reason you parenthesized (gross − pretax deductions) before applying a rate. |
| **Context** | The who/what/where/when/why/how that gives data meaning | A column of numbers labeled nothing could be hours, dollars, or headcount. Column headers, pay-period labels, and source notes ARE context. |
| **Scope of work (SOW)** | Agreed-upon outline of the tasks a project will perform | The engagement letter / project charter: deliverables, timeline, milestones, what's in and out of scope. |
| **Problem domain** | Every activity affecting or affected by the problem | For a payroll-errors analysis: timekeeping, HR data entry, approvals — the whole ecosystem, not just the paycheck. |
| **Open data** | Data available to the public | NYC Open Data — exactly where nyc-payroll-explorer's dataset comes from. |

### Spreadsheet errors decoded (memorize this table)
| Error | Meaning |
|---|---|
| **#DIV/0!** | Dividing by zero or a blank cell |
| **#ERROR!** | (Sheets only) parsing error — input can't be interpreted (e.g., missing comma between ranges) |
| **#N/A** | Formula can't find the data |
| **#NAME?** | Function name misspelled/unrecognized |
| **#NUM!** | Invalid numeric value for the calculation (e.g., DATEDIF with dates reversed) |
| **#REF!** | Referenced cell no longer valid (you deleted its column) |
| **#VALUE!** | General problem with formula or referenced cells — spaces, text, etc. |

Pro tip from the reading: conditional formatting with custom formula `=ISERROR(A1)` on the whole
sheet highlights every error cell at once.

### Error-prevention best practices
Filter to reduce clutter; freeze headers; `*` for multiply (never x); always start with `=`;
match every open parenthesis; keep a raw-data tab separate from your working tab.

## 🗣️ Teach it to a friend

A formula is math you write yourself; a function is a shortcut the spreadsheet ships with —
both start with `=`. Formulas point at cells, not numbers, so when a value changes everything
recalculates on its own. The one gotcha is that copied references *move with you* unless you pin
them with dollar signs: `=B2*$F$1` dragged down keeps multiplying by the same F1 rate. When the
sheet yells at you with a #-something error, it's telling you exactly what's wrong — #REF! means
you deleted something a formula needed, #DIV/0! means a blank or zero snuck into a denominator.
And none of the numbers mean anything without context: label the columns, note who collected
the data, when, and why — otherwise it's just digits.

## 🃏 Flashcards

**Q:** What's the difference between a formula and a function?
**A:** A formula is a set of instructions you write to perform a calculation; a function is a preset command that performs a specific task (SUM, AVERAGE, MIN, MAX, COUNTIF).

**Q:** What does `$A$2` do that `A2` doesn't?
**A:** It's an absolute reference — it stays pointed at A2 when the formula is copied elsewhere. `A2` is relative and shifts. (F4 toggles between them; `$A2`/`A$2` are mixed.)

**Q:** You see #REF! in a cell. What probably happened?
**A:** The formula references a cell that's no longer valid — commonly a column or row that was deleted.

**Q:** What causes #DIV/0! and what's the quick fix?
**A:** Dividing by zero or a blank cell; fill in the missing value (or guard the formula against blanks).

**Q:** Which error appears only in Google Sheets, and what does it mean?
**A:** #ERROR! — a parsing error; the input can't be interpreted (e.g., ranges not separated by a comma).

**Q:** What does COUNTIF do?
**A:** Counts the cells in a range that meet a condition, e.g. =COUNTIF(A1:A16, "7") — a function whose behavior depends on criteria you set.

**Q:** Sorting vs. filtering — what's the difference?
**A:** Sorting arranges all the data into a meaningful order; filtering shows only rows that meet criteria and hides the rest.

**Q:** What is a scope of work (SOW)?
**A:** An agreed-upon outline of the tasks to be performed during a project — deliverables, timeline, milestones.

**Q:** Name the six context questions that turn raw data into meaningful information.
**A:** Who (created/collected it), What (it impacts), Where (it came from), When (collected), Why (motivation), How (method).

## 💡 How I'll actually use this

- This module is my home turf — 20 years of payroll workbooks. The new part is the vocabulary: in interviews say "absolute references," "COUNTIF," and "raw-data tab vs. working tab" instead of "the dollar-sign trick."
- Write a one-page SOW for the next flask-analytics-app feature (deliverable, data source, timeline). It's résumé-ready evidence of structured project thinking.
- nyc-payroll-explorer already runs on *open data* — use that exact term; it's a glossary word employers recognize.
- Add the who/what/where/when/why/how context block to both projects' READMEs so anyone landing on the repo understands the dataset in ten seconds.
