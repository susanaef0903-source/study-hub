# Google Data Analytics — Course 4, Module 4: Verify and Report on Cleaning Results

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 4 readings (verification step-by-step, verification checklist, embrace changelogs, advanced functions, glossary)

## 🎯 What this module is about (one sentence)

Cleaning data isn't finished when you stop editing — it's finished when you've **verified** the
cleaning worked, **documented** every change you made (the changelog), and **reported** the
result so someone else can trust it; plus a few spreadsheet functions (IMPORTRANGE, QUERY,
FILTER) that speed the cleaning up.

**Sue's note:** this is the audit sign-off module. Verification is the tick-and-tie before you
certify. The changelog is the adjustment log you kept every payroll cycle: what changed, when,
who, why, who approved. Google is teaching a discipline you already practice — the only new
part is the tooling (pivot tables for anomaly counts, SQL CASE, version control).

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll / audit translation |
|---|---|---|
| **Verification** | A process to confirm that a data-cleaning effort was well executed and the resulting data is accurate and reliable | Audit sign-off. You don't certify the payroll register because you *ran* the process — you certify it because you *checked* the output ties out. |
| **Changelog** | A file containing a chronologically ordered list of modifications made to a project — what changed, when, who, who approved, version, and *why* | The adjustment log / journal-entry support binder. Every manual check, every rate override, every retro adjustment had a note: date, reason, initials, approver. Same thing. |
| **Version history (automated)** | Built-in tracking (Sheets edit history, Excel Track Changes, BigQuery history) that records *what* changed — but not *why* | The system audit trail. It shows the field went from 40 to 42 hours and who did it — but not that the supervisor emailed a corrected timesheet. The "why" lives in your notes. |
| **Find and replace** | A tool that finds a specified search term and replaces it with something else (fix every "Plos" → "Plus" at once) | Global correction of a mis-keyed vendor or department name across a whole file — the fast way, but you spot-check that it didn't hit something it shouldn't have. |
| **COUNTA** | A spreadsheet function that counts the total number of values (text or numbers) within a range | Head-count check: how many rows actually have an entry, blanks excluded. |
| **COUNT vs COUNTA** | COUNT counts only numeric cells; COUNTA counts anything non-blank | If you COUNT a name column you get zero — the classic "why is my pivot empty" moment. Use COUNTA for text like supplier or employee names. |
| **Pivot table for verification** | Group by a text column and COUNTA it → every spelling variant shows up as its own row with a count | Listing pay codes with a count of each — the one-off "OT " with a trailing space or "Overtme" jumps out immediately. Frequency check as an audit tool. |
| **CASE (SQL)** | A SQL statement that returns records that meet conditions by including an if/then statement in a query — WHEN x THEN y ELSE keep END | The rule sheet: "if the code says TNOY, treat as TONY, otherwise leave it." Note: CASE fixes the *displayed* result, not the underlying table. Like a report-level reclass vs. a posted correction. |
| **IMPORTRANGE** (Sheets) / **Paste Link** (Excel) | Pull a range from another spreadsheet, kept in sync with the source; you cherry-pick only the columns you need | Linking the GL summary tab to the payroll register instead of pasting values — when the register updates, the summary follows. No stale copies. |
| **QUERY** (Sheets) | SQL-like SELECT/WHERE inside a spreadsheet; can be combined with SUM/COUNT; can build multiple "views" (tabs) of one dataset without touching the original | Building the by-department and by-month tabs from one raw register without ever editing the raw data — the "leave the source alone" rule. |
| **FILTER** (Sheets) | Show only rows/columns meeting conditions; fully internal (no query language), often faster than QUERY, but can't be combined with SUM/COUNT the way QUERY can | Quick filter to isolate one department's rows for review — good for looking, not for summarizing. |
| **Version control system** | Company-wide repository of official queries; you *sync*, change, get a *code review*, *commit* with a comment, and can *revert* | Controlled documents. The official payroll calc query is like the approved rate table — you don't edit it in place, you check out, change, get approval, and the change is dated and reversible. |
| **Code review** | Someone (formally or informally) checks your change before it's committed | Second-set-of-eyes review before a payroll run is released. |
| **Business logic check** | Does the cleaned data make sense given what you know about the business? | The gut check after everything ties: 3,000 hours in a biweekly pay period does not pass, no matter how clean the formatting is. |

### The verification checklist (from the reading — exam favorite!)
Did you check for and correct:
1. **Sources of errors** — used the right tools/functions to find where errors come from?
2. **Null data** — searched with conditional formatting and filters?
3. **Misspelled words** — located them all?
4. **Mistyped numbers** — double-checked numeric data?
5. **Extra spaces and characters** — removed with **TRIM**?
6. **Duplicates** — removed with **Remove Duplicates** (spreadsheet) or **DISTINCT** (SQL)?
7. **Mismatched data types** — numeric, date, and string typecast correctly?
8. **Messy (inconsistent) strings** — consistent and meaningful?
9. **Messy (inconsistent) date formats** — dates formatted the same throughout?
10. **Misleading variable labels (columns)** — columns named meaningfully?
11. **Truncated data** — anything cut off or missing that needs correction?
12. **Business logic** — data makes sense given your knowledge of the business?

