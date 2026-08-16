# Google Data Analytics — Course 4, Module 5: Optional — Add Data to Your Resume

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 5 readings (add technical skills to your resume; the importance of diversity on a data analytics team)

## 🎯 What this module is about (one sentence)

Two career-side readings: which technical skills entry-level data analyst employers actually
look for (and how to put them on a resume as a "toolbox"), and why diverse teams and ethical
data practices produce fairer, more accurate analysis — plus what to do about bias when your
team is small.

**Sue's note:** this is the module that talks directly to the job hunt. The four skills Google
names — SQL, spreadsheets, data visualization, Python — you already have three on your resume
and 20 years of the fourth. The diversity reading is your HR background showing up in a new
context: bias in data collection is the same problem as bias in a hiring funnel.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll / HR translation |
|---|---|---|
| **Technical skills as a toolbox** | How you list each skill on a resume shows employers you can use that tool | Listing "ADP Workforce Now, Paychex, multi-state tax filing" — specific tools, not "payroll software." Same rule for data tools. |
| **SQL** | Basic, pivotal skill for any entry-level analyst; lets you retrieve information from databases; thousands of postings per month require it | Pulling the register from the payroll database yourself instead of waiting for IT to run the report. |
| **Spreadsheets** | 62% of companies still prefer spreadsheets for data insights; your first "database" on the job may be a spreadsheet; still powerful for reporting and presenting | You've lived in Excel — reconciliations, GL uploads, benefits census files. That's a real, listable analytics skill, not a footnote. |
| **Data visualization tools** | Simplify complex data so it's understood visually; Tableau, Power BI, Looker, Data Studio, Microstrategy, Datarama; **Tableau** is the beginner must-have (ease of use; ~34.9% projected job growth over the decade) | The turnover chart in the quarterly HR deck — same job, better tools. |
| **Python** | Most widely used programming language among data analysts; fundamentals are a big plus at entry level (expert not required) | The automation of everything you did by hand: `pandas` reads the register, applies the rules, writes the exceptions report. |
| **R** | A great addition as you become more advanced | Later, not now. |
| **Bias in data collection** | Bias can enter *before* collection — in deciding what to collect and how; biased data → inaccurate insights or reinforced inequity (bank collecting mainly in affluent areas → excludes lower-income customers) | Only surveying full-time salaried staff about benefits satisfaction and calling it "employee sentiment" — hourly staff never made it into the sample. |
| **Bias in data interpretation** | Analysts who don't know about disparities in a population may present an incomplete report (heart-disease study focused on male participants) | Reading a pay-equity report without adjusting for tenure and title mix — the number looks fine and it's wrong. |
| **Diverse team as a control** | More perspectives → more likely someone notices the gap in collection or the missing context in interpretation; also opens new markets (broader loan base) | Why HR investigations use a panel, not one person: someone catches what one reviewer wouldn't. |
| **Informed consent** | Voluntary, informed agreement before collecting someone's data | Employee authorization forms before pulling anything beyond payroll-required data. |
| **Anonymity & confidentiality** | De-identify; keep sensitive data protected | Redacting SSNs and names before a dataset leaves the payroll office; masking IDs in a shared file. |
| **Data security** | Robust safeguards against breaches and unauthorized access | Locked drives, role-based access to the payroll system — the same access-control mindset. |
| **Transparency** | Clearly communicate how data is collected, processed, shared | The privacy notice attached to open-enrollment forms. |
| **Data ownership & control** | People can access, correct, or delete their data | Employees' right to review and correct their own personnel and pay records. |

### Mitigating bias when your team is small or not diverse (from the reading)
1. Educate yourself on unconscious bias and its impact on data analysis
2. Review data collection methods to find and fix bias in tools and survey questions
3. Document all aspects of collection and analysis transparently so others can review your methodology
4. Consult diverse data experts and seek peer reviews from colleagues with diverse perspectives
5. Keep learning — stay current on research and techniques through discussion with other analysts

*Sue's note:* item 3 is the changelog/verification habit from Module 4 wearing an ethics hat.
Documentation is what makes your methodology reviewable for bias at all.

## 📝 Applied to Sue's resume

Concrete suggestions based on the "toolbox" reading and what's already on the resume (Projects
section with GitHub links; skills section listing Python, SQL, pandas):

**Skills section**
- **Rename the section "Technical Skills"** and group by tool type so all four employer-sought categories are visibly present:
  - *Languages & libraries:* Python (pandas), SQL (SQLite, BigQuery)
  - *Spreadsheets:* Excel (pivot tables, VLOOKUP, conditional formatting, data validation), Google Sheets (QUERY, IMPORTRANGE, FILTER)
  - *Data visualization:* Tableau Public, matplotlib/Chart.js (whichever flask-analytics-app actually uses) — if Tableau isn't there yet, publish one viz of the NYC payroll data on Tableau Public and add it; the reading calls Tableau the beginner must-have
  - *Version control & tools:* Git/GitHub, VS Code, Flask
- **Add spreadsheets explicitly.** Right now the section reads as "Python, SQL, pandas" — 20 years of Excel is a real analytics skill and 62% of companies still run insights in spreadsheets. Don't leave the most experienced tool off the list.
- **Be specific, not generic.** "SQL" → "SQL (JOINs, aggregation, CASE, DISTINCT; BigQuery, SQLite)". Specificity is how the resume "demonstrates you can use the tool."

