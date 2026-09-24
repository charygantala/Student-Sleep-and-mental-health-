# Data Dictionary

**Project:** Student Sleep & Lifestyle Analysis  **Author:** Veerabhadra Chary

## Source file

`data/student_sleep_mental_health_2026.csv` — 3,000 rows × 15 columns, one row per student, comma-separated with a header row.

Quality checks run on the CSV: **0 missing values, 0 duplicate rows, `student_id` is unique.** The records are anonymous; there are no names, e-mail addresses or other direct identifiers.

## Columns

| Column | Type | Description | Values in this file |
|---|---|---|---|
| `student_id` | Integer | Unique row identifier (1–3000); used for counting students. | 1 – 3000 |
| `age` | Integer | Student age in years. | 14 – 29 |
| `gender` | Text | Gender: Female, Male, Non-binary or Prefer not to say. | Female (1,410), Male (1,406), Non-binary (110), Prefer not to say (74) |
| `education_level` | Text | High School, Undergraduate or Graduate. | Undergraduate (1,681), High School (889), Graduate (430) |
| `avg_sleep_hours` | Decimal | Average nightly sleep, in hours. | 4.4 – 10.9 |
| `screen_time_hours` | Decimal | Daily total screen time, in hours. | 1 – 13.6 |
| `social_media_hours` | Decimal | Daily social-media time, in hours. | 0 – 9 |
| `study_hours_per_day` | Decimal | Daily study time, in hours. | 0 – 8.7 |
| `exercise_hours_per_week` | Decimal | Weekly exercise time, in hours. | 0 – 11.3 |
| `caffeine_drinks_per_day` | Integer | Number of caffeinated drinks per day. | 0 – 8 |
| `stress_level` | Integer | Stress level on a 1–10 scale (higher = more stress). | 1 – 10 |
| `anxiety_score` | Integer | Anxiety score on a 1–10 scale (higher = more anxiety). | 1 – 10 |
| `gpa` | Decimal | Grade point average on a 4.0 scale. | 1.97 – 4 |
| `uses_sleep_app` | Boolean | TRUE if the student uses a sleep-tracking app. | 1,028 TRUE / 1,972 FALSE |
| `feels_burned_out` | Boolean | TRUE if the student reports feeling burned out. | 2,039 TRUE / 961 FALSE |

## Tables in the Power BI model

| Table | Purpose |
|---|---|
| `student_sleep` | The student-level data (the 15 columns above) plus the calculated columns listed below. |
| `measure` | A measures-only table that holds the report's DAX measures (see [dax-measures.md](dax-measures.md)). |

## Derived columns used by the report

These columns do **not** exist in the CSV; they are created inside the Power BI model and are used by visuals.

| Column | Used for |
|---|---|
| `Sleep Band` | Groups students by sleep duration — *Student Distribution by Sleep Duration* (Lifestyle Analysis). |
| `GPA Band` | Groups students by GPA — *Student GPA Distribution* (Performance Analysis). |
| `Burnout Status` | Text label for `feels_burned_out` — burnout donut, GPA / sleep comparisons, the profile table. |
| `Sleep App User` (shown in visuals as *Sleep App Usage*) | Text label for `uses_sleep_app` (contains a *Non-Users* group) — *Sleep App Users vs Non-Users*. |

The exact band boundaries and labels are stored in the model. To list them, open the PBIX in Power BI Desktop → **DAX query view** and run `EVALUATE INFO.COLUMNS()` (calculated columns have their formula in the *Expression* field; if a column was added in Power Query instead, see **Transform data**).