Then **review the goal** (a continuous loop): confirm the business problem → confirm the goal
of the project → verify the data can solve the problem and is aligned to the goal.
No one-size-fits-all checklist exists — every project adds its own items, and you revisit
the list as more data or better understanding arrives.

### The verification walkthrough (step-by-step reading)
- **Spreadsheet, method 1 — Find and Replace:** Edit → Find and replace → Find "Plos", Replace with "Plus" → Replace all. Fast, global.
- **Spreadsheet, method 2 — pivot table:** select the Suppliers column → Insert → Pivot table (new sheet) → Rows: Suppliers, Values: Suppliers summarized by **COUNTA** → every variant appears with a count → fix the one-offs by hand. **Don't use COUNT** — it only counts numbers.
- **SQL — CASE statement:**
  ```sql
  SELECT
    customer_id,
    CASE
      WHEN first_name = 'Tnoy' THEN 'Tony'
      ELSE first_name
    END AS cleaned_name
  FROM project-id.customer_data.customer_name
  ```
  Corrects the *display* in a new column `cleaned_name`; the underlying table is unchanged. (Drop the WHERE clause — you're not filtering, you're cleaning every row.)

### What a changelog records (from "Embrace changelogs")
- The data, file, formula, query, or other component that changed
- Description of what changed
- Date of the change
- Person who made the change
- Person who approved the change
- Version number
- **Reason for the change** ← the part automated version history can't give you

Why the *why* matters: you copied a formula from another report to stay consistent; later that
report turns out to be wrong. Version history lets you undo. The changelog tells you *who to go
tell* that their formula is wrong — integrity outside your project, and it shows you're someone
who can be trusted with data. Also: with a changelog you can undo change #2 of 4 without losing
#3 and #4 — imagine that with hundreds of changes.

No set format — a blank doc works — but on a shared changelog, agree the entry format with the
team first. Engineers do the same thing with **engineering change orders (ECOs)**; writers with
**document revision histories**.

### Where automated history lives
| Tool | How |
|---|---|
| Google Sheets | Right-click cell → **Show edit history** → < > arrows to walk back and forth |
| Microsoft Excel | If Track Changes is on: Review → Track Changes → **Accept/Reject Changes** |
| BigQuery | Bring up a previous version (without reverting) and compare to current |

### The version-control workflow for shared SQL (bonus tip — 8 steps)
1. Official queries live in the company's **version control system**
2. **Sync** — make sure you're editing the latest version
3. Make the change
4. **Code review** — formal or as informal as asking a senior analyst to look
5. **Commit** the updated query to the repository, with a comment saying *what* and *why* (e.g., "Updated revenue to include revenue from the new product, Calypso")
6. Once submitted, everyone gets it when they sync
7. Problem or business change? Look at the chronological change list, find yours, **revert**
8. Everyone sees the reverted query too

*Sue's note:* this is literally what `git commit -m` and `git push` do in your study-hub and
project repos. You've been running a version control system for weeks.

### Advanced functions cheat sheet
| Function | Sheets syntax | Excel equivalent | Use it for |
|---|---|---|---|
| IMPORTRANGE | `=IMPORTRANGE("spreadsheet_url", "Sheet!A1:C10")` | Paste Link (copy first, then Paste Special → Paste Link) | Pull data from another sheet, auto-updated; must click **Allow access** the first time |
| QUERY | `=QUERY(range, "SELECT * WHERE ...")` | Data → From Other Sources → From Microsoft Query | Pseudo-SQL inside a spreadsheet; SQL goes **inside the quotes** |
| FILTER | `=FILTER(range, condition1, [condition2, ...])` | Filter (per-column conditions) | Show only rows meeting conditions; no query language needed |

- IMPORTRANGE example from the reading: a fundraiser analyst pulls matched-donation transactions into the donor sheet; each day the range grows (A1:B4001 → A1:B4501) so the newest rows come along.
- QUERY beats manual filtering when you'd otherwise copy filtered results out repeatedly (e.g., month-over-month customer growth) — build tabs as views, leave the original untouched.
- FILTER may run faster than QUERY, but QUERY can be combined with SUM/COUNT for summaries; FILTER can't.

## 🗣️ Teach it to a friend

