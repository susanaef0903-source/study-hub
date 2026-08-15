# Google Data Analytics — Course 2, Module 1: Ask Effective Questions

**Platform:** Coursera (Google Data Analytics) | **Studied:** Aug 2026 | **Source:** module 1 readings

## 🎯 What this module is about (one sentence)

Before touching any data, a good analyst nails down the *right question* — using the six-phase
analysis process, the six common problem types, and the SMART checklist to make sure the
question is actually answerable.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data analysis process** | Six phases: Ask, Prepare, Process, Analyze, Share, Act | Your payroll cycle already works this way: figure out what's needed (ask), pull timesheets (prepare), fix errors (process), calculate (analyze), send reports (share), cut checks (act). |
| **Data life cycle** | Plan, capture, manage, analyze, archive, destroy — the stages *data itself* goes through | Document retention rules: a W-4 is collected, filed, used, archived 4 years, then shredded. Don't confuse this with the analysis process — exam trap! |
| **Structured thinking** | Recognize the problem, organize info, reveal gaps, identify options | How you approached a payroll discrepancy: what's wrong, what records do I have, what's missing, what are my fix options. |
| **Problem types (6)** | Predictions, categorizing, spotting something unusual, identifying themes, discovering connections, finding patterns | Forecasting OT costs (prediction), coding pay types (categorizing), catching a paycheck that's way off (spotting unusual), grouping exit-interview feedback (themes), linking late timesheets to late checks (connections), noticing errors spike every quarter-end (patterns). |
| **SMART question** | Specific, Measurable, Action-oriented, Relevant, Time-bound | "Reduce payroll errors" is vague. "What caused the 12 off-cycle corrections in Q2?" is SMART. |
| **Leading question** | A question that pushes people toward one answer | "The new timekeeping system is better, isn't it?" — you'd never get honest feedback from staff that way. |
| **Closed-ended question** | Invites a one-word answer | "Was open enrollment smooth?" → "Yes." Useless. Ask "What confused employees most during open enrollment?" instead. |
| **Vague question** | No context, can't be answered usefully | "Does the tool work for you?" vs. "Is the new payroll system faster at data entry than ADP was, and by how much?" |
| **Unfair question** | Makes assumptions or can't be answered honestly | "Why is our benefits package the best in the industry?" assumes the conclusion. |

### The six phases, memorized
**Ask → Prepare → Process → Analyze → Share → Act.**
(Ask = define the problem with stakeholders; Prepare = decide what data and where;
Process = clean it; Analyze = calculate and find the story; Share = visuals and dashboards;
Act = recommendations that drive decisions.)

### Categorizing vs. identifying themes (they love to test this)
Categorizing = assigning items to categories. Identifying themes = grouping those categories
into *broader* themes. Themes are one level up from categories.

## 🗣️ Teach it to a friend

Data analysis isn't "run the numbers" — it's a six-step loop that starts with a conversation, not
a spreadsheet. First you sit down with whoever has the problem and ask questions until the real
problem is clear (not the problem they *think* they have). A good question passes the SMART test:
specific enough to focus, measurable so you'll know the answer when you see it, action-oriented so
the answer changes something, relevant to the actual problem, and time-bound so you know what
period you're studying. Avoid questions that lead people, close them off with yes/no, or are so
vague nobody can answer. Only then do you gather data, clean it, analyze it, present it, and act.

## 🃏 Flashcards

**Q:** Name the six phases of the data analysis process, in order.
**A:** Ask, Prepare, Process, Analyze, Share, Act.

**Q:** How is the data *life cycle* different from the data *analysis process*?
**A:** The life cycle is what data itself goes through (plan, capture, manage, analyze, archive, destroy); the analysis process is what the analyst does (ask → act).

**Q:** What does SMART stand for in SMART questions?
**A:** Specific, Measurable, Action-oriented, Relevant, Time-bound.

**Q:** Name the six common problem types.
**A:** Making predictions, categorizing things, spotting something unusual, identifying themes, discovering connections, finding patterns.

**Q:** What's the difference between categorizing things and identifying themes?
**A:** Categorizing assigns items to categories; identifying themes groups those categories into broader themes.

**Q:** "This product is too expensive, isn't it?" is what kind of bad question?
**A:** A leading question — it steers the person toward a certain response.

**Q:** What are the four activities of structured thinking?
**A:** Recognize the current problem, organize available information, reveal gaps and opportunities, identify your options.

**Q:** Why should survey questions be open-ended?
**A:** Open-ended questions invite detailed responses you can qualify or disqualify solutions with; closed-ended ones get uninformative one-word answers.

## 💡 How I'll actually use this

- Before adding any new chart to flask-analytics-app or nyc-payroll-explorer, write the SMART question it answers first (e.g., "Which NYC agencies had the highest OT spend growth from FY22 to FY24?") — if I can't write it, the chart doesn't earn a spot.
- Interview line: "I've run the ask-prepare-process-analyze-share-act loop for 20 years — every payroll cycle is exactly that process, I just didn't have the vocabulary."
- When someone asks me for "a report on overtime," practice the Ask phase: turn it into a specific, time-bound question before opening a single file.