**Projects section**
- Each project bullet should name the tool *and* the analytics task, so the toolbox shows in action:
  - **nyc-payroll-explorer:** "Cleaned and verified NYC public payroll data (n rows) with pandas — standardized text, removed duplicates, documented every transformation in a changelog; queried with SQL; visualized pay by agency in [Tableau/Chart.js]." (Add the changelog and verification script from Module 4 first, then the bullet is true.)
  - **flask-analytics-app:** "Built a Flask + SQLite analytics app; wrote SQL and pandas summaries with input validation on uploaded CSVs; deployed with Git-based workflow."
- Keep the GitHub links — recruiters click them. Make sure each repo has a README that names the same tools the resume does.

**Experience section (the bridge)**
- Rewrite two or three payroll/HR bullets in analyst language: "Reconciled multi-entity payroll to GL monthly using Excel pivot tables and VLOOKUP; identified and resolved variances before certification." That's data cleaning + verification + spreadsheets, described the way this reading says employers scan for.
- Add one line on data ethics/handling: "Managed confidential employee data under access-control and de-identification standards" — the ethics list from the diversity reading, and a real differentiator vs. bootcamp-only candidates.

**Summary line**
- "Data analyst with 20 years in payroll/HR operations; SQL, Python (pandas), Excel/Sheets, and Tableau; Google Data Analytics Certificate (in progress); Pursuit fellow." — all four categories, one sentence.

## 🗣️ Teach it to a friend

Employers hiring entry-level data analysts look for four technical tools: SQL (to pull data
from databases — the single most-required skill), spreadsheets (most companies still run
insights in Excel or Sheets), a visualization tool (Tableau is the beginner standard), and
Python fundamentals (R comes later). Your resume should list them specifically, like a toolbox,
and your project bullets should show each tool doing a real task. The second reading is about
bias: it can creep in before data is even collected (a bank only collecting data in wealthy
neighborhoods) and again when the data is interpreted (missing that a heart study was mostly
men). Diverse teams catch these gaps because someone at the table has the missing context. If
your team isn't diverse, you compensate by educating yourself on unconscious bias, auditing
your collection methods, documenting everything so others can review it, and asking outside
experts and peers to look. Underneath it all are ethical rules: informed consent, anonymity and
confidentiality, data security, transparency, and giving people control over their own data.

## 🃏 Flashcards

**Q:** What four technical skills does the course name as most sought for entry-level data analysts?
**A:** SQL, spreadsheets, data visualization tools, and Python programming.

**Q:** Which technical skill is described as "basic and pivotal to any entry-level data analyst position"?
**A:** SQL — it lets you communicate with and retrieve information from databases.

**Q:** What percentage of companies still prefer spreadsheets for data insights?
**A:** 62%.

**Q:** Which visualization tool is called a "must-have" for beginners, and what's its projected job growth?
**A:** Tableau — best known for ease of use; jobs requiring it expected to grow about 34.9% over the next decade.

**Q:** Do entry-level analysts need to be Python experts?
**A:** No — understanding the fundamentals is a big plus; Python is the most widely used language among analysts. R is a good addition later.

**Q:** Give the reading's example of bias in data collection.
**A:** A bank collecting data mainly in affluent areas — excluding lower-income individuals from its marketing and loan initiatives.

**Q:** Give the reading's example of bias in data interpretation.
**A:** A healthcare analyst not accounting for disparities among populations — e.g., a heart-disease study focused mostly on male participants; a diverse team spots the gender bias and recommends a balanced study.

**Q:** Name the five ethical guidelines for data use from the reading.
**A:** Informed consent; anonymity and confidentiality; data security; transparency; data ownership and control.

**Q:** Your team is small and not diverse. Name three steps to mitigate bias.
**A:** Educate yourself on unconscious bias; review collection methods for biased tools/questions; document methods transparently for review; consult diverse experts / seek peer review; keep learning (any three).

**Q:** Why does the reading say a diverse data team also helps the business, not just fairness?
**A:** Noticing gaps (e.g., extending loans to a broader base) attracts more customers and opens new markets and revenue streams.

**Q:** How should technical skills appear on a resume, per the reading?
**A:** Like a toolbox — each skill listed in a way that demonstrates you can use that tool (specific tools, shown in action).

## 💡 How I'll actually use this

- **Resume (this week):** apply the "Applied to Sue's resume" section above — add a Spreadsheets line and a Data visualization line to the skills section, tighten the two project bullets to name tool + task, and rewrite two payroll bullets in analyst language. This is one of the two pending job applications' prerequisites anyway.
- **nyc-payroll-explorer:** the NYC payroll dataset is a bias case study waiting to happen — before publishing any "average pay by agency" chart, check what's *not* in the data (which agencies or job categories are underrepresented, whether part-time/seasonal rows skew averages) and say so in the README. That's the "document transparently so others can review" step.
- **flask-analytics-app:** add a small "About this data" panel: source, what's collected, what's excluded, how IDs are anonymized. Transparency and confidentiality from the ethics list, made visible in the product.
- **Tableau Public:** publish one viz from the payroll data and link it from the resume — closes the visualization gap the reading flags.
- **Interview line:** "Twenty years of HR taught me where bias hides in a process — who's in the sample and who never got the survey. I bring that same eye to data collection and interpretation, and I document my methods so a reviewer can check my work."
