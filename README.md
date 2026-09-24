# Student Sleep & Lifestyle Analysis

An interactive **Power BI** dashboard that explores how sleep, screen time, study habits, stress and burnout relate to academic performance in a dataset of 3,000 students.

**Author:** Veerabhadra Chary

---

## Table of contents
- [Project overview](#project-overview)
- [Problem statement](#problem-statement)
- [Objectives](#objectives)
- [Dataset](#dataset)
- [Data preparation](#data-preparation)
- [Power BI data model](#power-bi-data-model)
- [DAX](#dax)
- [Dashboard pages](#dashboard-pages)
- [Features](#features)
- [Key insights](#key-insights)
- [Screenshots](#screenshots)
- [Project structure](#project-structure)
- [Setup instructions](#setup-instructions)
- [How to open the PBIX](#how-to-open-the-pbix)
- [Future improvements](#future-improvements)
- [Author](#author)

## Project overview
The dashboard turns a student survey-style dataset into a six-page report that moves from a high-level summary to lifestyle drivers, mental-health patterns, academic performance, student segments and written recommendations.

## Problem statement
Students who sleep poorly, spend long hours on screens and carry high stress are more likely to burn out and to see their grades suffer. Which habits are most closely linked to sleep, stress and burnout — and how strongly?

## Objectives
- Summarise the student population and headline KPIs (burnout rate, sleep, GPA, stress, anxiety).
- Show how screen time, social media, exercise, caffeine and sleep-app use relate to sleep duration.
- Compare burned-out and non-burned-out students on stress, anxiety, sleep and GPA.
- Assess how sleep and study time relate to academic performance.
- Present findings and recommendations in a form that non-technical readers can filter and explore.

## Dataset
[`data/student_sleep_mental_health_2026.csv`](data/student_sleep_mental_health_2026.csv) — 3,000 rows, 15 columns, one row per student: age, gender, education level, sleep, screen time, social media, study, exercise, caffeine, stress, anxiety, GPA, sleep-app use and burnout flag. See the [data dictionary](documentation/data-dictionary.md).

> The file does not state where the data came from or under what licence. Confirm this before republishing the data.

## Data preparation
The CSV has 0 missing values, 0 duplicate rows and a unique `student_id`, so no rows were removed. Inside the Power BI model, four derived columns are added — `Sleep Band`, `GPA Band`, `Burnout Status` and `Sleep App User` — to group students for charts. Details: [project documentation](documentation/project-documentation.md#2-data-cleaning).

## Power BI data model
A simple flat model with two tables:

| Table | Role |
|---|---|
| `student_sleep` | Student-level data plus calculated columns |
| `measure` | Container for the report's DAX measures |

## DAX
14 named measures: Total Students; Average GPA, Sleep Hours, Anxiety Score, Screen Time, Study Hours, Exercise Hours, Caffeine Drinks, Stress Level; Burnout Rate, Burnout Rate %, Burnout Rate by Stress; Average GPA by Gender and by Education Level. See [documentation/dax-measures.md](documentation/dax-measures.md) for reference values and a query to export the formulas.

## Dashboard pages

| # | Page | Focus |
|---|---|---|
| 01 | Executive Overview | One-screen summary of the whole student population. |
| 02 | Lifestyle Analysis | How daily habits relate to sleep duration. |
| 03 | Behavioral Analysis | Stress, anxiety and burnout patterns. |
| 04 | Performance Analysis | How sleep, study time and burnout relate to GPA. |
| 05 | Student Segmentation | Behavioural profiles by stress level and burnout status. |
| 06 | Insights & Recommendations | Summary of findings, with a profile table and written recommendations. |

## Features
- Six report pages at 1920 × 1080 with a consistent custom theme
- Dropdown slicers for gender, education level, stress level and sleep-app use; slicers on pages 3–6 stay in sync
- KPI cards, column, donut, pie, line and scatter charts, and a profile table
- Trend lines on scatter charts to show direction and strength of relationships
- Extra fields in tooltips on the Lifestyle Analysis charts
- Cross-filtering between visuals on every page

## Key insights
- **Burnout is widespread.** 2,039 of 3,000 students (68.0%) report feeling burned out.
- **Burned-out students sleep less.** Average sleep is 7.16 h for burned-out students vs 7.96 h for the rest; 31.4% of all students average under 7 hours.
- **Stress is the sharpest dividing line.** Average stress is 8.07 (burned out) vs 5.40; in this dataset the burnout flag is TRUE for every student with stress ≥ 7 and FALSE for every student with stress ≤ 6.
- **Sleep and grades move together.** GPA is 3.13 for burned-out students vs 3.49; the correlation between sleep hours and GPA is +0.52, and between stress and GPA -0.56.
- **Screens and social media cost sleep.** Screen time vs sleep correlation is -0.59; social-media time vs sleep is -0.45. Burned-out students average 7.10 h of screen time vs 5.21 h.
- **Stress and anxiety rise together** (correlation +0.74); exercise is mildly protective (exercise vs stress -0.29).
- **No visible effect** of sleep-app use (average sleep 7.42 h for users vs 7.41 h for non-users), caffeine (correlation with sleep +0.00) or study hours (correlation with GPA +0.00).
- **Little difference across groups.** Average GPA is between 3.24 and 3.26 across genders and between 3.22 and 3.25 across education levels; burnout is 69.8% for undergraduates vs 65.5% (high school) and 65.8% (graduate).

> **Interpretation note:** these are correlations in a single cross-sectional sample. The perfect split of burnout at stress 7 and the near-zero effects of several lifestyle factors suggest the data may be synthetic or derived, so treat the findings as illustrative rather than causal.

## Screenshots
### 1. Executive Overview
![Executive Overview]screenshots\page 1 Executive Overview.png"

### 2. Lifestyle Analysis
![Lifestyle Analysis]screenshots\page 2 Lifestyle Analysis.png"

### 3. Behavioral Analysis
![Behavioral Analysis]screenshots\page 3 Behavioral Analysis.png"

### 4. Performance Analysis
![Performance Analysis]\screenshots\page 4 Performance Analysis.png"

### 5. Student Segmentation
![Student Segmentation]\screenshots\page 5 Student Segmentation.png"

### 6. Insights & Recommendations
![Insights & Recommendations]\screenshots\page 6 Key findings & Recomendations.png"

<!-- The files in /screenshots are placeholders generated from the report layout. Replace them with Power BI exports using the same file names. -->

## Project structure
```
Veerabhadra-Chary-Student-Sleep-Lifestyle-Analysis/
├── powerbi/
│   └── Veerabhadra-Chary-Student-Sleep-Lifestyle-Analysis.pbix
├── data/
│   └── student_sleep_mental_health_2026.csv
├── screenshots/
│   ├── page-01-executive-overview.png
│   ├── page-02-sleep-analysis.png
│   ├── page-03-behavioral-analysis.png
│   ├── page-04-health-analysis.png
│   ├── page-05-user-analysis.png
│   └── page-06-insights-overview.png
├── documentation/
│   ├── project-documentation.md
│   ├── data-dictionary.md
│   └── dax-measures.md
├── README.md
├── .gitignore
└── LICENSE
```

## Setup instructions
1. Install **Power BI Desktop** (Windows, current release) from Microsoft.
2. Clone or download this repository.
3. Keep the folder structure as shown above.

## How to open the PBIX
1. Double-click `powerbi/Veerabhadra-Chary-Student-Sleep-Lifestyle-Analysis.pbix`, or use **File → Open report** in Power BI Desktop.
2. The report opens with its data already loaded. Use the page tabs at the bottom to move between the six pages.
3. To refresh, or if Power BI asks for the data source, point it to `data/student_sleep_mental_health_2026.csv` via **Home → Transform data → Data source settings → Change Source…**, then click **Refresh**. More detail is in the [documentation](documentation/project-documentation.md#10-how-to-refresh-the-report).

## Future improvements
- Add page-navigation buttons and a report home page
- Add drill-through pages for individual student segments
- Add bookmarks for “high-stress” and “low-sleep” views
- Add a custom tooltip page
- Add simple statistical tests or a regression to quantify relationships
- Publish to the Power BI Service and schedule a refresh from a hosted data source

## Author
**Veerabhadra Chary**

## License
Released under the [MIT License](LICENSE).
"# Student-Sleep-and-mental-health-" 
