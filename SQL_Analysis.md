# Bellabeat SQL Analysis

## Overview

SQL was used in Google BigQuery to explore the cleaned Fitbit datasets, validate the imported data, calculate summary statistics, identify activity trends, and examine relationships between physical activity, calorie expenditure, and sleep.

The analysis was designed to answer five business questions that support Bellabeat's marketing strategy.

---

## Dataset Exploration

Before answering the business questions, the dataset was explored to verify the number of records, unique users, and date range.

### Number of Records

The `daily_activity` table contained **940 records**, confirming that all records from the cleaned dataset were successfully imported into BigQuery.

### Unique Users

The analysis identified **33 unique Fitbit users**.

This differed from the 30 users referenced in the original case study documentation and was documented as a limitation of the dataset.

### Date Range

The activity data covered the period from **April 12, 2016 to May 12, 2016**, representing approximately one month of consecutive activity data.

---

# Business Question 1

## How active are Fitbit users on average?

The first analysis calculated the average daily steps, distance traveled, calories burned, and activity minutes recorded by Fitbit users.

### SQL Query

```sql
SELECT
    ROUND(AVG(total_steps), 0) AS average_steps,
    ROUND(AVG(total_distance), 2) AS average_distance,
    ROUND(AVG(calories), 0) AS average_calories,
    ROUND(AVG(very_active_minutes), 0) AS average_very_active_minutes,
    ROUND(AVG(fairly_active_minutes), 0) AS average_fairly_active_minutes,
    ROUND(AVG(lightly_active_minutes), 0) AS average_lightly_active_minutes,
    ROUND(AVG(sedentary_minutes), 0) AS average_sedentary_minutes
FROM `capstone250.Fitbit.daily_activity`;
Results
Metric	Average
Daily steps	7,638
Daily distance	5.49 miles
Calories burned	2,304
Very active minutes	21
Fairly active minutes	14
Lightly active minutes	193
Sedentary minutes	991
Insight

Fitbit users recorded an average of 7,638 steps and traveled approximately 5.49 miles per day, while burning approximately 2,304 calories.

The results indicate moderate levels of daily physical activity within the dataset, although users also spent a substantial amount of time sedentary.

Business Question 2
Which days of the week are users most active?

This analysis compared average daily steps and calorie expenditure across the seven days of the week to identify when Fitbit users were most and least active.

SQL Query
SELECT
    day_of_week,
    ROUND(AVG(total_steps), 0) AS average_steps,
    ROUND(AVG(calories), 0) AS average_calories
FROM `capstone250.Fitbit.daily_activity`
GROUP BY day_of_week
ORDER BY average_steps DESC;
Results
Day	Average Steps	Average Calories
Saturday	8,153	2,355
Tuesday	8,125	2,356
Monday	7,781	2,324
Wednesday	7,559	2,303
Friday	7,448	2,332
Thursday	7,406	2,200
Sunday	6,933	2,263
Insight

Saturday recorded the highest average daily step count at 8,153 steps, closely followed by Tuesday at 8,125 steps.

Sunday recorded the lowest average at 6,933 steps.

The variation across the week suggests that user activity changes depending on the day. Bellabeat could use this pattern to encourage consistent movement through targeted reminders, challenges, or activity prompts on lower-activity days.

Business Question 3
How much sleep do Fitbit users get on average?

This analysis examined average sleep duration, average time spent in bed, and the average difference between time in bed and actual sleep duration.

SQL Query
SELECT
    ROUND(AVG(total_minutes_asleep), 0) AS average_minutes_asleep,
    ROUND(AVG(total_time_in_bed), 0) AS average_minutes_in_bed,
    ROUND(
        AVG(total_time_in_bed - total_minutes_asleep),
        0
    ) AS average_minutes_awake_in_bed
FROM `capstone250.Fitbit.sleep_day`;
Results
Metric	Average
Minutes asleep	419 minutes
Time in bed	458 minutes
Awake in bed	39 minutes

419 minutes ≈ 7 hours of sleep

458 minutes ≈ 7 hours 38 minutes in bed

Insight

Users slept for approximately 7 hours per night on average while spending approximately 7 hours and 38 minutes in bed.

The difference of approximately 39 minutes represents time spent in bed while not asleep. This may reflect time taken to fall asleep, periods of waking during the night, or remaining in bed after waking.

This finding suggests an opportunity for Bellabeat to provide users with more detailed sleep insights, such as sleep efficiency and personalized sleep recommendations.

Business Question 4
Do users who take more steps burn more calories?

To examine the relationship between physical activity and calorie expenditure, daily activity records were grouped into three activity levels based on daily step count:

Low Activity: fewer than 5,000 steps
Moderate Activity: 5,000–9,999 steps
High Activity: 10,000 steps or more
SQL Query
SELECT
    CASE
        WHEN total_steps < 5000 THEN 'Low Activity'
        WHEN total_steps BETWEEN 5000 AND 9999 THEN 'Moderate Activity'
        ELSE 'High Activity'
    END AS activity_level,
    COUNT(*) AS number_of_days,
    ROUND(AVG(total_steps), 0) AS average_steps,
    ROUND(AVG(calories), 0) AS average_calories
FROM `capstone250.Fitbit.daily_activity`
GROUP BY activity_level
ORDER BY average_steps;
Results
Activity Level	Number of Days	Average Steps	Average Calories
Low Activity	303	2,128	1,807
Moderate Activity	334	7,466	2,355
High Activity	303	13,337	2,744
Insight

The results show a clear positive relationship between daily step count and calorie expenditure.

Users in the high-activity group averaged 13,337 steps and approximately 2,744 calories per day, compared with 2,128 steps and 1,807 calories among users in the low-activity group.

This suggests that encouraging users to increase their daily movement may also increase overall calorie expenditure.

Business Question 5
Do users with higher daily activity levels tend to sleep longer?

This analysis examined whether daily activity levels were associated with sleep duration.

The daily_activity and sleep_day datasets were joined using user ID and activity date.

SQL Query
SELECT
    CASE
        WHEN d.total_steps < 5000 THEN 'Low Activity'
        WHEN d.total_steps BETWEEN 5000 AND 9999 THEN 'Moderate Activity'
        ELSE 'High Activity'
    END AS activity_level,
    COUNT(*) AS number_of_days,
    ROUND(AVG(d.total_steps), 0) AS average_steps,
    ROUND(AVG(s.total_minutes_asleep), 0) AS average_minutes_asleep
FROM `capstone250.Fitbit.daily_activity` AS d
INNER JOIN `capstone250.Fitbit.sleep_day` AS s
    ON d.id = s.id
    AND d.activity_date = DATE(s.sleep_day)
GROUP BY activity_level
ORDER BY average_steps;
Results
Activity Level	Number of Days	Average Steps	Average Minutes Asleep
Low Activity	96	3,054	454
Moderate Activity	149	7,591	422
High Activity	165	12,526	396
Insight

Users in the high-activity group averaged 12,526 steps per day but slept approximately 396 minutes (6 hours 36 minutes).

In comparison, users in the low-activity group averaged 3,054 steps and slept approximately 454 minutes (7 hours 34 minutes).

Within this dataset, higher daily activity levels were associated with shorter average sleep duration.

However, this finding represents an association rather than a causal relationship. The dataset does not contain additional factors such as age, occupation, health status, or lifestyle that could influence sleep duration.

This suggests an opportunity for Bellabeat to encourage users to balance physical activity with healthy sleep habits.

Summary of Key Findings

The SQL analysis produced several important findings:

Fitbit users averaged 7,638 daily steps.
Users traveled approximately 5.49 miles per day.
Average daily calorie expenditure was approximately 2,304 calories.
Saturday recorded the highest average daily steps at 8,153.
Sunday recorded the lowest average daily steps at 6,933.
Users slept approximately 419 minutes (7 hours) per night.
Users spent approximately 39 minutes awake while in bed.
Higher activity levels were associated with higher calorie expenditure.
Higher activity levels were associated with shorter average sleep duration in this dataset.
SQL Techniques Demonstrated

The analysis used several SQL techniques, including:

SELECT
COUNT()
COUNT(DISTINCT)
AVG()
MIN()
MAX()
ROUND()
CASE WHEN
GROUP BY
ORDER BY
INNER JOIN
Date functions and transformations
Conditional categorization
Aggregation and comparative analysis
Business Implications

The findings suggest several opportunities for Bellabeat:

Encourage consistent daily activity through reminders, challenges, and personalized activity goals.
Promote balanced activity and sleep habits, particularly because higher activity levels were associated with shorter sleep duration.
Provide more detailed sleep insights, including sleep efficiency and personalized recommendations.
Use activity-based personalization to deliver more relevant recommendations to users with different activity levels.
Conclusion

The SQL analysis transformed cleaned Fitbit activity and sleep data into actionable business insights.

The results demonstrate how SQL can be used to explore user behavior, identify trends, compare groups, and support data-driven marketing recommendations.

The findings from this analysis were subsequently visualized in Tableau and incorporated into the complete Bellabeat case study.
