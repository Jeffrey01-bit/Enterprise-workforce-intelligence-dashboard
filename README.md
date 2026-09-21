# Enterprise Workforce Intelligence & Attrition Analytics

## Overview

Enterprise Workforce Intelligence & Attrition Analytics is a Power BI report for reviewing workforce composition, employee status, workforce movement, headcount trends, and attrition. The report combines employee and organizational dimensions with lifecycle, compensation, performance, engagement, training, and attendance data to present a focused workforce overview and supporting business insights.

The current report is implemented as a single-page Power BI dashboard with interactive slicers, KPI cards, charts, and a Key Insights section.

## Objectives

- Monitor total, active, and inactive workforce levels.
- Understand employee distribution by department, location, and employment type.
- Review workforce movement, including hires, promotions, transfers, exits, and returns.
- Track headcount trends and year-to-date employee exits.
- Measure attrition and compare the current attrition rate with the previous year.
- Surface concise, filter-responsive workforce observations for business review.

## Dashboard Features

The implemented dashboard includes:

- KPI cards for total employees, active employees, inactive employees, employee exits, active and inactive workforce percentages, and year-to-date attrition measures.
- A workforce trend visual based on the `Headcount Trend` measure.
- An employee movement visual titled **Employee Movement (YTD)** covering new hires, promotions, transfers, employee exits, and return events.
- Employee distribution by department.
- Employee distribution by location/city.
- Workforce distribution by employee type.
- A **Key Insights** section with measures that format headcount growth, active workforce percentage, and attrition-rate commentary.
- Slicers for year, quarter, department, location/city, employee status, and employment type.
- A **Clear Filters** action button.
- Supporting visual elements and report-page layout styling.

## Data Model

The semantic model uses imported tables organized into dimensions, facts, and a dedicated measures table.

### Dimension tables

| Table | Role |
| --- | --- |
| `dim_employee` | Employee attributes, employment type, hire date, status, organization keys, and manager indicators |
| `dim_date` | Calendar attributes used for date filtering and time-based analysis |
| `dim_department` | Department and business-unit mapping |
| `dim_business_unit` | Business-unit attributes |
| `dim_job_role` | Job role, family, category, and level information |
| `dim_location` | Office, city, country, region, and time-zone attributes |
| `dim_manager` | Manager hierarchy and manager status attributes |

### Fact tables

| Table | Role |
| --- | --- |
| `fact_employee_lifecycle` | Dated employee events such as hires, promotions, transfers, leave, returns, and exits |
| `fact_compensation` | Effective-dated salary, bonus, pay grade, and total compensation values |
| `fact_performance` | Performance reviews, ratings, scores, and goal achievement |
| `fact_engagement` | Engagement survey and employee sentiment measures |
| `fact_training` | Training activity, hours, cost, and completion status |
| `fact_attendance` | Attendance, absence, leave, and onsite-work measures |

The model defines relationships from the fact tables to `dim_employee` through `EmployeeID`, and from event or effective dates to `dim_date[Date]`. It also relates employees to departments, locations, job roles, and business units through their corresponding keys. The model includes Power BI-generated local date tables for employee date hierarchies.

## Measures and Analytics

The dedicated `_Measures` table contains the report calculations. Important implemented measures include:

| Measure group | Implemented measures and purpose |
| --- | --- |
| Workforce overview | `Total Employees`, `Active Employees`, `Inactive Employees`, `New Hires`, `Total Managers`, and `Individual Contributors` |
| Attrition and lifecycle | `Employee Exits`, `Attrition Rate`, `YTD Employee Exits`, `YTD Attrition Rate`, `Promotions`, `Transfers`, `Leave Events`, and `Return Events` |
| Workforce percentages | `Employee of Total`, `Active of Total`, `Inactive of Total`, `Promotion Rate`, and `Transfer Rate` |
| Trend analysis | `Headcount Trend`, `Headcount Growth %`, `Previous Year Attrition Rate`, and `Attrition Rate Change` |
| Performance and engagement | Average performance score, performance rating, goal achievement, engagement score, manager satisfaction, career growth, compensation satisfaction, and intent to stay |
| Compensation, attendance, and training | Average base salary, total compensation, attendance and absence measures, training hours, training cost, and training completion measures |
| Insight text | `Insight 1`, `Insight 2`, `Insight 3`, `Data & AI + Cloud Workforce %`, and `Top Location` provide formatted or derived values used by the Key Insights area |

