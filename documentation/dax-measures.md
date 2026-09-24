# DAX Measures

**Project:** Student Sleep & Lifestyle Analysis  **Author:** Veerabhadra Chary

The report has **14 named measures**, all stored in the `measure` table, and four derived columns on `student_sleep` (see [data-dictionary.md](data-dictionary.md)). Several KPI cards and charts on later pages use Power BI's built-in aggregations (average, count) of columns directly rather than a named measure.

## Measure inventory

*Purpose* is taken from each measure's name and the visuals that use it. *Reference value* is what the measure should return on the **full, unfiltered** CSV, calculated independently from `data/student_sleep_mental_health_2026.csv` — use it to check the report after any refresh or data change.

| Measure | Used on | Purpose | Reference value (no filters) |
|---|---|---|---|
| `Total Students` | Executive Overview (KPI card, 3 charts, pie) | Number of students in the current filter context. | 3,000 |
| `Average GPA` | Executive Overview, Behavioral, Performance, Insights (cards; pivot table) | Mean GPA. | 3.24 |
| `Average GPA by Gender` | Executive Overview (column chart) | Mean GPA per gender. | Female 3.25; Male 3.24; Non-binary 3.26; Prefer not to say 3.25 |
| `Average GPA by Education Level` | Executive Overview (column chart) | Mean GPA per education level. | Graduate 3.22; High School 3.25; Undergraduate 3.25 |
| `Average Sleep Hours` | Executive Overview, Lifestyle, Behavioral, Performance, Insights | Mean of `avg_sleep_hours`. | 7.41 |
| `Average Screen Time` | Executive Overview, Lifestyle | Mean of `screen_time_hours`. | 6.49 |
| `Average Anxiety Score` | Executive Overview, Performance, Insights (pivot table) | Mean of `anxiety_score`. | 7.15 |
| `Average Stress Level` | Behavioral, Performance, Insights (pivot table) | Mean of `stress_level`. | 7.22 |
| `Average Study Hours` | Lifestyle, Performance, Insights (pivot table) | Mean of `study_hours_per_day`. | 3.24 |
| `Average Exercise Hours` | Lifestyle | Mean of `exercise_hours_per_week`. | 3.54 |
| `Average Caffeine Drinks` | Lifestyle | Mean of `caffeine_drinks_per_day`. | 1.78 |
| `Burnout Rate` | Behavioral, Insights (KPI cards) | Share of students with `feels_burned_out` = TRUE. | 67.97% |
| `Burnout Rate %` | Executive Overview (KPI card) | Burnout share shown as a percentage. | 67.97% |
| `Burnout Rate by Stress` | Behavioral (column chart by `stress_level`) | Burnout share within each stress level. | 0% for stress 1–6, 100% for stress 7–10 |

## Exporting the exact DAX definitions

The formulas live inside the PBIX data model. To print them (for review, or to paste into this file):

1. Open the PBIX in Power BI Desktop.
2. Go to **DAX query view** (left rail).
3. Run:

```dax
EVALUATE INFO.MEASURES()
```

4. For the calculated columns, run:

```dax
EVALUATE INFO.COLUMNS()
```

   and read the *Expression* field.

## Validation query

Run this in **DAX query view** with no slicers applied; the results should match the reference values above.

```dax
EVALUATE
ROW(
    "Total Students", [Total Students],
    "Average GPA", [Average GPA],
    "Average Sleep Hours", [Average Sleep Hours],
    "Average Anxiety Score", [Average Anxiety Score],
    "Average Screen Time", [Average Screen Time],
    "Average Study Hours", [Average Study Hours],
    "Average Exercise Hours", [Average Exercise Hours],
    "Average Caffeine Drinks", [Average Caffeine Drinks],
    "Average Stress Level", [Average Stress Level],
    "Burnout Rate", [Burnout Rate]
)
```

## Built-in aggregations used directly in visuals

Power BI stores the aggregation used for each field. Where a card or chart is not driven by a named measure, it uses:

| Aggregation | Fields |
|---|---|
| Average | `avg_sleep_hours`, `stress_level`, `anxiety_score`, `gpa` |
| Count | `student_id` (student counts), `uses_sleep_app` |
| Sum | `stress_level`, `anxiety_score`, `avg_sleep_hours`, `exercise_hours_per_week`, `caffeine_drinks_per_day` (tooltips; one chart on *Student Segmentation*) |
