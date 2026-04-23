## SQL-User-Subscription-Analysis
SQL Analysis of yser acquisition trends. This project focuses on time-series data manipulation and extracting logic to identify peak signup periods, seasonal growth, and user behavior patterns overtime.

### Table Used
<img width="507" height="267" alt="1" src="https://github.com/user-attachments/assets/7fe41e3f-eb90-4fc3-9a11-fb86ad98b3d1" />

### Query

### 1. what is the username and year that users signed up?
```SQL
SELECT user_id, strftime('%Y', signup_timestamp) AS "signup year"
FROM User_Subscriptions;
```
<img width="152" height="182" alt="1" src="https://github.com/user-attachments/assets/1fd35eba-7f83-4f2d-bd17-2528025e7d76" />

### 2. which users signed up in March?
```SQL
SELECT user_id AS Users
FROM User_Subscriptions
WHERE strftime('%m', signup_timestamp) = '03';
```
<img width="73" height="85" alt="2" src="https://github.com/user-attachments/assets/a73366ce-860d-448d-b8d4-a2ab109724e4" />

### 3. How many users signed up each year?
```SQL
WITH New AS (
SELECT user_name AS Username, 
strftime ('%Y', signup_timestamp) AS Year
FROM User_Subscriptions
)

SELECT Year, COUNT(Year)
FROM New
GROUP BY Year;
```
<img width="149" height="84" alt="3" src="https://github.com/user-attachments/assets/486cefb7-16f0-4465-8af2-ec47ebdd8367" />

### 4. How many users signed up in the morning, afternoon and evening?
```SQL
WITH New AS(
SELECT user_name AS Username, 
strftime ('%H:%M:%S', signup_timestamp) AS Time
FROM User_Subscriptions
)

SELECT 
CASE 
WHEN Time BETWEEN '00:00:00' AND '11:59:59' THEN 'Morning'
WHEN Time BETWEEN '12:00:00' AND '16:59:59' THEN 'Afternoon'
ELSE 'Evening'
END AS "Time Category", COUNT("Time Category") AS "Number of Users"
FROM New
GROUP BY "Time Category"
ORDER BY "Number of Users" DESC;
```
<img width="223" height="111" alt="4" src="https://github.com/user-attachments/assets/414dcdec-d0bc-41d1-8ae4-42377609c4bf" />
