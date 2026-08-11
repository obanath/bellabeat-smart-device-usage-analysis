SQL QUERIES

#To check the number of records in the daily_activity table

SELECT 
 COUNT(*)
FROM  `capstone250.Fitbit.daily_activity`;

#To check the number of unique users
SELECT  
  COUNT(DISTINCT id)
FROM `capstone250.Fitbit.daily_activity`

#To check for the date range
SELECT  
  MIN(Activity_Date),
  MAX(Activity_Date)
FROM `capstone250.Fitbit.daily_activity` 


#To get summary statistics

SELECT
    ROUND(AVG(Total_Steps), 0) AS average_steps,
    ROUND(AVG(total_distance), 2) AS average_distance,
    ROUND(AVG(calories), 0) AS average_calories,
    ROUND(AVG(very_active_minutes), 0) AS average_very_active_minutes,
    ROUND(AVG(fairly_active_minutes), 0) AS average_fairly_active_minutes,
    ROUND(AVG(lightly_active_minutes), 0) AS average_lightly_active_minutes,
    ROUND(AVG(sedentary_minutes), 0) AS average_sedentary_minutes
FROM `capstone250.Fitbit.daily_activity` 






#To get the days of the week where users are most active

SELECT
    day_of_week,
    ROUND(AVG(total_steps), 0) AS average_steps,
    ROUND(AVG(calories), 0) AS average_calories
FROM `capstone250.Fitbit.daily_activity`
GROUP BY day_of_week
ORDER BY average_steps DESC;



#To get how much sleep users are getting on average

SELECT
    ROUND(AVG(total_minutes_asleep), 0) AS average_minutes_asleep,
    ROUND(AVG(total_time_in_bed), 0) AS average_minutes_in_bed,
    ROUND(AVG(total_time_in_bed - total_minutes_asleep), 0) AS average_minutes_awake_in_bed
FROM capstone250.Fitbit.sleep_day;


#To get the relationship between daily steps(activity) and sleep

SELECT
    CASE
        WHEN d.total_steps < 5000 THEN 'Low Activity'
        WHEN d.total_steps BETWEEN 5000 AND 9999 THEN 'Moderate Activity'
        ELSE 'High Activity'
    END AS activity_level,
    COUNT(*) AS number_of_days,
    ROUND(AVG(d.total_steps),0) AS average_steps,
    ROUND(AVG(s.total_minutes_asleep),0) AS average_minutes_asleep
FROM `capstone250.Fitbit.daily_activity` AS d
INNER JOIN `capstone250.Fitbit.sleep_day` AS s
    ON d.id = s.id
    AND d.activity_date = DATE(s.sleep_day)
GROUP BY activity_level
ORDER BY average_steps;


#To get the relationship between steps and calories

SELECT
    CASE
        WHEN total_steps < 5000 THEN 'Low Activity'
        WHEN total_steps BETWEEN 5000 AND 9999 THEN 'Moderate Activity'
        ELSE 'High Activity'
    END AS activity_level,
    COUNT(*) AS number_of_days,
    ROUND(AVG(total_steps),0) AS average_steps,
    ROUND(AVG(calories),0) AS average_calories
FROM `capstone250.Fitbit.daily_activity`
GROUP BY activity_level
ORDER BY average_steps;



