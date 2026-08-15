# Google Data Analytics — Course 3, Module 2: Data Ethics, Anonymization & Open Data

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 2 readings

## 🎯 What this module is about (one sentence)

Handling data responsibly: spotting bias, judging whether a source is trustworthy (ROCCC),
protecting people's private information (PII, anonymization), and balancing open public data
against individual privacy.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data ethics** | Standards of right and wrong for how data is collected, shared, and used | The same professional duty of care you had with payroll files — just written down as a framework. |
| **PII (personally identifiable information)** | Info that can identify a person, alone or combined with other data | SSNs, home addresses, bank details on direct deposit forms — the stuff you've guarded your whole career. |
| **Data anonymization** | Removing or masking identifying info (blanking, hashing, masking) | Redacting SSNs before sending a file to the auditors, or replacing names with employee numbers in a report. |
| **De-identification** | Wiping data completely clean of all personally identifying information | The scrubbed census-style version of a wage file — nothing in it can trace back to one person. |
| **Data privacy** | Preserving a data subject's information any time a data transaction occurs | Why W-2s go in sealed envelopes and payroll reports aren't left on the printer. |
| **Consent** | People's right to know how and why their data will be used before providing it | The authorization forms employees sign before you run a background check or garnishment. |
| **Transaction transparency** | All data processing should be explainable to the person who provided the data | Being able to walk an employee through exactly how their net pay was calculated, line by line. |
| **Data bias** | A preference that systematically skews analysis results in one direction | Judging "average salary" from only the managers' files — the sample skews everything upward. |
| **Sampling bias** | A sample that over/under-represents parts of the population | Surveying only day-shift staff about scheduling and calling it "employee opinion." |
| **ROCCC (good data source)** | Reliable, Original, Comprehensive, Current, Cited | Your source-document checklist: is this the original timesheet, is it complete, is it this period's, who signed it? |
| **Open data** | Data freely available to the public to use, reuse, and redistribute | NYC publishing its payroll data — the very dataset in my explorer project. |
| **Data interoperability** | Different systems/organizations being able to use each other's data | Why standardized formats matter — same reason every payroll vendor can produce an ACH/NACHA file. |
| **GDPR** | The European Union's data-protection regulation | HIPAA-style rules, but for personal data of people in the EU. |

### The aspects of data ethics (exam favorite!)
1. **Ownership** — individuals own the raw data they provide → *your employees own their personal info; you're the custodian*
2. **Transaction transparency** — processing should be explainable → *show the math on the paystub*
3. **Consent** — right to know how data will be used before giving it → *signed authorization first*
4. **Currency** — people should know about financial transactions from their data → *if someone profits from your data, you should know*
5. **Privacy** — protect the subject's info in every transaction → *lock the file room*
6. **Openness** — free access, usage, and sharing of (appropriate) data → *public salary schedules for government jobs*

### What makes data "open"? (all three required)
1. Available and accessible to the public as a **complete dataset**
2. Provided under terms allowing **reuse and redistribution**
3. **Universal participation** — anyone can use, reuse, and redistribute

The debate: open data speeds up research and decision-making, but third parties collect and resell data about people, so openness must be balanced against individual privacy.

### Open-data starting points
- **Data.gov** (most comprehensive US source) • **US Census Bureau** • **Open Data Network** • **Google Cloud Public Datasets** (pre-loaded in BigQuery) • **Google Dataset Search**

## 🗣️ Teach it to a friend

Think of every dataset as a filing cabinet full of other people's paperwork. Ethics is the
rulebook: people own their own information, they must consent to how it's used, and you must
be able to explain what you did with it. Before anything leaves the room, you black out the
parts that identify anyone (anonymization) — names, SSNs, account numbers. And before you
*trust* incoming data, you run the ROCCC check: is it Reliable, Original, Comprehensive,
Current, and Cited? Open data is the government leaving cabinets unlocked on purpose so
everyone benefits — which is great, as long as nobody's personal pages are in the drawer.

## 🃏 Flashcards

**Q:** What does PII stand for and what is it?
**A:** Personally identifiable information — data that can identify a person by itself or combined with other data (SSN, address, medical records, account numbers).

**Q:** What is data anonymization, and what techniques does it typically involve?
**A:** Protecting private/sensitive data by eliminating identifying info — typically blanking, hashing, or masking it.

**Q:** Which two industries rely most heavily on de-identification?
**A:** Healthcare and finance — the stakes (and regulations) are highest.

**Q:** What does ROCCC stand for?
**A:** Reliable, Original, Comprehensive, Current, Cited — the test for a good data source.

**Q:** Name the three requirements for data to be considered "open."
**A:** Publicly available/accessible as a complete dataset; terms allow reuse and redistribution; universal participation.

**Q:** Consent vs. currency — which ethics aspect is which?
**A:** Consent = right to know how your data will be used *before* providing it. Currency = right to know about financial transactions made from your data.

**Q:** What is sampling bias?
**A:** Over- or under-representing parts of a population because the sample isn't representative of the whole.

**Q:** Are data analysts usually responsible for performing anonymization?
**A:** Usually no — but they must know *what* needs anonymizing, and may do it themselves when working with copies for testing/development.

## 💡 How I'll actually use this

- **nyc-payroll-explorer** runs on open data — NYC's payroll dataset meets all three openness tests. Worth noting in the README: it's already anonymized-by-design debate territory (public employee names + salaries = the openness-vs-privacy tension in real life).
- If I ever load sample HR data into **flask-analytics-app** for a demo, I'll generate fake records or mask names/IDs first — never real employee data, even "just for testing."
- Interview line: "Twenty years of payroll means twenty years of PII handling — garnishment orders, SSNs, medical leave records. Data ethics isn't new to me; the vocabulary is."
- Bookmark Data.gov and Google Cloud Public Datasets as sources for my next portfolio project.
