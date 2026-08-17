# Google Data Analytics — Course 6, Module 1: Visualize Data

**Platform:** Coursera (Google Data Analytics — *Share Data Through the Art of Visualization*) | **Studied:** Aug 2026 | **Source:** module 1 readings + module 1 glossary

> *(guide grows as more module 1 readings are added)*

## 🎯 What this module is about (one sentence)

Analysis nobody understands is analysis nobody acts on — this module covers what makes a
visualization *effective* (not just pretty), the design principles and design-thinking process
behind good charts, how to pick the right chart for the pattern in your data, how to make the
key number impossible to miss, and why "these two things moved together" is not the same as
"one caused the other."

**Sue's note:** you have been doing data visualization for 20 years without calling it that.
Every financial package you walked shareholders and CPAs through — the trend chart of labor cost,
the pie of benefits spend, the highlighted variance column — was a visualization with an audience,
a story, and a goal. This module gives you the vocabulary and a checklist for what you already do
by instinct, plus the tool (Plotly, Tableau, spreadsheets) to do it on any dataset.

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data visualization** | The graphical representation of data — turning numbers into shapes, colors, and positions the eye can read fast | The labor-cost trend chart in the board package. The CFO didn't read the 40-column register; they read the chart. Your job was to make the chart tell the truth in five seconds. |
| **McCandless method** (4 elements) | A good viz balances **Information** (data), **Story** (concept), **Goal** (function), and **Visual form** (metaphor). Missing one and it's a sketch, a pretty picture, or a boring table. | The quarterly package: data = the GL numbers; story = "overtime is climbing in one department"; goal = get approval to hire; visual form = the chart that makes it obvious. All four, or the meeting goes nowhere. |
| **Kaiser Fung's Junk Charts trifecta checkup** | Three questions to critique any chart: (1) What is the practical question? (2) What does the data say? (3) What does the visual say? A good chart answers all three at once. | The auditor's questions in a different order: what are we trying to prove, what do the numbers show, and does the exhibit actually show it? If the chart says something the data doesn't, that's an exhibit you'd never sign. |
| **Pre-attentive attributes** | Visual elements the brain registers automatically, without conscious effort — the reason a red cell jumps out of a sea of black text | Conditional formatting on the variance column. Nobody "reads" that a cell is red — they just see it. You've been using pre-attentive attributes since Excel 97. |
| **Marks** | Basic visual objects (points, lines, shapes). Each has four qualities: **position, size, shape, color** | A bar's height (size), where it sits on the timeline (position), whether it's a bar or a dot (shape), red for over budget (color). |
| **Channels** | Visual variables that carry data. Judged on **accuracy** (color is great for categories, bad for 5 vs 5.5), **popout** (how easily a value stands out), **grouping** (proximity, similarity, enclosure, connection) | Color-coding departments works; color-coding exact dollar amounts doesn't — nobody can tell $48,200 from $49,100 by shade. Use position/length for amounts, color for categories. |
| **Emphasis dilutes** | The more things you emphasize, the less each one counts — they compete | A variance report where every line is bold and highlighted highlights nothing. One red number in a clean table gets the room's attention. |
| **Nine principles of design** | Balance, Emphasis, Movement, Pattern, Repetition, Proportion (build with these six) + Rhythm, Variety, Unity (check with these three) | See the breakdown below — you'll recognize every one from laying out a financial statement page. |
| **Design thinking** (5 phases) | Empathize → Define → Ideate → Prototype → Test. A user-centric process for solving problems, including improving dashboards | How you rolled out a new timesheet or self-service portal: put yourself in the employee's shoes, define what they need, brainstorm, mock it up, have a few people try it before HR sees it. |
| **Decision tree (chart choice)** | A series of questions about your data that leads you to the right chart type | "What's the story?" One numeric variable → histogram. Change over time → line (small changes) or column (big changes). Parts of a whole → pie. Relationship between two variables → scatterplot (or heat map if too many points). |
| **Correlation** | The degree to which two variables move together — positive (both up), negative/inverse (one up, one down), none (unrelated). Correlation does NOT mean one causes the other | Overtime went up and turnover went up — **related, but did one cause the other?** Maybe both were caused by a hiring freeze. Correlation tells you to look closer; it doesn't tell you the answer. |
| **Causation** | An action directly leads to an outcome (lightning causes thunder) | Raising the shift differential caused night-shift applications to rise — you can defend that because you controlled the change and watched the result. Most payroll "trends" aren't that clean. |
| **Headline / Subtitle / Labels / Annotations** | The text that turns a chart into something readable in five seconds: headline says what it is, subtitle adds context, labels identify axes/data (ideally replacing the legend), annotations point at the key value | Every exhibit in the package had a title, a "(in thousands, FY2025)" subtitle, labeled columns, and a footnote arrow on the number the board would ask about. Same discipline. |
| **Static vs. dynamic visualization** | Static doesn't change unless edited; dynamic is interactive or changes over time | The printed PDF board package vs. the Plotly dashboard where a stakeholder can filter by department themselves. |
| **Alternative text (alt text)** | Text describing non-text content (images, charts) for people who can't see it | Accessibility — the equivalent of describing an exhibit aloud on a conference call for someone who didn't get the deck. |
| **Mental model** | An analyst's thought process and approach to a problem | The month-end close routine in your head: you know the order you check things. Chart design gets its own routine (see 60-minute chart). |
| **Patterns in data** | Change (line/column), Clustering (distribution graph), Relativity (pie), Ranking (column), Correlation (scatterplot) | Trend in labor cost = change; who earns what band = clustering; benefits as % of total comp = relativity; top 10 OT earners = ranking; hours vs. errors = correlation. |

