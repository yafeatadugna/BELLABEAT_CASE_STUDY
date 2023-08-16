# Project-Portfolio

SQL Script for Capstone Project


 -- After Cleaning the data, To get a better understanding, the datasets - daily activity and sleep day were merged using their primary key called “ID”.


SELECT
  *
FROM
  `my-project-1234-391913.dailyActivity.dailyActivity` AS daily_activity
INNER JOIN
  `my-project-1234-391913.dailyActivity.sleepday` AS sleep
ON
  dailyactivity.id = sleep.id




 -- To show the distribution of customers and users, for the first analysis I used the “steps” column to see if user were 
Beginners - < 40,000 steps in 2 month
Fairly Active - between 40,000 and 90,000 steps in 2 month
Very Active - > 90,000 step in 2 month
Data Points ranged between 2,366 - 156,880 steps in 2 month
 --This can help answer the business question by showing the distribution of smartwatch users.


SELECT
  id,
  CASE
    WHEN total_steps_per_day < 40000 THEN "Beginner"
    WHEN total_steps_per_day BETWEEN 40000 AND 90000 THEN "fairly_active"
  ELSE
  "Very_active"
END
  AS activity_level_per_total_steps
FROM (
  SELECT
    ID,
    total_steps/60 AS total_steps_per_day
  FROM (
    SELECT
      ID,
      SUM(TotalSteps) AS total_steps
    FROM
      `my-project-1234-391913.dailyActivity.ac_sleep`
    GROUP BY
      Id ))



Analysis:
Results show that there is an even distribution between Beginners and Ver_active users.


2.


-- Second Analysis was to Find the Average hours of sleep per user to show users sleeping distribution.


SELECT
  id,
  AVG(sleep_day) AS Average_sleep_per_day_in_hr
FROM (
  SELECT
    id,
    TotalMinutesAsleep/60 AS sleep_day
  FROM
    `my-project-1234-391913.dailyActivity.ac_sleep` )
GROUP BY
  Id





Analysis:
Result shows users on average sleep approximately 8 hours per night.


3.
-- third Analysis was to find Correlation between Sleep Hours and Total Calories Burned.
This shows the marketing team whether or NOT total calories burn is correlated with having a consistent and better sleep
In other words whether or not Carliers burn leads to having better sleep.
--This can help answer the business question by showing how users might use these two different features on a relationship basis.


SELECT
  id,
  SUM(Calories) AS total_calories_burn,
  AVG(sleep_day) AS Average_sleep_per_day_in_hr
FROM (
  SELECT
    id,
    Calories,
    TotalMinutesAsleep/60 AS sleep_day
  FROM
    `my-project-1234-391913.dailyActivity.ac_sleep` )
GROUP BY
  Id

 
Analysis:
Results show that Total Calories Burned and Average sleep per night is slightly correlated.
This shows that these two feature are often used together
Also shows that consist calorie burn leads to consistent sleep schedule


4.


-- Forth Analysis was to find Correlations between Total Calories Burned and Total Steps.
--This can help answer the business question by showing how users might use these two different features on a relationship basis.


SELECT
    id,
    total_calories,
    total_step
  FROM (
    SELECT
      id,
      SUM(Calories) AS total_calories,
      SUM(TotalSteps) AS total_step
    FROM
      `my-project-1234-391913.dailyActivity.ac_sleep`
  group by Id)





Analysis
Results showed there is a strong correlation between Total Calories Burned and Total Steps taken.
This shows that these two feature are often used together because they go hand to hand
This shows the strongest correlation and reason people use smartwatch devices. 