When you finish cleaning data, you're not actually done — you have to prove it worked. That's
verification: go back through a checklist (nulls, misspellings, extra spaces, duplicates, wrong
data types, inconsistent dates, bad column names, truncated data) and finally ask whether the
data makes business sense and still answers the original question. Two handy verification
tricks: a pivot table with COUNTA on a text column shows every spelling variant with a count,
so the typo with one occurrence jumps out; in SQL, a CASE statement fixes "Tnoy" to "Tony" in
the output without touching the source table. Then document everything in a changelog — what
changed, when, who, who approved, version, and *why*. Your software's version history records
the *what*, but only your changelog records the *why*, and the why is what lets you go back and
warn someone their formula was wrong six months later. If you're editing a shared query, the
company probably uses version control: sync, change, get reviewed, commit with a comment,
revert if needed. Bonus: IMPORTRANGE, QUERY, and FILTER let you pull and slice data in
spreadsheets without copy-pasting or altering the original.

## 🃏 Flashcards

**Q:** What is verification in data cleaning?
**A:** A process to confirm that a data-cleaning effort was well executed and the resulting data is accurate and reliable.

**Q:** What is a changelog?
**A:** A file containing a chronologically ordered list of modifications made to a project.

**Q:** What does a changelog capture that automated version history does not?
**A:** The *reason* for the change (plus who approved it). Version history records what was done, not why.

**Q:** Name the seven things a changelog typically records.
**A:** The component that changed (data/file/formula/query), description of the change, date, person who made it, person who approved it, version number, reason for the change.

**Q:** Why use COUNTA instead of COUNT in a pivot table to check supplier names?
**A:** COUNT only counts numeric values; COUNTA counts the total number of values (including text) in a range.

**Q:** What is a CASE statement in SQL?
**A:** A statement that returns records that meet conditions by including an if/then statement in a query — WHEN condition THEN value ELSE original END.

**Q:** Does `CASE WHEN first_name = 'Tnoy' THEN 'Tony' ELSE first_name END AS cleaned_name` change the table?
**A:** No — it corrects only the displayed output in a new column; the underlying table data is not updated.

**Q:** What is Find and replace?
**A:** A tool that finds a specified search term and replaces it with something else.

**Q:** Which functions/features from the checklist handle extra spaces and duplicates?
**A:** TRIM for extra spaces; Remove Duplicates (spreadsheets) or DISTINCT (SQL) for duplicates.

**Q:** After the cleaning checklist, what three things do you review?
**A:** Confirm the business problem, confirm the goal of the project, verify the data can solve the problem and is aligned to the goal.

**Q:** In a version control system, what are syncing, code review, commit, and revert?
**A:** Sync = get the latest version before editing; code review = someone checks your change; commit = submit the change to the repository (with a what/why comment); revert = restore the previous version.

**Q:** IMPORTRANGE vs QUERY vs FILTER — which one syncs data from another spreadsheet? Which uses SQL-like syntax? Which can't be combined with SUM/COUNT?
**A:** IMPORTRANGE syncs from another sheet (Excel: Paste Link); QUERY uses SQL-like SELECT/WHERE (Excel: Microsoft Query wizard); FILTER shows matching rows but can't be combined with SUM/COUNT (QUERY can).

**Q:** What must you do the first time you use IMPORTRANGE on a spreadsheet?
**A:** Allow access to the source spreadsheet (click Allow access) — otherwise you get #REF!.

**Q:** Why isn't there a single universal verification checklist?
**A:** Each project has its own organization and data requirements; you build a project-specific list and revisit it as you get more data or better understanding of the goal.

## 💡 How I'll actually use this

- **nyc-payroll-explorer:** add a `CHANGELOG.md` to the repo (the Markdown link in this module's resources is exactly for this) — date, what changed, why, version. Every cleaning step I apply to the NYC payroll CSV (trimming agency names, standardizing title case, dropping true duplicates) gets an entry with the reason. Then a `verify.py` that runs the checklist: null counts per column, `value_counts()` on agency/title to spot spelling variants (the pandas version of the COUNTA pivot), dtype check, date-format check, and a business-logic sanity range on hours and pay.
- **flask-analytics-app:** use pandas `.map()` / `np.where` as the CASE-statement equivalent to reclass known bad labels at display time without touching the source table — same "report-level reclass, not a posted correction" idea. Write it in SQL CASE too when the query runs against SQLite.
- **Study-hub / all repos:** my git commits already are the version-control workflow from the bonus tip. Make the commit messages carry the *why*, not just the what — that's the changelog discipline, and recruiters read commit history.
- **Spreadsheet work:** rebuild the "by department" and "by month" tabs in any Sheets project with QUERY instead of copy-paste, and IMPORTRANGE for a tracking sheet that follows the source. Never edit the raw tab.
- **Interview line:** "Verification and changelogs aren't new to me — I've signed off certified payroll registers and kept adjustment logs with date, reason, and approver for 20 years. I now do the same in pandas and SQL, and my repos have CHANGELOG files and descriptive commit history to prove it."
