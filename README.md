# Bellabeat Smart Device Usage Analysis

## Project Overview

This project was completed as part of the Google Data Analytics Professional Certificate Capstone.

The objective of this analysis was to examine Fitbit smart device usage data to identify consumer usage patterns and generate insights that can help Bellabeat improve its marketing strategy. Using SQL, Google Sheets, and Tableau, the data was cleaned, analyzed, and visualized to uncover trends in physical activity and sleep behavior. The findings were then translated into actionable business recommendations for Bellabeat's marketing team.

## Business Task

Analyze Fitbit smart device usage data to identify consumer behavior patterns and generate data-driven insights that can help Bellabeat better understand its target customers and improve its marketing strategy.

## Stakeholders

- Urška Sršen – Bellabeat Co-founder and Chief Creative Officer
- Sando Mur – Bellabeat Co-founder
- Bellabeat Marketing Analytics Team

## Dataset

The analysis uses the **Fitbit Fitness Tracker Data** dataset available on Kaggle. The dataset was made available by Mobius under the **CC0: Public Domain** license and contains personal fitness tracker data collected from Fitbit users through Amazon Mechanical Turk between **March 12, 2016, and May 12, 2016**.

The dataset includes daily activity, sleep, calorie expenditure, distance, and activity intensity metrics that were used to analyze smart device usage patterns and generate business insights for Bellabeat.

### Data Limitations

- The dataset contains records for **33 unique Fitbit users**, representing a relatively small sample size.
- No demographic information (such as age, gender, or location) is available.
- The data was collected in **2016**, so user behavior may not reflect current smart device usage.
- Some records contain inconsistencies (for example, 1,440 sedentary minutes together with activity data), which were documented as limitations rather than removed.

## Tools Used

| Tool | Purpose |
|------|---------|
| **Google Sheets** | Data cleaning, validation, formatting, and |
| **SQL (Google BigQuery)** | Data exploration, querying, aggregation, and analysis |
| **Tableau Public** | Data visualization |

## Project Workflow

This project followed the six-step data analysis process from the Google Data Analytics Professional Certificate:

1. **Ask**
   - Defined the business task.
   - Identified stakeholders and project objectives.

2. **Prepare**
   - Evaluated the dataset's credibility and identified its limitations.
   - Selected the Daily Activity and Sleep datasets for analysis.

3. **Process**
   - Cleaned and validated the data in Google Sheets.
   - Removed duplicate records.
   - Checked for missing values.
   - Standardized column names.
   - Created additional fields to support analysis.

4. **Analyze**
   - Imported the cleaned datasets into Google BigQuery.
   - Used SQL to calculate summary statistics, identify activity trends, and examine relationships between activity, calories burned, and sleep duration.

5. **Share**
   - Designed a Tableau dashboard to communicate key insights.
   - Summarized findings using clear visualizations and business-focused interpretations.

6. **Act**
   - Developed marketing recommendations for Bellabeat based on the analytical findings.

  ## Key Analysis & Findings

The analysis identified several notable patterns in Fitbit users' activity and sleep behavior.

### 1. Daily Activity Summary

- Users averaged **7,638 daily steps**.
- Users traveled an average of **5.49 miles** per day.
- Average daily calorie expenditure was **2,304 calories**.
- Users spent an average of **991 minutes** per day being sedentary.

### 2. Weekly Activity Trends

- **Saturday** recorded the highest average daily step count (**8,153 steps**).
- **Tuesday** was the second most active day (**8,125 steps**).
- **Sunday** recorded the lowest average daily step count (**6,933 steps**).

These findings suggest users tend to be more physically active toward the beginning and end of the week.

### 3. Sleep Patterns

- Users slept an average of **419 minutes (approximately 7 hours)** each night.
- Users spent an average of **458 minutes** in bed.
- On average, users remained awake in bed for **39 minutes** before falling asleep or after waking.

### 4. Relationship Between Activity and Calories Burned

Users with higher activity levels consistently burned more calories.

| Activity Level | Average Steps | Average Calories |
|----------------|--------------:|-----------------:|
| Low Activity | 2,128 | 1,807 |
| Moderate Activity | 7,466 | 2,355 |
| High Activity | 13,337 | 2,744 |

This indicates a clear positive relationship between daily physical activity and calorie expenditure.

### 5. Relationship Between Activity and Sleep

Users with higher activity levels did not necessarily sleep longer.

| Activity Level | Average Steps | Average Sleep |
|----------------|--------------:|--------------:|
| Low Activity | 3,054 | 454 minutes |
| Moderate Activity | 7,591 | 422 minutes |
| High Activity | 12,526 | 396 minutes |

Within this dataset, higher daily activity levels were associated with shorter average sleep duration. This represents an observed association and should not be interpreted as a causal relationship.

## Tableau Dashboard

An Tableau dashboard was created to communicate the key findings from the analysis.

The dashboard includes:

- Average Daily Steps by Day of Week
- Average Calories Burned by Activity Level
- Average Sleep Duration by Activity Level
- Summary of Key Business Findings

> **Dashboard Preview**

[View the Bellabeat Smart Device Usage Analysis Dashboard](https://public.tableau.com/views/BellabeatSmartDeviceUsageAnalysis_17862825746700/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

## Business Recommendations

Based on the analysis, the following recommendations are proposed for Bellabeat:

### 1. Promote Daily Activity Challenges

Users recorded their highest average step counts on Saturdays and Tuesdays. Bellabeat can encourage consistent physical activity by introducing personalized step challenges, achievement badges, and reminders, especially on less active days such as Sundays.

### 2. Encourage a Balance Between Activity and Sleep

The analysis showed that users with higher activity levels did not necessarily sleep longer. Bellabeat can provide personalized wellness insights that encourage users to balance physical activity with healthy sleep habits through sleep reminders, recovery recommendations, and wellness notifications.

### 3. Deliver Personalized Health Insights

Higher activity levels were associated with greater calorie expenditure. Bellabeat can leverage this relationship by providing users with personalized reports that connect daily activity, calories burned, and sleep behavior, helping users better understand their overall wellness.

## Skills Demonstrated

### Data Preparation
- Data cleaning
- Data validation
- Duplicate detection and removal
- Data quality assessment
- Data transformation

### SQL & Data Analysis
- SQL (Google BigQuery)
- Data exploration
- Data aggregation
- Summary statistics
- JOIN operations
- CASE statements
- Trend analysis

### Data Visualization
- Tableau Public
- Dashboard design
- Data storytelling
- Business-focused visualizations

### Business & Communication
- Business problem solving
- Insight generation
- Business recommendations
- Analytical reporting

## About This Project

This project was completed as the capstone project for the Google Data Analytics Professional Certificate. It demonstrates my ability to complete an end-to-end data analysis project by defining a business problem, preparing and cleaning data, performing SQL analysis, creating data visualizations, and communicating actionable business insights through a professional report and interactive dashboard.

## Project Deliverables

This repository contains:

- **Bellabeat Smart Device Usage Analysis - Case Study.pdf** – Complete project report following the Google Data Analytics process.
- **bellabeat_analysis.sql** – SQL queries used for data exploration and analysis in Google BigQuery.
- **Tableau Dashboard** – Dashboard visualizing key findings from the analysis.

## Contact

**Nathaniel Obanor**

Thank you for taking the time to review my project. If you have any questions or feedback, feel free to connect with me.

- **GitHub:** https://github.com/obanath
