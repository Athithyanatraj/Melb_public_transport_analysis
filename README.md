# Melbourne Public Transport Analytics

> **Status: work in progress.** This repository is being built as a portfolio project for a Data Analyst / BI Analyst pathway.

## Project overview

This project explores scheduled Melbourne metropolitan train services using Victorian GTFS timetable data. It demonstrates a Databricks workflow for preparing data with PySpark, creating Delta tables, and analysing service patterns. The project does not analyse actual patronage or punctuality.

## Planned tools

- Databricks
- PySpark
- SQL
- Power BI
- Databricks AI/BI Genie (planned exploration)

## Current contents

The repository currently contains one Databricks notebook:

- `notebooks/01_project_setup.ipynb` — reads GTFS source files from a Databricks Volume, creates raw and cleaned Delta tables, and calculates scheduled-service and accessibility measures.

The notebook uses a Databricks Volume path configured in the workspace. It does not include raw GTFS data or any Databricks credentials.

## Work in progress

The dashboard documentation, reproducible setup instructions, documented data source, SQL-only query files, Power BI report, and AI/BI Genie exploration are still to be expanded.

## Databricks dashboard

A published Databricks dashboard is available in the project workspace: [Open the dashboard](https://dbc-d0e3bc0b-bca5.cloud.databricks.com/dashboardsv3/01f1c91a3fc515a3bc61b7350c5c988c/published?o=7474657943932641).

Access currently requires permission to the Databricks workspace, so it is not a public portfolio link.

## Dashboard screenshots

The screenshots below are saved from the project dashboard. They show scheduled-service measures for the dates displayed in the visuals; they should not be interpreted as live service information.

### Scheduled-service overview

![Top lines by scheduled journeys and top stations by scheduled stop events](docs/screenshots/dashboard-service-overview.png)

### Weekday, weekend, and accessibility view

![Weekday versus weekend scheduled journeys by line and station accessibility](docs/screenshots/dashboard-weekday-weekend-accessibility.png)

## Planned workflow

1. Document the public dataset source and its licence.
2. Make the Databricks setup reproducible for another user.
3. Add SQL query files alongside the notebook workflow.
4. Build a Power BI report from the prepared data.
5. Explore how Databricks AI/BI Genie can help users ask natural-language questions of the prepared data, documenting the setup and limitations.

## Repository structure

Current and planned folders:

```text
melbourne-public-transport-analytics/
├── data/           # Planned dataset notes; raw data is not committed unless licensing permits
├── notebooks/
│   └── 01_project_setup.ipynb
├── sql/            # SQL queries (to be added)
├── power-bi/       # Power BI files or report documentation (to be added)
├── docs/           # Data dictionary, methodology, and screenshots (to be added)
├── README.md
└── .gitignore
```

## How to follow the project

As the work progresses, this README will be updated with the data source, setup instructions, dashboard views, and documented insights.

## Author

Built as a learning and portfolio project.
