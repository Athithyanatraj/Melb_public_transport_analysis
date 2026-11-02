# Dashboard documentation — Melbourne Metro Train Service Explorer

The published Databricks AI/BI dashboard summarising scheduled Melbourne metropolitan train services from Victorian GTFS timetable data. It was built on the gold-layer tables produced by `notebooks/01_project_setup.ipynb` and answers four business questions about demand, peak pressure, weekend service, and accessibility.

- **Platform:** Databricks AI/BI Dashboards
- **Data window:** GTFS service calendar, 8 October – 31 December 2026
- **Tables:** Unity Catalog silver and gold Delta tables (`pt_silver_*`, `pt_gold_*`)
- **Layout:** one page, 11 widgets — 4 KPI counters, 5 bar charts, an hourly service-pattern chart, an accessibility pie chart, and an audit table

## Headline KPIs

| KPI | Value |
| --- | --- |
| Scheduled weekday journeys (network, per day) | 2,744 |
| Busiest station — daily stop events | Flinders Street, 1,944 |
| Network wheelchair accessible | 99.6% (225 of 226 stations) |
| Average weekend change vs weekday | −26% |

## Widgets

| Widget | Type | What it shows |
| --- | --- | --- |
| Scheduled weekday journeys | KPI counter | Total scheduled weekday journeys per day across the network |
| Busiest station — stop events | KPI counter | Daily stop events at the busiest station (Flinders Street) |
| Network wheelchair accessible (%) | KPI counter | Share of stations with wheelchair access |
| Avg weekend change vs weekday (%) | KPI counter | Average percentage change in journeys on weekend days |
| Top 10 Lines by Scheduled Journeys | Bar chart | Lines ranked by daily scheduled journeys |
| Top 10 Stations by Stop Events | Bar chart | Stations ranked by daily scheduled stop events |
| Weekday vs Weekend Scheduled Journeys by Line | Grouped bar | Weekday vs weekend journeys for each line |
| Services by hour of day | Line chart | Scheduled services across the day, highlighting the AM and PM peaks |
| Top interchange hubs | Bar chart | Stations ranked by number of lines serving them |
| Station Accessibility Across the Network | Pie chart | Stations by wheelchair-accessible status |
| Stations needing accessibility audit | Table | Stations with unknown accessibility status |

## Business questions answered

### Q1 — Where is demand concentrated across the network?

**Sunbury** runs the most daily journeys (324), and **Flinders Street** handles **1,944 stop events** — roughly 2× Southern Cross (998). The three City Loop stations (Melbourne Central, Parliament, Flagstaff) each carry 676.

*Takeaway: weight staffing, security, and cleaning rosters toward the CBD corridor.*

### Q2 — When is the network under most pressure?

Services peak during the weekday **AM (7–9am)** and **PM (4–6pm)** commuter peaks, as the hourly chart shows.

*Takeaway: plan crew shifts, platform staffing, and maintenance windows around the peaks; avoid works 7–9am and 4–6pm.*

### Q3 — How does weekend service differ from weekday?

Averaged over **every weekday (Mon–Fri) and weekend day (Sat–Sun)** in the timetable window, weekend services run **~26% below** weekday. **Werribee loses 50%** and **Lilydale 47%**, while branch lines (Upfield, Williamstown, Belgrave) hold steady or gain slightly. Flemington Racecourse runs weekend services only.

*Takeaway: model differentiated weekend timetables instead of one-size-fits-all cuts.*

### Q4 — How accessible is the network?

**99.6% of stations (225 of 226)** are wheelchair accessible; one station has an unknown accessibility status (shown in the audit table).

*Takeaway: close the data gap so every station can be promoted as accessible.*

## Methodology notes

- **Weekday vs weekend comparison:** the dashboard averages journeys across **all** Monday–Friday service dates versus **all** Saturday–Sunday service dates in the GTFS calendar window (8 October – 31 December 2026). Service dates are derived from `pt_silver_calendar` flags plus `pt_silver_calendar_dates` exceptions (all 40 exceptions in the window are service removals). See [genie-code-analysis.md](genie-code-analysis.md) for how this definition evolved.
- **Top-line measures** (busiest line, busiest station, stop-event counts) are daily scheduled-service measures for the dates displayed in the visuals; they are not live service information.
- **Accessibility** comes from `pt_gold_station_accessibility`; stations with unknown status are surfaced in the audit table rather than silently dropped.