The calculations use DAX functions including `DISTINCTCOUNT`, `CALCULATE`, `DIVIDE`, `AVERAGE`, `SUM`, `COUNTROWS`, `DATESYTD`, `DATEADD`, `REMOVEFILTERS`, `FILTER`, and `TOPN`. For example, `Attrition Rate` divides employee exits by total employees, while `Headcount Trend` counts employees hired on or before the selected date.

## Dashboard Structure

The report contains one page presented as a dashboard-style workforce overview:

1. KPI cards summarize workforce size, active/inactive status, exits, and attrition.
2. A headcount trend visual shows workforce development over the report's date context.
3. An employee movement chart compares lifecycle event categories on a year-to-date basis.
4. Department, location, and employee-type visuals show workforce composition.
5. The Key Insights section displays formatted trend, workforce, location, and attrition observations.
6. Slicers provide filtering by year, quarter, department, city/location, employee status, and employment type. The Clear Filters button resets the report filters.

## Technology and Tools

- Microsoft Power BI Desktop
- Power BI Project (`.pbip`) format
- Power BI report definition (`.pbir`) and semantic model definition (`.pbism`)
- DAX measures
- Power Query/M import partitions using CSV files
- Git-compatible project structure for source control

## Project Structure

```text
powerbi/
├── Enterprise_Workforce_Intelligence.pbip
├── Enterprise_Workforce_Intelligence.Report/
│   ├── definition.pbir
│   ├── definition/
│   │   └── pages/
│   └── StaticResources/
├── Enterprise_Workforce_Intelligence.SemanticModel/
│   ├── definition.pbism
│   ├── definition/
│   │   ├── model.tmdl
│   │   ├── relationships.tmdl
│   │   └── tables/
│   └── .pbi/
├── Enterprise_Workforce_Intelligence/
│   ├── README.md
│   ├── .gitattributes
│   └── .gitignore
└── .gitignore
```

## Insights

The dashboard enables users to:

- Compare total, active, and inactive workforce levels.
- Identify how employees are distributed across departments, locations, and employment types.
- Review the relative volume of hires, promotions, transfers, exits, and returns.
- Observe headcount direction and year-to-date workforce movement.
- Assess the current attrition rate and its change versus the previous year.
- Review supporting workforce indicators such as performance, engagement, compensation, attendance, and training through the model's measures and filters.

These are analytical views provided by the report; the repository does not document a specific business result or conclusion from the underlying data.

## How to Open the Project

1. Install a version of Microsoft Power BI Desktop that supports Power BI Projects.
2. Open `Enterprise_Workforce_Intelligence.pbip` from the project root.
3. Allow Power BI Desktop to load the report and its referenced semantic model.
4. If a refresh is required, review the Power Query/M source definitions. The current model references CSV files through local file paths outside this project folder, so those source files must be available or the paths must be updated for the local environment.

## GitHub / Version Control

The report is maintained in Power BI Project format rather than as a single binary `.pbix` file. The `.pbip` entry point references separate report and semantic model artifacts, while the report definitions, TMDL tables, relationships, and DAX measures remain visible as project files. This structure is suitable for Git-based version control and review in a GitHub repository.

## Future Enhancements

Potential enhancements, not current functionality, include:

- Add dedicated report pages for deeper performance, engagement, compensation, attendance, or training analysis.
- Replace machine-specific CSV paths with a portable or parameterized data-source configuration.
- Add documented data-refresh and validation instructions for contributors.
- Add automated checks for model-definition changes before publishing updates.

## Author

Jeffrey
