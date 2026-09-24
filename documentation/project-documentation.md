# Project Documentation

**Project:** Student Sleep & Lifestyle Analysis
**Author:** Veerabhadra Chary

## 1. Dataset

A student-level survey-style dataset of **3,000 students** and 15 variables covering demographics (age, gender, education level), lifestyle (sleep, screen time, social media, study, exercise, caffeine, sleep-app use), wellbeing (stress, anxiety, burnout) and academic performance (GPA). Full column descriptions and observed value ranges are in [data-dictionary.md](data-dictionary.md).

## 2. Data cleaning

Checks run on `data/student_sleep_mental_health_2026.csv`:

| Check | Result |
|---|---|
| Missing values | 0 |
| Duplicate rows | 0 |
| Unique `student_id` | Yes (3,000 distinct) |
| Numeric columns | All numeric, within plausible ranges (age 14–29, stress 1–10, anxiety 1–10, GPA 1.97–4.00) |
| Boolean columns | `uses_sleep_app`, `feels_burned_out` stored as TRUE/FALSE |

No rows were removed or altered. The report adds four derived columns in the model (`Sleep Band`, `GPA Band`, `Burnout Status`, `Sleep App User`); see the data dictionary.

## 3. Data model

- **`student_sleep`** — the single data table (one row per student).
- **`measure`** — a measures-only table holding the report's DAX measures.

Every dimension used by a visual (gender, education level, stress level, bands, flags) comes from `student_sleep`, so the model works as a single-table (flat) model and no relationships between tables are required by any visual.

## 4. Important DAX measures

14 named measures cover the KPIs (Total Students, Average GPA / Sleep Hours / Anxiety Score / Screen Time / Study Hours / Exercise Hours / Caffeine Drinks / Stress Level), burnout (Burnout Rate, Burnout Rate %, Burnout Rate by Stress) and GPA by group. See [dax-measures.md](dax-measures.md) for the inventory, reference values and a query to export the formulas.

## 5. Dashboard pages

The report has six 1920 × 1080 pages, all using the same look (a custom theme on the Fluent 2 base theme). Navigation is through the page tabs at the bottom of Power BI.

### 01. Executive Overview
*Screenshot file:* `screenshots/page-01-executive-overview.png`  ·  *On-page title:* “Student Sleep & Mental Health — Executive Overview”

One-screen summary of the whole student population.

- Slicers (dropdown): Gender, Educational level, Stress level
- KPI cards: Burnout Rate %, Average Screen Time, Average Anxiety Score, Average Sleep Hours, Average GPA, Total Students
- Column charts: Students by Gender; Students by education level; Students by stress level; Average GPA by Gender; Average GPA by Education Level
- Pie chart: students by burnout flag (`feels_burned_out`)

### 02. Lifestyle Analysis
*Screenshot file:* `screenshots/page-02-sleep-analysis.png`  ·  *On-page title:* “Student Sleep & Lifestyle — Lifestyle Analysis”

How daily habits relate to sleep duration.

- Slicers (dropdown): Gender, Stress level, Educational level, Uses sleep app
- KPI cards: Average Study Hours, Average Screen Time, Average Caffeine Drinks, Average Exercise Hours, Average Sleep Hours
- Column chart: Student Distribution by Sleep Duration (`Sleep Band`)
- Scatter charts with trend lines: Screen Time vs Sleep Duration; Social Media Usage vs Sleep Duration (both coloured by burnout flag); Exercise vs Sleep Duration
- Column charts: Caffeine Intake vs Sleep; Sleep App Users vs Non-Users

### 03. Behavioral Analysis
*Screenshot file:* `screenshots/page-03-behavioral-analysis.png`  ·  *On-page title:* “Student Mental Health & Burnout — Behavioral Analysis”

Stress, anxiety and burnout patterns.

- Slicers (dropdown, synced with pages 4–6): Gender, Stress level, Educational level, Uses sleep app
- KPI cards: Average Sleep Hours, Burnout Rate, Average Stress Level, Average Anxiety Score, Average GPA
- Donut chart: Burnout Distribution (`Burnout Status`)
- Scatter chart: anxiety score vs average stress level
- Column charts: Stress Level vs Sleep Duration; Burnout Rate by Stress Level

### 04. Performance Analysis
*Screenshot file:* `screenshots/page-04-health-analysis.png`  ·  *On-page title:* “Student Academic Performance — Performance Analysis”

How sleep, study time and burnout relate to GPA.

- Slicers (dropdown, synced): Gender, Stress level, Educational level, Uses sleep app
- KPI cards: Average Stress Level, Average Sleep Hours, Average Anxiety Score, Average Study Hours, Average GPA
- Column chart: Student GPA Distribution (`GPA Band`)
- Scatter charts with trend lines: Study Hours vs GPA; Sleep hours vs GPA by `Burnout Status`
- Column chart: average GPA by `Burnout Status`

### 05. Student Segmentation
*Screenshot file:* `screenshots/page-05-user-analysis.png`  ·  *On-page title:* “Student Segmentation — Behavioral Profiles”

Behavioural profiles by stress level and burnout status.

