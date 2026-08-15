# Google Data Analytics — Course 3, Module 4: Organize & Protect Your Data

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 4 readings

## 🎯 What this module is about (one sentence)

Keeping your work findable and safe: consistent file naming conventions, logical folder
hierarchies, and the security tools (encryption, tokenization, version control) that let you
protect data without losing access to it.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **File naming conventions** | Consistent rules for naming files: content, date, version | "PR_Register_2024-06-15_Final.xlsx" vs. "copy of copy (2).xlsx" — you already know which office runs smoother. |
| **YYYYMMDD date format** | International date standard: year, month, day (20231125) | Filing by 20240615 instead of "June run" — files sort themselves chronologically, like check numbers. |
| **Revision version (v02)** | Version number in the file name, with a leading zero | "W-2 corrections round 2" → v02. The leading zero means round 10 (v10) still sorts correctly. |
| **Folder hierarchy** | Broad folders on top, specific subfolders inside | The file room: Year → Quarter → Pay period. Broad to specific, same as your paper system was. |
| **Archiving** | Moving completed/older files to a separate folder or storage | The banker's boxes: closed years go to storage, current year stays at your desk. |
| **Data security** | Protecting data from unauthorized access or corruption | The locked file room plus the "who can see salaries" access list, in digital form. |
| **Access control** | Password protection, user permissions, and encryption protecting a spreadsheet | Exactly who could open the payroll register and who could only see their own department — now enforced by the file itself. |
| **Encryption** | Scrambling data with an algorithm; a "key" reverses it | The locked bank bag: unreadable in transit, but your key opens it back to the original. |
| **Tokenization** | Replacing sensitive values with random tokens; real data stored/mapped elsewhere | Employee numbers on public reports instead of SSNs — the SSN-to-ID crosswalk lives in a separate, locked system. |
| **Version control** | Tracking who changed a file, what, when, and why | The audit trail on a payroll adjustment — every change initialed and dated, nothing overwritten silently. |

### Anatomy of a good file name (exam favorite!)
`SalesReport_20231125_v02`
1. **Name** — what's in it (`SalesReport`) → *short, meaningful, searchable*
2. **Creation date** — `20231125` = Nov 25, 2023 (YYYYMMDD) → *know your company's date standard*
3. **Revision version** — `v02`, leading zero for double-digit rounds → *never edit the wrong version again*
4. **Consistent order and style** — same pieces, same order, every time; underscores or hyphens, **no spaces or special characters** (software can choke on them)

### File organization best practices
- Agree on naming conventions **as a team, early** in the project — renaming later wastes time
- Align with existing company conventions rather than inventing new ones
- Keep a sample **text file documenting the conventions** where the whole team can find it (great for onboarding)
- Folders and subfolders in a logical hierarchy: broad → specific
- Store **completed work separately from in-progress work**; archive old files elsewhere

### Security vs. access: the tug-of-war
Data must be safe, but analysts need to use it *now*. Encryption and tokenization protect data while keeping it usable by the right people. Junior analysts don't build these systems (dedicated security teams do) — but the one practice you *can* own is **version control**: it lets teams collaborate on the same files and experiment without fear of overwriting each other's work.

## 🗣️ Teach it to a friend

Imagine two file rooms. In one, every folder is labeled "Misc" and "Final FINAL v3 (use this)."
In the other, every file reads Project_Date_Version, current work sits in one drawer, finished
work in another, and old years are boxed in storage. Same documents — but only one room lets
you find anything in ten seconds. That's file naming and hierarchy. Then protect the room:
encryption is a lockbox only your key opens; tokenization swaps the sensitive pages for
numbered placeholders and keeps the real ones in a vault across the hall. And version control
is the sign-out sheet showing who touched what, when, and why — so nobody's work gets
overwritten.

## 🃏 Flashcards

**Q:** What four things should a file name include?
**A:** The project's name, the file creation date, the revision version, and a consistent style/order.

**Q:** Why lead revision numbers with a zero (v02 instead of v2)?
**A:** So double-digit revision rounds (v10+) are built into the convention and files still sort correctly.

**Q:** What's wrong with spaces and special characters in file names?
**A:** Some software can't recognize them, causing errors — use hyphens, underscores, and capital letters instead.

**Q:** What is the YYYYMMDD in SalesReport_20231125_v02?
**A:** The creation date in international standard order — November 25, 2023.

**Q:** Encryption vs. tokenization — what's the key difference?
**A:** Encryption scrambles the data itself and a key reverses it; tokenization replaces data with random tokens while the original is stored and mapped in a separate location.

**Q:** If tokenized data is hacked, is the original data exposed?
**A:** No — the original lives in a separate location; the tokens alone are useless without the mapping.

**Q:** What does version control let you track?
**A:** Who made what changes to a file, when they were made, and why — enabling safe collaboration and experimentation.

**Q:** Where should completed files live relative to in-progress files?
**A:** Separately — and older files should be archived in a separate folder or external storage.

**Q:** Name three access control features that protect a spreadsheet.
**A:** Password protection, user permissions, and encryption.

## 💡 How I'll actually use this

- **Both repos get the treatment:** rename loose exports in nyc-payroll-explorer to the convention — `nyc-payroll_20260815_raw.csv`, `nyc-payroll_20260815_clean_v01.csv` — and add a `data/raw` vs. `data/processed` vs. `archive` folder hierarchy.
- **Git IS version control** — flask-analytics-app and this study-hub already track who/what/when/why on every commit. This module is why commit messages matter.
- Add a short `NAMING.md` to my projects documenting the convention — the "sample text file for the team" habit, even when the team is just me (and future me).
- Interview line: "I ran the file room and the audit trail for years — retention schedules, version-controlled adjustment logs, locked access to PII. This module is my old job with new tools: Git instead of initials, tokenization instead of a locked crosswalk binder."
