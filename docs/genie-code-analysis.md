# Answering business questions with Databricks Genie Code

The analysis in this project was built with **Genie Code**, the AI assistant in Databricks that turns natural-language requests into SQL, AI/BI dashboard datasets, and widgets. This document records the workflow, the questions asked, and what made it effective — including one place where reviewing the generated SQL changed the answer.

## The workflow

1. **Ask a business question in plain English**, e.g. *"How does weekend service differ from weekday service, by line?"*
2. **Genie Code writes the SQL** against the Unity Catalog tables (`pt_silver_*`, `pt_gold_*`). Every query is visible and reviewable — the output is a draft, not a black box.
3. **The query becomes a dashboard dataset** powering a widget (KPI counter, bar chart, table, …).
4. **A takeaway is added next to the visual**, so each chart answers a decision rather than just displaying a metric.

## Questions asked and what they produced

| Business question | Dashboard output |
| --- | --- |
| Where is demand concentrated across the network? | Top-lines and top-stations bar charts; busiest-station and journey KPIs |
| When is the network under most pressure? | Services-by-hour chart showing the AM and PM peaks |
| How does weekend service differ from weekday? | Weekday-vs-weekend grouped bar chart; average weekend change KPI |
| How accessible is the network? | Accessibility pie chart; 99.6% KPI; audit table for unknown-status stations |

## Worked example: iterating on the weekday/weekend definition

The first version of the weekday-vs-weekend comparison used a **single Tuesday versus a single Saturday**, which reported a network-wide weekend reduction of about **23%**.

That definition was challenged: a one-day sample is not a fair representation of "weekday" and "weekend" service. Genie Code rebuilt the comparison to **average every Monday–Friday service date against every Saturday–Sunday service date** across the full GTFS calendar window (8 October – 31 December 2026), honouring calendar exception dates (all 40 exceptions in the window are service removals).

The corrected figures:

- Network average weekend reduction: **−26%** (not −23%)
- Largest cuts: **Werribee −50%**, **Lilydale −47%**
- Branch lines (Upfield, Williamstown, Belgrave) hold steady or gain slightly; Flemington Racecourse runs weekend services only

The recommendation also changed: with per-line variation this wide, a **differentiated weekend timetable** is the right approach rather than a uniform percentage cut.

## What made the workflow effective

- **Questions framed as business decisions** ("where should staffing be weighted?") rather than metric pulls, which keeps the dashboard decision-oriented.
- **Transparent SQL** — every number on the dashboard is backed by an inspectable query over governed tables, so claims can be verified rather than trusted.
- **Iterative refinement** — the single-date → full-window correction shows the value of reviewing AI-generated logic and treating it as a draft.
- **Speed** — question, visual, and takeaway in one cycle made it practical to test different framings of the analysis.

## Limitations and lessons learned

- Always review the generated SQL: the first weekday/weekend definition was plausible but methodologically weak, and only human review caught it.
- Definitions should live in one place: the dashboard datasets were corrected, but the notebook's `pt_gold_weekday_weekend_comparison` table still uses the single-date definition and should be rebuilt to match.
- Scheduled-service measures answer *what is timetabled*, not *what ran* — GTFS data contains no realtime or ridership information.
- AI assistance accelerates the question → visual → takeaway cycle, but the analyst still owns the methodology and the conclusions.