- Slicers (dropdown, synced): Gender, Stress level, Educational level, Uses sleep app
- KPI cards: Total Students, Average Stress Level, Average Sleep Hours, Average Anxiety Score, Average GPA
- Column charts: student count by stress level; total sleep hours by `Burnout Status`
- Line chart: average sleep by stress level
- Scatter chart with trend line: anxiety score vs average GPA

### 06. Insights & Recommendations
*Screenshot file:* `screenshots/page-06-insights-overview.png`  ·  *On-page title:* “Insights — Key Findings & Recommendations”

Summary of findings, with a profile table and written recommendations.

- Slicers (dropdown, synced): Gender, Stress level, Educational level, Uses sleep app
- KPI cards: Total Students, Burnout Rate, Average GPA, Average Anxiety Score, plus an average-sleep card
- Column charts: Average Sleep by Burnout Status; Average Stress by Burnout Status
- Table: Student Profile by Burnout Status (average stress, sleep, GPA, study hours, anxiety)
- Text box with five key findings (burnout prevalence ≈ 68 %; sleep and wellbeing; stress and burnout; academic performance; lifestyle factors)

## 6. Filters and slicers

- All slicers are **dropdown** slicers.
- **Executive Overview** has three slicers (Gender, Educational level, Stress level). **Lifestyle Analysis** has four (Gender, Stress level, Educational level, Uses sleep app). Slicers on these two pages are not synced with other pages.
- On pages **3–6** the four slicers are **synced**: a selection made on one page carries to the others (sync groups: gender, stress_level, education_level, uses_sleep_app).
- Slicers cross-filter the KPI cards and charts on their page; clicking a chart element also cross-filters the other visuals (Power BI default interaction).
- Use **Ctrl + click** to multi-select in a chart; use *Clear selections* in the dropdown to reset.

## 7. Tooltips

The report uses Power BI's standard (enhanced) tooltips with extra fields added to the tooltip well on the **Lifestyle Analysis** charts — Screen Time vs Sleep, Social Media vs Sleep, Exercise vs Sleep, Caffeine Intake vs Sleep and Sleep App Users vs Non-Users — showing, depending on the chart, the student count and totals of sleep hours, stress and anxiety. There are no custom report-page tooltips.

## 8. Drill-through, bookmarks and buttons

The report **does not use** drill-through pages, bookmarks, page-navigation buttons or hidden pages. Interactivity comes from slicers, cross-filtering, tooltips and scatter-chart trend lines.

## 9. Key insights

Calculated from the CSV (unfiltered):

- **Burnout is widespread.** 2,039 of 3,000 students (68.0%) report feeling burned out.
- **Burned-out students sleep less.** Average sleep is 7.16 h for burned-out students vs 7.96 h for the rest; 31.4% of all students average under 7 hours.
- **Stress is the sharpest dividing line.** Average stress is 8.07 (burned out) vs 5.40; in this dataset the burnout flag is TRUE for every student with stress ≥ 7 and FALSE for every student with stress ≤ 6.
- **Sleep and grades move together.** GPA is 3.13 for burned-out students vs 3.49; the correlation between sleep hours and GPA is +0.52, and between stress and GPA -0.56.
- **Screens and social media cost sleep.** Screen time vs sleep correlation is -0.59; social-media time vs sleep is -0.45. Burned-out students average 7.10 h of screen time vs 5.21 h.
- **Stress and anxiety rise together** (correlation +0.74); exercise is mildly protective (exercise vs stress -0.29).
- **No visible effect** of sleep-app use (average sleep 7.42 h for users vs 7.41 h for non-users), caffeine (correlation with sleep +0.00) or study hours (correlation with GPA +0.00).
- **Little difference across groups.** Average GPA is between 3.24 and 3.26 across genders and between 3.22 and 3.25 across education levels; burnout is 69.8% for undergraduates vs 65.5% (high school) and 65.8% (graduate).

> **Interpretation note:** these are correlations in a single cross-sectional sample. The perfect split of burnout at stress 7 and the near-zero effects of several lifestyle factors suggest the data may be synthetic or derived, so treat the findings as illustrative rather than causal.

## 10. How to refresh the report

1. Open the PBIX in Power BI Desktop (Windows).
2. If Power BI reports a missing file or asks for credentials, choose **Home → Transform data → Data source settings → Change Source…** and point the source to `data/student_sleep_mental_health_2026.csv` in your local clone.
3. Click **Home → Refresh**.
4. To load new data: replace the CSV with a file that has **exactly the same column names and types** (see the data dictionary), then refresh. Calculated columns and measures recalculate automatically.
5. Verify with the validation query in [dax-measures.md](dax-measures.md), and check that *Total Students* matches the row count of the CSV.

## Maintenance notes

- **Screenshots** in `screenshots/` are currently layout placeholders; replace them with real exports from Power BI Desktop (same file names).
- Three details in the dashboard as delivered that you may want to tidy in Power BI Desktop: (a) on *Insights & Recommendations* the card titled “Average Anxiety Score” at top-centre displays **average sleep hours**; (b) on *Lifestyle Analysis* the “Average Study Hours” card appears twice; (c) the *Student Segmentation* chart “total sleep hours by Burnout Status” plots a **sum** of sleep hours, which is driven by group size rather than typical sleep (the average is shown on *Insights & Recommendations*).
