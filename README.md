# Social Media Impact on Life | Power BI Dashboard

## Project Overview

This project explores how social media usage relates to students' academic performance, sleep, stress, and mental health. The dataset is analyzed and visualized using **Microsoft Power BI**, with data preparation in **Power Query** and calculations using **DAX**.

> **Note:** The dataset provides observational associations. The dashboard cannot establish that social media use causes changes in GPA, sleep, stress, or mental health.

## Project Objectives

- Understand patterns of daily social-media use across platforms and student groups.
- Explore relationships between usage time, GPA, sleep, stress, and mental health.
- Compare late-night users with other students.
- Create an interactive, filterable Power BI report.
- Validate the dashboard values against the original CSV.

  ## Dataset

**Source file:** [`data/Social_media_impact_on_life.csv`](Social_media_impact_on_life.csv)

- **Rows:** 4,500
- **Columns:** 16
- **Missing cells:** 131 — 46 in `Perceived_Stress_Score`, 85 in `Academic_Performance_GPA`

| Column | Description |
|---|---|
| `Student_ID` | Student identifier |
| `Age` | Student age |
| `Gender` | Gender category |
| `Academic_Level` | Education level |
| `Primary_Platform` | Main social-media platform |
| `Daily_Usage_Hours` | Hours spent on social media daily |
| `Weekend_Extra_Hours` | Additional weekend usage hours |
| `Device_Type` | Primary device |
| `Sleep_Duration_Hours` | Daily sleep duration |
| `Sleep_Quality_Score` | Sleep quality rating |
| `Late_Night_Usage` | Late-night usage indicator |
| `Social_Comparison_Frequency` | Self-reported social-comparison frequency |
| `Perceived_Stress_Score` | Stress score |
| `Mental_Health_Index` | Mental-health index |
| `Academic_Performance_GPA` | Student GPA |
| `Overall_Impact` | Reported overall impact category |

## Dashboard 

The Power BI dashboard is included here: [`assets/social-media-impact-dashboard.jpeg`](assets/social-media-impact-bi.jpeg).
![Social media impact dashboard](assets/social-media-impact-bi.jpeg)
## Data Preparation in Power Query

1. Import the CSV using **Home → Get Data → Text/CSV → Transform Data**.
2. Check column quality, distribution, and data types.
3. Set usage, sleep, GPA, and stress fields to numeric types; keep categorical fields as text.
4. Check for duplicate values in `Student_ID` before removing any rows.
5. Keep missing GPA and stress values as `null` unless there is a documented reason to impute them. DAX `AVERAGE` excludes blanks.
6. Select **Close & Apply**.

## DAX Measures

Rename the imported table to **Social Media** before using these measures.

```dax
Total Students = DISTINCTCOUNT('Social Media'[Student_ID])
```

```dax
Average Daily Usage = AVERAGE('Social Media'[Daily_Usage_Hours])
```

```dax
Average Sleep Hours = AVERAGE('Social Media'[Sleep_Duration_Hours])
```

```dax
Average GPA = AVERAGE('Social Media'[Academic_Performance_GPA])
```

```dax
Average Stress Score = AVERAGE('Social Media'[Perceived_Stress_Score])
```

```dax
Average Mental Health Index = AVERAGE('Social Media'[Mental_Health_Index])
```
## Dashboard Pages and Visualizations

### 1. Social Media Overview

- **Cards:** Total Students, Average Daily Usage, Average GPA, Average Sleep Hours
- **Bar chart:** Student count by `Primary_Platform`
- **Donut chart:** Students by `Gender`
- **Column chart:** Students by `Age` or `Academic_Level`
- **Slicers:** Gender, Academic Level, Primary Platform, Device Type

### 2. Sleep and Mental Health

- **Scatter plot:** `Daily_Usage_Hours` versus `Sleep_Duration_Hours`
- **Column chart:** Average `Sleep_Quality_Score` by `Late_Night_Usage`
- **Bar chart:** Average `Perceived_Stress_Score` by usage group
- **Column chart:** Average `Mental_Health_Index` by `Social_Comparison_Frequency`

### 3. Academic Performance

- **Scatter plot:** `Daily_Usage_Hours` versus `Academic_Performance_GPA`, with `Gender` as the legend
- **Column chart:** Average GPA by usage group
- **Matrix:** Average GPA by gender and primary platform
- **Stacked column chart:** Student count by `Academic_Level`, split by `Overall_Impact`

## Descriptive Findings

These values are calculated directly from the original CSV before imputation.

| Metric | Result |
|---|---:|
| Total records | 4,500 |
| Average daily usage | 5.30 hours |
| Average sleep duration | 6.70 hours |
| Average GPA | 3.43 |
| Average perceived stress score | 13.51 |
| Average mental-health index | 79.87 |

### Primary Platforms

| Platform | Students |
|---|---:|
| Instagram | 1,453 |
| TikTok | 1,226 |
| YouTube | 818 |
| Snapchat | 472 |
| Reddit | 229 |
| X (Twitter) | 206 |
| LinkedIn | 96 |

### Reported Overall Impact

- **Beneficial:** 3,681 students
- **Neutral:** 654 students
- **Negative:** 165 students

### Main observations

- Instagram is the most common primary platform.
- Smartphone use is the dominant device category with 3,775 students.
- The negative-impact group has higher average usage and stress, and lower average sleep, mental-health index, and GPA.
- Daily usage is negatively correlated with GPA (`r = -0.710`) and sleep duration (`r = -0.716`).
- Daily usage is positively correlated with perceived stress (`r = 0.754`) and negatively correlated with the mental-health index (`r = -0.850`).

## Dashboard Comparison

| Dashboard item | Screenshot | CSV | Result |
|---|---:|---:|---|
| Count of `Student_ID` | 4.5K | 4,500 | Matches |
| Average daily usage | 5.30 | 5.2959 → 5.30 | Matches |
| Average academic performance | 3.43 | 3.4293 → 3.43 | Matches |
| Platform counts | Instagram 1,453; TikTok 1,226; YouTube 818; Snapchat 472; Reddit 229; X 206; LinkedIn 96 | Same counts | Matches |
| Age distribution | Highest at age 18 | Age 18 has 1,028 students | Matches |
| Gender distribution | Female largest, Male second | Female 2,234; Male 2,051 | Matches |

The screenshot chart titled **“Count of Device_Type by Primary_Platform”** appears to show platform counts rather than device counts. Rename it to **“Count of Students by Primary Platform”** or change the visual to use `Device_Type`.