### The nine principles of design (exam favorite!)

**Build with these six:**
1. **Balance** — visual elements distributed evenly; not symmetry, just no side distracting from the other. *(A balanced financial statement page: columns aligned, consistent widths, nothing lopsided.)*
2. **Emphasis** — a focal point so the audience knows where to look; contrasting color/value is the tool. *(The one red variance number.)*
3. **Movement** — the path the eye travels; should mimic how people read (left to right). *(A trend line pulling the eye across the fiscal year.)*
4. **Pattern** — similar shapes/colors show similarity; break the pattern to create emphasis. *(Same color for the same department across every chart in the deck.)*
5. **Repetition** — repeating chart types, shapes, colors makes distinct data sets recognizable. *(Every quarter's package laid out the same way, so the board knows where to look.)*
6. **Proportion** — relative size signals importance; the biggest chart on the dashboard is the one that matters most — and every chart must still accurately reflect the values in it. *(Don't make the pie slice bigger than the number justifies.)*

**Check with these three (once the chart is finished):**
7. **Rhythm** — sense of movement/flow; if it doesn't flow, rearrange.
8. **Variety** — enough variety in chart types/colors to engage, not so much it confuses.
9. **Unity** — the whole thing is cohesive; disjointed = confusing and overwhelming.

### Chart-choice decision tree (from "Data grows on decision trees")
- **Only one numeric variable?** → histogram or density plot (sometimes a bar chart). *Student heights → histogram of how many in each height range.*
- **Multiple datasets?** → line chart (change over a continuous line) or pie chart (parts of a whole). *Quarterly sales.*
- **Measuring change over time?** → line chart usually; **when the changes are larger, a bar/column chart is better.** *NYC visitors over 6 months.*
- **Need to show relationships between two variables?** → scatterplot; **if too many data points obscure the relationship, use a heat map.** *Hours studied vs. grades → scatterplot; population of 50 states with millions of points → heat map.*

### Chart types cheat sheet (from "The wonderful world of visualizations")
| Chart | Best for | Payroll example |
|---|---|---|
| **Line chart** | Changes over time (short or long); better than bars when changes are small; compare groups over the same period | Graduation rate 2008–2012 → *labor cost by month; male vs. female headcount trend* |
| **Column / bar chart** | Contrast and compare two or more values by height/length; ranking | Vehicles sold by month → *OT hours by department, top 10 earners* |
| **Heat map** | Color contrast to compare categories; relationships between two variables | Temperature by city × month → *OT hours by department × week* |
| **Pie chart** | Proportions of a whole | Favorite movie categories → *benefits vs. taxes vs. net as % of gross* |
| **Scatterplot** | Relationship between two variables, no connecting line | Temperature vs. ice cream sales → *tenure vs. hourly rate* |
| **Distribution graph** | Spread/frequency of outcomes; becomes a **histogram** when the x-axis is numeric ranges | Coffee cups per customer per week → *how many employees fall in each pay band* |

### Design a chart in 60 minutes (the prototype routine)
1. **Prep (5 min)** — clear mental/physical space; brainstorm how the data should look given how much and what type you have.
2. **Talk and listen (15 min)** — get to the **"ask behind the ask"** and set expectations; really listen to stakeholder feedback. *(The CEO says "show me overtime" — the ask behind the ask is "should I approve two more hires?")*
3. **Sketch and design (20 min)** — draft the approach; define timing and output.
4. **Prototype and improve (20 min)** — build a visual, gauge if it communicates, repeat until it does. Several drafts is normal.
- Goal: a mock-up you can show quickly to confirm it's communicating what you want — before polishing.

### Design thinking for a dashboard (the banking example)
- **Empathize** — use the online-banking dashboard like a customer: do colors/labels make sense? how easy is it to set a budget? does clicking a donut slice show the transactions? Main purpose = help customers stay within budget / save money.
- **Define** — what else do customers need? Track income, track discretionary spending, pay off debt.
- **Ideate** — new visuals? bar/line charts alongside the donut? custom categories?
- **Prototype** — developers build the next version.
- **Test** — you (and others) test before stakeholders see it.
- Takeaway: understand user needs, generate ideas, make **incremental improvements over time**. A junior analyst won't build the dashboard alone but can drive its improvement this way.

### Correlation vs. causation (exam favorite!)
- **Positive** correlation: both go up. **Negative/inverse:** one up, one down. **None:** one changes, the other stays flat.
- Temperature and ice cream sales rise together — but not every temperature change moves sales, and maybe there was an ice cream sale that week. Correlation ≠ cause.
- **Pellagra:** people thought dirty living conditions caused it (most sufferers lived in them). Real cause: niacin (B3) deficiency. Poverty caused both the diet and the housing — the housing was correlation only.
- **SNAP website:** analytics show qualifying people visit and leave without signing up. Analytics gives clues (correlations: repeat visits, fast exits) but you need **additional data — a survey — to find the actual cause** before you can fix sign-up rates.
- Key takeaways: critically analyze any correlation; examine context to see if causation makes sense *and is supported by all the data*; know the limits of your tools.
- Payroll version: OT up + turnover up. Before you tell the board "overtime is driving people out," check whether a hiring freeze, a new manager, or a seasonal push explains both. Report the correlation honestly; earn the causation.

### Highlighting key information: guidelines and style checks (exam favorite!)
Audience should understand the chart in **the first five seconds**.

| Component | Content | Length | Position | Style checks |
|---|---|---|---|---|
| **Headline** | Briefly describe the data | Usually the width of the data frame | Above the data | Brief language; no all caps, no italic, no acronyms, no abbreviations, no humor/sarcasm |
| **Subtitle** | Clarify context | Same as or shorter than headline | Directly below headline | Smaller font than headline; no undefined words; no all caps/bold/italic; no acronyms/abbreviations |
| **Labels** | Replace the need for legends | Usually under 30 characters | Next to data, or below/beside axes | A few words only; thoughtful color-coding; callouts pointing to data; no all caps/bold/italic |
| **Annotations** | Draw attention to certain data | Varies, limited by open space | Immediately next to the data annotated | No all caps/bold/italic; **no rotated text**; don't distract from the data |

- The tri-city rents example: a naked line chart could be rents, product sales, or school absences. Headline "Average Rents in the Tri-City Area" → still ambiguous (San Diego? Bay Area? NC? UAE?) → subtitle "Oceanside, Vista, and Carlsbad" fixes it → axis labels "Months (January–June 2020)" / "Average Monthly Rents ($)" → **direct labels** on each line instead of a legend → annotate the peak rents.
- **Always label your axes.** Prefer direct labels over legends.

### Glossary terms not covered above (from the module 1 glossary)

| Term | Plain-English meaning | Sue's payroll translation |
|---|---|---|
| **Data composition** | Combining the individual parts of a visualization and displaying them as a whole | Assembling the package: chart + title + footnote + source line = one exhibit. |
| **Cluster** | A collection of data points with similar values | The knot of employees all earning within $1 of the minimum — visible on a distribution graph. |
| **Ordinal data** | Qualitative data with a set order or scale | Job grades 1–10, performance ratings (Exceeds / Meets / Below) — ordered categories, not numbers you'd average. |
| **Ranking** | Positioning values within a scale of achievement or status | Top 10 OT earners — a column chart, sorted. |
| **Relativity** | Considering observations in relation/proportion to something else | Benefits as a percentage of total comp, not just dollars. |
| **Legend** | Identifies the meaning of elements in a viz | The color key — which the "Pro tips" reading says to replace with direct labels when possible. |
| **X-axis / Y-axis** | Horizontal (bottom; time scales, categories) / vertical (left; frequencies, numeric values) | Months across the bottom, dollars up the side. |
| **AVERAGEIF / MAXIFS / MINIFS** | Spreadsheet functions returning the average / max / min of a range that meets a condition | Average pay rate *for one department*; highest OT *for hourly staff only*. Conditional aggregates you've built by hand a hundred times. |
| **Sort sheet vs. sort range** | Sort sheet: sorts all data by one column, keeps rows together. Sort range: sorts only the selected range, leaves everything else | Sort sheet is safe (rows stay intact); sort range on only the name column is how someone ends up with the wrong SSN on the wrong employee. |
| **CONVERT** (SQL) | Changes the unit of measurement of a value | Hours to minutes, or annual salary to hourly rate in-query. |
| **CREATE TABLE / SELECT INTO / DROP TABLE** (SQL) | Add a temporary table usable by multiple people / copy data into a temp table without adding it to the DB / remove a temp table | Building a scratch table of this period's payroll for analysis, then cleaning up. |
| **HAVING** (SQL) | Filters a query's results (not the underlying table); only with aggregate functions | `GROUP BY department HAVING SUM(ot_hours) > 500` — show me only departments over the OT threshold. |
| **Inner query** | A SQL subquery inside another SQL statement | "Employees whose rate is above the average rate" — the average is computed by the inner query. |
| **Calculus** | Math of rates of change | Mentioned in passing; not something you'll compute here. |
| **R / Tableau** | R = programming language for stats and viz (Course 7); Tableau = BI/analytics platform for visualizing data (Module 2) | The tools coming next. |

## 🗣️ Teach it to a friend

A visualization is only good if it does four things at once: it has real data, tells a story,
serves a specific goal, and has a visual form that fits — that's the McCandless method. To check
one, ask Kaiser Fung's three questions: what's the practical question, what does the data say,
and what does the visual say? The brain notices some things automatically — position, size,
shape, color — so you use those "pre-attentive attributes" on purpose: color for categories,
length or position for amounts, and emphasize *one* thing, because emphasizing everything
emphasizes nothing. Nine design principles guide the layout (balance, emphasis, movement,
pattern, repetition, proportion — then check rhythm, variety, unity), and design thinking
(empathize, define, ideate, prototype, test) keeps you focused on what the audience actually
needs. Pick the chart by the pattern in the data: change → line or column, parts of a whole →
pie, distribution → histogram, relationship → scatterplot. Then make it readable in five seconds
with a headline, a subtitle, labeled axes, direct labels instead of a legend, and one annotation
on the number that matters. And when two things move together — overtime and turnover, say —
report the correlation honestly, but don't claim one caused the other until you've done the work
to prove it. It's exactly what I did with every board package; now it has names.

## 🃏 Flashcards

**Q:** What are the four elements of the McCandless method?
**A:** Information (data), Story (concept), Goal (function), Visual form (metaphor). A successful visualization balances all four.

**Q:** What are the three questions in Kaiser Fung's Junk Charts trifecta checkup?
**A:** (1) What is the practical question? (2) What does the data say? (3) What does the visual say?

**Q:** What are pre-attentive attributes?
**A:** Elements of a visualization people recognize automatically, without conscious effort (e.g., a red mark among gray ones).

**Q:** What are marks, and what four qualities does each mark have?
**A:** Basic visual objects (points, lines, shapes). Qualities: position, size, shape, color.

**Q:** Channels vary in effectiveness based on which three elements?
**A:** Accuracy, popout, and grouping.

**Q:** Is color a good channel for distinguishing 5 from 5.5?
**A:** No — color is accurate for categorical differences (apples vs. oranges) but poor for quantitative differences.

**Q:** Name the nine principles of design, and which are "build" vs. "check" principles.
**A:** Build: Balance, Emphasis, Movement, Pattern, Repetition, Proportion. Check (once finished): Rhythm, Variety, Unity.

**Q:** What are the five phases of design thinking?
**A:** Empathize, Define, Ideate, Prototype, Test.

**Q:** Per the decision tree, your data has one continuous numeric variable. Which chart?
**A:** Histogram (or density plot); sometimes a bar chart.

**Q:** You're plotting change over time and the changes are large. Line or bar?
**A:** Bar/column — line charts are better for smaller changes.

**Q:** When should you use a heat map instead of a scatterplot?
**A:** When there are too many data points and the relationship gets obscured (e.g., population across all 50 states).

**Q:** Match the pattern to the chart: change, clustering, relativity, ranking, correlation.
**A:** Change → line/column; clustering → distribution graph; relativity → pie; ranking → column; correlation → scatterplot.

**Q:** Define positive, negative, and no correlation.
**A:** Positive: both variables go up. Negative/inverse: one up, one down. None: one changes and the other stays about the same.

**Q:** Why was the pellagra example a correlation, not causation?
**A:** Unsanitary conditions co-occurred with pellagra, but the cause was niacin (B3) deficiency — poverty drove both the diet and the housing.

**Q:** In the SNAP website example, what does Google Analytics give you and what do you still need?
**A:** It gives clues/correlations (repeat visits, quick exits); you need additional data such as a survey to find the actual cause.

**Q:** What are the four steps and time boxes of the 60-minute chart?
**A:** Prep (5 min), Talk and listen (15 min), Sketch and design (20 min), Prototype and improve (20 min).

**Q:** What is the "ask behind the ask"?
**A:** The real objective underneath a stakeholder's stated request — uncovered in the talk-and-listen step by asking questions and listening to feedback.

**Q:** How quickly should an audience be able to understand a visualization?
**A:** In the first five seconds.

**Q:** Headline vs. subtitle vs. label vs. annotation?
**A:** Headline: large text at top saying what data is presented. Subtitle: adds context below the headline in smaller font. Label: identifies data or an axis (can replace a legend). Annotation: briefly explains or focuses attention on specific data, placed right next to it.

**Q:** Name three style "don'ts" for headlines.
**A:** Don't use all caps, italic, acronyms, abbreviations, or humor/sarcasm (any three).

**Q:** How long should a label usually be, and what's one thing annotations must never do?
**A:** Fewer than 30 characters; annotations should not use rotated text (or all caps/bold/italic) or distract from the data.

**Q:** Static vs. dynamic visualization?
**A:** Static doesn't change unless edited; dynamic is interactive or changes over time.

**Q:** Sort sheet vs. sort range?
**A:** Sort sheet sorts all data by one column and keeps rows together; sort range sorts only the selected range and leaves the rest untouched.

## 💡 How I'll actually use this

- **flask-analytics-app — audit the Plotly charts against the nine principles:** one consistent color per category across every chart (repetition/pattern), a single accent color reserved for the number that matters (emphasis — and only one), x-axis time left-to-right (movement), the most important chart largest on the page (proportion), and a final pass for rhythm/variety/unity. Run each chart through the trifecta checkup: what's the question, what does the data say, does the visual say the same thing?
- **flask-analytics-app — KPI cards are pre-attentive attributes in a box:** big number = size, position at the top = position, red/green only where it means something = color. Add a one-line subtitle for context ("vs. prior month") and don't color every card — emphasis dilutes.
- **flask-analytics-app — headline/subtitle/label discipline in Plotly:** every `fig.update_layout(title=...)` gets a plain-English headline plus subtitle-style context, both axes titled, direct labels or hover text instead of a legend where possible, and an annotation on the peak or the outlier. No rotated axis text if I can avoid it.
- **nyc-payroll-explorer — pick charts by the pattern:** OT pay over fiscal years → line; top agencies by OT → sorted column (ranking); base pay distribution → histogram (clustering); base pay vs. OT pay → scatterplot, and switch to a heat map when I'm plotting hundreds of thousands of rows. Sketch the story first (60-minute routine) before writing code.
- **nyc-payroll-explorer — correlation vs. causation on purpose:** if OT and headcount move together in an agency, I'll write that as a correlation and list the plausible causes (budget cycles, seasonal work) instead of claiming one drives the other. Good practice for how I'll word findings in a README.
- **Job hunt / interviews:** "I've been building visualizations for stakeholders for 20 years — labor-cost trend charts, benefits mix, variance exhibits for shareholders and CPAs. Course 6 gave me the framework: McCandless's four elements, the nine design principles, and the five-second rule for headlines and labels. And I know the difference between overtime and turnover being *correlated* and one *causing* the other — I don't put a causal claim in front of a board without the evidence." Design thinking (empathize → test) is also a clean answer to "how would you improve our dashboard?"
