﻿# Решение задач ['SQL 50'](https://leetcode.com/studyplan/top-sql-50/) на LeetCode


**Оглавление**

- [Решение задач 'SQL 50' на LeetCode](#решение-задач-sql-50-на-leetcode)
  - [Select](#select)
    - [Задача 1](#задача-1)
    - [Задача 2](#задача-2)
    - [Задача 3](#задача-3)
    - [Задача 4](#задача-4)
    - [Задача 5](#задача-5)
  - [Basic Joins](#basic-joins)
    - [Задача 6](#задача-6)
    - [Задача 7](#задача-7)
    - [Задача 8](#задача-8)
    - [Задача 9](#задача-9)
    - [Задача 10](#задача-10)
    - [Задача 11](#задача-11)
    - [Задача 12](#задача-12)
    - [Задача 13](#задача-13)
    - [Задача 14](#задача-14)
  - [Basic Aggregate Functions](#basic-aggregate-functions)
    - [Задача 15](#задача-15)
    - [Задача 16](#задача-16)
    - [Задача 17](#задача-17)
    - [Задача 18](#задача-18)
    - [Задача 19](#задача-19)
    - [Задача 20](#задача-20)
    - [Задача 21](#задача-21)
    - [Задача 22](#задача-22)
  - [Sorting and Grouping](#sorting-and-grouping)
    - [Задача 23](#задача-23)
    - [Задача 24](#задача-24)
    - [Задача 25](#задача-25)
    - [Задача 26](#задача-26)
    - [Задача 27](#задача-27)
    - [Задача 28](#задача-28)
    - [Задача 29](#задача-29)
  - [Advanced Select and Joins](#advanced-select-and-joins)
    - [Задача 30](#задача-30)
    - [Задача 31](#задача-31)
    - [Задача 32](#задача-32)
    - [Задача 33](#задача-33)
    - [Задача 34](#задача-34)
    - [Задача 35](#задача-35)
    - [Задача 36](#задача-36)
  - [Subqueries](#subqueries)
    - [Задача 37](#задача-37)
    - [Задача 38](#задача-38)
    - [Задача 39](#задача-39)
    - [Задача 40](#задача-40)
    - [Задача 41](#задача-41)
    - [Задача 42](#задача-42)
    - [Задача 43](#задача-43)
  - [Advanced String Functions / Regex / Clause](#advanced-string-functions--regex--clause)
    - [Задача 44](#задача-44)
    - [Задача 45](#задача-45)
    - [Задача 46](#задача-46)
    - [Задача 47](#задача-47)
    - [Задача 48](#задача-48)
    - [Задача 49](#задача-49)
    - [Задача 50](#задача-50)


## [Select](#решение-задач-sql-50-на-leetcode)


### [Задача 1](#решение-задач-sql-50-на-leetcode)

**1757. Recyclable and Low Fat Products**

Table: Products

| Column Name | Type    |
|-------------|---------|
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |

product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.
 

Write a solution to find the ids of products that are both low fat and recyclable.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Products table:

| product_id  | low_fats | recyclable |
|-------------|----------|------------|
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |

Output: 

| product_id  |
|-------------|
| 1           |
| 3           |

Explanation: Only products 1 and 3 are both low fat and recyclable.


**Решение:**

```SQL
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```


### [Задача 2](#решение-задач-sql-50-на-leetcode)

**584. Find Customer Referee**

Table: Customer

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

In SQL, id is the primary key column for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.
 
Find the names of the customer that are not referred by the customer with id = 2.

Return the result table in any order.

The result format is in the following example.
 
Example 1:

Input: 
Customer table:

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

Output: 

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |


**Решение:**

```SQL
SELECT name
FROM Customer
WHERE referee_id != 2
   OR referee_id IS NULL;
```


### [Задача 3](#решение-задач-sql-50-на-leetcode)

**595. Big Countries**

Table: World

| Column Name | Type    |
|-------------|---------|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |

name is the primary key (column with unique values) for this table.
Each row of this table gives information about the name of a country, the continent to which it belongs, its area, the population, and its GDP value.

A country is big if:

it has an area of at least three million (i.e., 3000000 km2), or
it has a population of at least twenty-five million (i.e., 25000000).
Write a solution to find the name, population, and area of the big countries.

Return the result table in any order.

The result format is in the following example.
 
Example 1:

Input: 
World table:

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

Output: 

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |


**Решение:**

```SQL
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
```


### [Задача 4](#решение-задач-sql-50-на-leetcode)

**1148. Article Views I**

Table: Views

| Column Name   | Type    |
|---------------|---------|
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |

There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.
 

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

The result format is in the following example.

Example 1:

Input: 
Views table:

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

Output: 

| id   |
|------|
| 4    |
| 7    |


**Решение:**

```SQL
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```


### [Задача 5](#решение-задач-sql-50-на-leetcode)

**1683. Invalid Tweets**

Table: Tweets

| Column Name    | Type    |
|----------------|---------|
| tweet_id       | int     |
| content        | varchar |

tweet_id is the primary key (column with unique values) for this table.
This table contains all the tweets in a social media app.

Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Tweets table:

| tweet_id | content                          |
|----------|----------------------------------|
| 1        | Vote for Biden                   |
| 2        | Let us make America great again! |

Output: 

| tweet_id |
|----------|
| 2        |

Explanation: 
Tweet 1 has length = 14. It is a valid tweet.
Tweet 2 has length = 32. It is an invalid tweet.


**Решение:**

```SQL
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```


## [Basic Joins](#решение-задач-sql-50-на-leetcode)


### [Задача 6](#решение-задач-sql-50-на-leetcode)

**1378. Replace Employee ID With The Unique Identifier**

Table: Employees

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| name          | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.

Table: EmployeeUNI

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| unique_id     | int     |

(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Employees table:

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

EmployeeUNI table:

| id | unique_id |
|----|-----------|
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

Output: 

| unique_id | name     |
|-----------|----------|
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |

Explanation: 
Alice and Bob do not have a unique ID, We will show null instead.
The unique ID of Meir is 2.
The unique ID of Winston is 3.
The unique ID of Jonathan is 1.


**Решение:**

```SQL
SELECT eu.unique_id,
       e.name
FROM Employees AS e
LEFT JOIN EmployeeUNI AS eu ON e.id = eu.id;
```


### [Задача 7](#решение-задач-sql-50-на-leetcode)

**1068. Product Sales Analysis I**

Table: Sales

| Column Name | Type  |
|-------------|-------|
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |

(sale_id, year) is the primary key (combination of columns with unique values) of this table.
product_id is a foreign key (reference column) to Product table.
Each row of this table shows a sale on the product product_id in a certain year.
Note that the price is per unit.

Table: Product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the product name of each product.

Write a solution to report the product_name, year, and price for each sale_id in the Sales table.

Return the resulting table in any order.

The result format is in the following example.

Example 1:

Input: 
Sales table:

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

Product table:

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

Output: 

| product_name | year  | price |
|--------------|-------|-------|
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |

Explanation: 
From sale_id = 1, we can conclude that Nokia was sold for 5000 in the year 2008.
From sale_id = 2, we can conclude that Nokia was sold for 5000 in the year 2009.
From sale_id = 7, we can conclude that Apple was sold for 9000 in the year 2011.


**Решение:**

```SQL
SELECT product_name, year, price
FROM Sales AS s
    LEFT JOIN Product AS p ON s.product_id = p.product_id;
```


### [Задача 8](#решение-задач-sql-50-на-leetcode)

**1581. Customer Who Visited but Did Not Make Any Transactions**

Table: Visits

| Column Name | Type    |
|-------------|---------|
| visit_id    | int     |
| customer_id | int     |

visit_id is the column with unique values for this table.
This table contains information about the customers who visited the mall.

Table: Transactions

| Column Name    | Type    |
|----------------|---------|
| transaction_id | int     |
| visit_id       | int     |
| amount         | int     |

transaction_id is column with unique values for this table.
This table contains information about the transactions made during the visit_id.

Write a solution to find the IDs of the users who visited without making any transactions and the number of times they made these types of visits.

Return the result table sorted in any order.

The result format is in the following example.

Example 1:

Input: 
Visits

| visit_id | customer_id |
|----------|-------------|
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

Transactions

| transaction_id | visit_id | amount |
|----------------|----------|--------|
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |

Output: 

| customer_id | count_no_trans |
|-------------|----------------|
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |

Explanation: 
Customer with id = 23 visited the mall once and made one transaction during the visit with id = 12.
Customer with id = 9 visited the mall once and made one transaction during the visit with id = 13.
Customer with id = 30 visited the mall once and did not make any transactions.
Customer with id = 54 visited the mall three times. During 2 visits they did not make any transactions, and during one visit they made 3 transactions.
Customer with id = 96 visited the mall once and did not make any transactions.
As we can see, users with IDs 30 and 96 visited the mall one time without making any transactions. Also, user 54 visited the mall twice and did not make any transactions.


**Решение:**

```SQL
SELECT customer_id,
       COUNT(customer_id) AS count_no_trans
FROM Visits AS v
    LEFT JOIN Transactions AS t ON v.visit_id = t.visit_id
WHERE transaction_id IS NULL
GROUP BY customer_id;
```


### [Задача 9](#решение-задач-sql-50-на-leetcode)

**197. Rising Temperature**

Table: Weather

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| recordDate    | date    |
| temperature   | int     |

In SQL, id is the primary key for this table.
This table contains information about the temperature on a certain day.

Find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Weather table:

| id | recordDate | temperature |
|----|------------|-------------|
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |

Output: 

| id |
|----|
| 2  |
| 4  |

Explanation: 
In 2015-01-02, the temperature was higher than the previous day (10 -> 25).
In 2015-01-04, the temperature was higher than the previous day (20 -> 30).


**Решение:**

```SQL
SELECT  id
FROM (SELECT  id,
              recordDate,
              temperature,
              LAG(recordDate, 1) OVER (ORDER BY recordDate) AS date_prev,
              LAG(temperature, 1 ) OVER (ORDER BY recordDate) AS temp_prev
      FROM Weather) AS temp
WHERE (temperature - temp_prev) > 0
  AND DATEDIFF(recordDate, date_prev) = 1;
```


### [Задача 10](#решение-задач-sql-50-на-leetcode)

**1661. Average Time of Process per Machine**

Table: Activity

| Column Name    | Type    |
|----------------|---------|
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |

The table shows the user activities for a factory website.
(machine_id, process_id, activity_type) is the primary key (combination of columns with unique values) of this table.
machine_id is the ID of a machine.
process_id is the ID of a process running on the machine with ID machine_id.
activity_type is an ENUM (category) of type ('start', 'end').
timestamp is a float representing the current time in seconds.
'start' means the machine starts the process at the given timestamp and 'end' means the machine ends the process at the given timestamp.
The 'start' timestamp will always be before the 'end' timestamp for every (machine_id, process_id) pair.

There is a factory website that has several machines each running the same number of processes. Write a solution to find the average time each machine takes to complete a process.

The time to complete a process is the 'end' timestamp minus the 'start' timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run.

The resulting table should have the machine_id along with the average time as processing_time, which should be rounded to 3 decimal places.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Activity table:

| machine_id | process_id | activity_type | timestamp |
|------------|------------|---------------|-----------|
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     |
| 2          | 1          | end           | 5.000     |

Output: 

| machine_id | processing_time |
|------------|-----------------|
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |

Explanation: 
There are 3 machines running 2 processes each.
Machine 0's average time is ((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894
Machine 1's average time is ((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995
Machine 2's average time is ((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456


**Решение:**

```SQL
WITH
a1 AS (
    SELECT *
    FROM Activity
    WHERE activity_type = 'start'),
a2 AS (
    SELECT *
    FROM Activity
    WHERE activity_type = 'end')

SELECT  a1.machine_id,
        ROUND(AVG(a2.timestamp - a1.timestamp), 3) AS processing_time
FROM a1
    JOIN a2 ON a1.machine_id = a2.machine_id
            AND a1.process_id = a2.process_id
GROUP BY a1.machine_id;
```


### [Задача 11](#решение-задач-sql-50-на-leetcode)

**577. Employee Bonus**

Table: Employee

| Column Name | Type    |
|-------------|---------|
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |

empId is the primary key column for this table.
Each row of this table indicates the name and the ID of an employee in addition to their salary and the id of their manager.

Table: Bonus

| Column Name | Type |
|-------------|------|
| empId       | int  |
| bonus       | int  |

empId is the primary key column for this table.
empId is a foreign key to empId from the Employee table.
Each row of this table contains the id of an employee and their respective bonus.

Write an SQL query to report the name and bonus amount of each employee with a bonus less than 1000.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Employee table:

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

Bonus table:

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

Output: 

| name | bonus |
|------|-------|
| Brad | null  |
| John | null  |
| Dan  | 500   |


**Решение:**

```SQL
SELECT name, bonus
FROM Employee AS e
    LEFT JOIN Bonus AS b ON e.empId = b.empId
WHERE bonus < 1000
    OR bonus IS NULL;
```


### [Задача 12](#решение-задач-sql-50-на-leetcode)

**1280. Students and Examinations**

Table: Students

| Column Name   | Type    |
|---------------|---------|
| student_id    | int     |
| student_name  | varchar |

student_id is the primary key (column with unique values) for this table.
Each row of this table contains the ID and the name of one student in the school.

Table: Subjects

| Column Name  | Type    |
|--------------|---------|
| subject_name | varchar |

subject_name is the primary key (column with unique values) for this table.
Each row of this table contains the name of one subject in the school.

Table: Examinations

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| subject_name | varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.
Each student from the Students table takes every course from the Subjects table.
Each row of this table indicates that a student with ID student_id attended the exam of subject_name.

Write a solution to find the number of times each student attended each exam.

Return the result table ordered by student_id and subject_name.

The result format is in the following example.

Example 1:

Input: 
Students table:

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

Subjects table:

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

Examinations table:

| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

Output: 

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

Explanation: 
The result table should contain all students and all subjects.
Alice attended the Math exam 3 times, the Physics exam 2 times, and the Programming exam 1 time.
Bob attended the Math exam 1 time, the Programming exam 1 time, and did not attend the Physics exam.
Alex did not attend any exams.
John attended the Math exam 1 time, the Physics exam 1 time, and the Programming exam 1 time.


**Решение:**

```SQL
WITH e AS(
SELECT  student_id,
        subject_name,
        COUNT(subject_name) AS attended_exams
FROM Examinations
GROUP BY student_id, subject_name)

SELECT  st.student_id,
        st.student_name,
        s.subject_name,
        CASE
            WHEN e.attended_exams IS NULL THEN 0
            ELSE e.attended_exams
        END AS attended_exams
FROM Students AS st
    CROSS JOIN Subjects AS s
    LEFT JOIN e ON st.student_id = e.student_id
                AND s.subject_name = e.subject_name
ORDER BY st.student_id, s.subject_name;
```


### [Задача 13](#решение-задач-sql-50-на-leetcode)

**570. Managers with at Least 5 Direct Reports**

Table: Employee

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

id is the primary key (column with unique values) for this table.
Each row of this table indicates the name of an employee, their department, and the id of their manager.
If managerId is null, then the employee does not have a manager.
No employee will be the manager of themself.

Write a solution to find managers with at least five direct reports.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Employee table:

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | None      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

Output: 

| name |
|------|
| John |


**Решение:**

```SQL
SELECT e.name
FROM (
        SELECT  managerId,
                COUNT(id) AS count
        FROM Employee
        GROUP BY managerId
        HAVING count >= 5
     ) AS temp
    JOIN Employee AS e ON temp.managerId = e.id;
```


### [Задача 14](#решение-задач-sql-50-на-leetcode)

**1934. Confirmation Rate**

Table: Signups

| Column Name    | Type     |
|----------------|----------|
| user_id        | int      |
| time_stamp     | datetime |

user_id is the primary key for this table.
Each row contains information about the signup time for the user with ID user_id.

Table: Confirmations

| Column Name    | Type     |
|----------------|----------|
| user_id        | int      |
| time_stamp     | datetime |
| action         | ENUM     |

(user_id, time_stamp) is the primary key for this table.
user_id is a foreign key with a reference to the Signups table.
action is an ENUM of the type ('confirmed', 'timeout')
Each row of this table indicates that the user with ID user_id requested a confirmation message at time_stamp and that confirmation message was either confirmed ('confirmed') or expired without confirming ('timeout').

The confirmation rate of a user is the number of 'confirmed' messages divided by the total number of requested confirmation messages. The confirmation rate of a user that did not request any confirmation messages is 0. Round the confirmation rate to two decimal places.

Write an SQL query to find the confirmation rate of each user.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Signups table:

| user_id | time_stamp          |
|---------|---------------------|
| 3       | 2020-03-21 10:16:13 |
| 7       | 2020-01-04 13:57:59 |
| 2       | 2020-07-29 23:09:44 |
| 6       | 2020-12-09 10:39:37 |

Confirmations table:

| user_id | time_stamp          | action    |
|---------|---------------------|-----------|
| 3       | 2021-01-06 03:30:46 | timeout   |
| 3       | 2021-07-14 14:00:00 | timeout   |
| 7       | 2021-06-12 11:57:29 | confirmed |
| 7       | 2021-06-13 12:58:28 | confirmed |
| 7       | 2021-06-14 13:59:27 | confirmed |
| 2       | 2021-01-22 00:00:00 | confirmed |
| 2       | 2021-02-28 23:59:59 | timeout   |

Output: 

| user_id | confirmation_rate |
|---------|-------------------|
| 6       | 0.00              |
| 3       | 0.00              |
| 7       | 1.00              |
| 2       | 0.50              |

Explanation: 
User 6 did not request any confirmation messages. The confirmation rate is 0.
User 3 made 2 requests and both timed out. The confirmation rate is 0.
User 7 made 3 requests and all were confirmed. The confirmation rate is 1.
User 2 made 2 requests where one was confirmed and the other timed out. The confirmation rate is 1 / 2 = 0.5.


**Решение:**

```SQL
WITH
con AS(
  SELECT  user_id,
          COUNT(user_id) AS count_con
  FROM Confirmations
  WHERE action = 'confirmed'
  GROUP BY user_id),
tot AS(
  SELECT  user_id,
          COUNT(user_id) AS count_tot
  FROM Confirmations
  GROUP BY user_id)

SELECT  sig.user_id,
        CASE
          WHEN count_tot IS NULL THEN 0
          WHEN count_con IS NULL THEN 0
          ELSE ROUND((count_con / count_tot), 2)
        END AS confirmation_rate
FROM Signups AS sig
  LEFT JOIN con ON sig.user_id=con.user_id
  LEFT JOIN tot ON sig.user_id=tot.user_id;
```



## [Basic Aggregate Functions](#решение-задач-sql-50-на-leetcode)


### [Задача 15](#решение-задач-sql-50-на-leetcode)

**620. Not Boring Movies**

Table: Cinema

| Column Name    | Type     |
|----------------|----------|
| id             | int      |
| movie          | varchar  |
| description    | varchar  |
| rating         | float    |

id is the primary key (column with unique values) for this table.
Each row contains information about the name of a movie, its genre, and its rating.
rating is a 2 decimal places float in the range [0, 10]

Write a solution to report the movies with an odd-numbered ID and a description that is not "boring".

Return the result table ordered by rating in descending order.

The result format is in the following example.

Example 1:

Input: 
Cinema table:

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | Fantacy     | 8.6    |
| 5  | House card | Interesting | 9.1    |

Output: 

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 5  | House card | Interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |

Explanation: 
We have three movies with odd-numbered IDs: 1, 3, and 5. The movie with ID = 3 is boring so we do not include it in the answer.

**Решение:**

```SQL
SELECT id, movie, description, rating
FROM Cinema
WHERE (id % 2) != 0
  AND description != 'boring'
ORDER BY rating DESC;
```


### [Задача 16](#решение-задач-sql-50-на-leetcode)

**1251. Average Selling Price**

Table: Prices

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| start_date    | date    |
| end_date      | date    |
| price         | int     |

(product_id, start_date, end_date) is the primary key for this table.
Each row of this table indicates the price of the product_id in the period from start_date to end_date.
For each product_id there will be no two overlapping periods. That means there will be no two intersecting periods for the same product_id.

Table: UnitsSold

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| purchase_date | date    |
| units         | int     |

There is no primary key for this table, it may contain duplicates.
Each row of this table indicates the date, units, and product_id of each product sold. 

Write an SQL query to find the average selling price for each product. average_price should be rounded to 2 decimal places.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Prices table:

| product_id | start_date | end_date   | price  |
|------------|------------|------------|--------|
| 1          | 2019-02-17 | 2019-02-28 | 5      |
| 1          | 2019-03-01 | 2019-03-22 | 20     |
| 2          | 2019-02-01 | 2019-02-20 | 15     |
| 2          | 2019-02-21 | 2019-03-31 | 30     |

UnitsSold table:

| product_id | purchase_date | units |
|------------|---------------|-------|
| 1          | 2019-02-25    | 100   |
| 1          | 2019-03-01    | 15    |
| 2          | 2019-02-10    | 200   |
| 2          | 2019-03-22    | 30    |

Output: 

| product_id | average_price |
|------------|---------------|
| 1          | 6.96          |
| 2          | 16.96         |

Explanation: 
Average selling price = Total Price of Product / Number of products sold.
Average selling price for product 1 = ((100 * 5) + (15 * 20)) / 115 = 6.96
Average selling price for product 2 = ((200 * 15) + (30 * 30)) / 230 = 16.96

**Решение:**

```SQL
SELECT  product_id,
        ROUND(SUM(temp.total) / SUM(temp.units), 2) AS average_price
FROM (
        SELECT  p.product_id,
                (price * units) AS total,
                units
        FROM Prices AS p
            JOIN UnitsSold AS u ON p.product_id=u.product_id
                                AND p.start_date <= u.purchase_date
                                AND p.end_date >= u.purchase_date
     ) AS temp
GROUP BY product_id;
```


### [Задача 17](#решение-задач-sql-50-на-leetcode)

**1075. Project Employees I**

Table: Project

| Column Name | Type    |
|-------------|---------|
| project_id  | int     |
| employee_id | int     |

(project_id, employee_id) is the primary key of this table.
employee_id is a foreign key to Employee table.
Each row of this table indicates that the employee with employee_id is working on the project with project_id.

Table: Employee

| Column Name      | Type    |
|------------------|---------|
| employee_id      | int     |
| name             | varchar |
| experience_years | int     |

employee_id is the primary key of this table. It's guaranteed that experience_years is not NULL.
Each row of this table contains information about one employee.

Write an SQL query that reports the average experience years of all the employees for each project, rounded to 2 digits.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Project table:

| project_id  | employee_id |
|-------------|-------------|
| 1           | 1           |
| 1           | 2           |
| 1           | 3           |
| 2           | 1           |
| 2           | 4           |

Employee table:

| employee_id | name   | experience_years |
|-------------|--------|------------------|
| 1           | Khaled | 3                |
| 2           | Ali    | 2                |
| 3           | John   | 1                |
| 4           | Doe    | 2                |

Output: 

| project_id  | average_years |
|-------------|---------------|
| 1           | 2.00          |
| 2           | 2.50          |

Explanation: The average experience years for the first project is (3 + 2 + 1) / 3 = 2.00 and for the second project is (3 + 2) / 2 = 2.50

**Решение:**

```SQL
SELECT  project_id,
        ROUND(AVG(experience_years), 2) AS average_years
FROM Project AS p
    JOIN Employee AS e ON p.employee_id=e.employee_id
GROUP BY project_id;
```


### [Задача 18](#решение-задач-sql-50-на-leetcode)

**1633. Percentage of Users Attended a Contest**

Table: Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| user_name   | varchar |

user_id is the primary key (column with unique values) for this table.
Each row of this table contains the name and the id of a user.

Table: Register

| Column Name | Type    |
|-------------|---------|
| contest_id  | int     |
| user_id     | int     |

(contest_id, user_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id of a user and the contest they registered into.

Write a solution to find the percentage of the users registered in each contest rounded to two decimals.

Return the result table ordered by percentage in descending order. In case of a tie, order it by contest_id in ascending order.

The result format is in the following example.

Example 1:

Input: 
Users table:

| user_id | user_name |
|---------|-----------|
| 6       | Alice     |
| 2       | Bob       |
| 7       | Alex      |

Register table:

| contest_id | user_id |
|------------|---------|
| 215        | 6       |
| 209        | 2       |
| 208        | 2       |
| 210        | 6       |
| 208        | 6       |
| 209        | 7       |
| 209        | 6       |
| 215        | 7       |
| 208        | 7       |
| 210        | 2       |
| 207        | 2       |
| 210        | 7       |

Output: 

| contest_id | percentage |
|------------|------------|
| 208        | 100.0      |
| 209        | 100.0      |
| 210        | 100.0      |
| 215        | 66.67      |
| 207        | 33.33      |

Explanation: 
All the users registered in contests 208, 209, and 210. The percentage is 100% and we sort them in the answer table by contest_id in ascending order.
Alice and Alex registered in contest 215 and the percentage is ((2/3) * 100) = 66.67%
Bob registered in contest 207 and the percentage is ((1/3) * 100) = 33.33%

**Решение:**

```SQL
SELECT  contest_id,
        ROUND(100 * COUNT(user_id) / (SELECT COUNT(user_id) FROM Users), 2) AS percentage
FROM Register
GROUP BY contest_id
ORDER BY percentage DESC, contest_id;
```


### [Задача 19](#решение-задач-sql-50-на-leetcode)

**1211. Queries Quality and Percentage**

Table: Queries

| Column Name | Type    |
|-------------|---------|
| query_name  | varchar |
| result      | varchar |
| position    | int     |
| rating      | int     |

This table may have duplicate rows.
This table contains information collected from some queries on a database.
The position column has a value from 1 to 500.
The rating column has a value from 1 to 5. Query with rating less than 3 is a poor query.

We define query quality as:

The average of the ratio between query rating and its position.

We also define poor query percentage as:

The percentage of all queries with rating less than 3.

Write a solution to find each query_name, the quality and poor_query_percentage.

Both quality and poor_query_percentage should be rounded to 2 decimal places.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Queries table:

| query_name | result            | position | rating |
|------------|-------------------|----------|--------|
| Dog        | Golden Retriever  | 1        | 5      |
| Dog        | German Shepherd   | 2        | 5      |
| Dog        | Mule              | 200      | 1      |
| Cat        | Shirazi           | 5        | 2      |
| Cat        | Siamese           | 3        | 3      |
| Cat        | Sphynx            | 7        | 4      |

Output: 

| query_name | quality | poor_query_percentage |
|------------|---------|-----------------------|
| Dog        | 2.50    | 33.33                 |
| Cat        | 0.66    | 33.33                 |

Explanation: 
Dog queries quality is ((5 / 1) + (5 / 2) + (1 / 200)) / 3 = 2.50
Dog queries poor_ query_percentage is (1 / 3) * 100 = 33.33

Cat queries quality equals ((2 / 5) + (3 / 3) + (4 / 7)) / 3 = 0.66
Cat queries poor_ query_percentage is (1 / 3) * 100 = 33.33

**Решение:**

```SQL
WITH
p AS(
SELECT  query_name,
        COUNT(rating) AS poor
FROM Queries
WHERE rating < 3
GROUP BY query_name)

SELECT  q.query_name,
        ROUND(AVG(rating / position), 2) AS quality,
        CASE
          WHEN poor IS NULL THEN 0
          ELSE ROUND(100 * poor / COUNT(rating), 2)
        END AS poor_query_percentage
FROM Queries AS q
  LEFT JOIN p ON q.query_name=p.query_name
GROUP BY query_name;
```


### [Задача 20](#решение-задач-sql-50-на-leetcode)

**1193. Monthly Transactions I**

Table: Transactions

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| country       | varchar |
| state         | enum    |
| amount        | int     |
| trans_date    | date    |

id is the primary key of this table.
The table has information about incoming transactions.
The state column is an enum of type ["approved", "declined"].

Write an SQL query to find for each month and country, the number of transactions and their total amount, the number of approved transactions and their total amount.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Transactions table:

| id   | country | state    | amount | trans_date |
|------|---------|----------|--------|------------|
| 121  | US      | approved | 1000   | 2018-12-18 |
| 122  | US      | declined | 2000   | 2018-12-19 |
| 123  | US      | approved | 2000   | 2019-01-01 |
| 124  | DE      | approved | 2000   | 2019-01-07 |

Output: 

| month    | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
|----------|---------|-------------|----------------|--------------------|-----------------------|
| 2018-12  | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01  | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01  | DE      | 1           | 1              | 2000               | 2000                  |

**Решение:**

```SQL
WITH
a AS(
  SELECT  INSERT(EXTRACT(YEAR_MONTH FROM trans_date), 5, 0, '-') AS month,
          country,
          COUNT(trans_date) AS approved_count,
          SUM(amount) AS approved_total_amount
  FROM Transactions
  WHERE state = 'approved'
  GROUP BY country, EXTRACT(YEAR_MONTH FROM trans_date)),

t AS(
  SELECT  INSERT(EXTRACT(YEAR_MONTH FROM trans_date), 5, 0, '-') AS month,
          country,
          COUNT(trans_date) AS trans_count,
          SUM(amount) AS trans_total_amount
  FROM Transactions
  GROUP BY country, EXTRACT(YEAR_MONTH FROM trans_date))

SELECT  t.month,
        t.country,
        trans_count,
        CASE
          WHEN approved_count IS NULL THEN 0
          ELSE approved_count
        END AS approved_count,
        trans_total_amount,
        CASE
          WHEN approved_total_amount IS NULL THEN 0
          ELSE approved_total_amount
        END AS approved_total_amount
FROM t
  LEFT JOIN a ON t.country=a.country
              AND t.month=a.month;
```


### [Задача 21](#решение-задач-sql-50-на-leetcode)

**1174. Immediate Food Delivery II**

Table: Delivery

| Column Name                 | Type    |
|-----------------------------|---------|
| delivery_id                 | int     |
| customer_id                 | int     |
| order_date                  | date    |
| customer_pref_delivery_date | date    |

delivery_id is the column of unique values of this table.
The table holds information about food delivery to customers that make orders at some date and specify a preferred delivery date (on the same order date or after it).

If the customer's preferred delivery date is the same as the order date, then the order is called immediate; otherwise, it is called scheduled.

The first order of a customer is the order with the earliest order date that the customer made. It is guaranteed that a customer has precisely one first order.

Write a solution to find the percentage of immediate orders in the first orders of all customers, rounded to 2 decimal places.

The result format is in the following example.

Example 1:

Input: 
Delivery table:

| delivery_id | customer_id | order_date | customer_pref_delivery_date |
|-------------|-------------|------------|-----------------------------|
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 2           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-12                  |
| 4           | 3           | 2019-08-24 | 2019-08-24                  |
| 5           | 3           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
| 7           | 4           | 2019-08-09 | 2019-08-09                  |

Output: 

| immediate_percentage |
|----------------------|
| 50.00                |

Explanation: 
The customer id 1 has a first order with delivery id 1 and it is scheduled.
The customer id 2 has a first order with delivery id 2 and it is immediate.
The customer id 3 has a first order with delivery id 5 and it is scheduled.
The customer id 4 has a first order with delivery id 7 and it is immediate.
Hence, half the customers have immediate first orders.

**Решение:**

```SQL
SELECT ROUND(COUNT(*) * 100 / (SELECT COUNT(DISTINCT customer_id) FROM Delivery), 2) AS immediate_percentage
FROM (SELECT  customer_id,
              order_date,
              customer_pref_delivery_date,
              MIN(order_date) OVER(PARTITION BY customer_id) AS first_date
      FROM Delivery) AS temp
WHERE order_date=first_date
  AND customer_pref_delivery_date=order_date
```


### [Задача 22](#решение-задач-sql-50-на-leetcode)

**550. Game Play Analysis IV**

Table: Activity

| Column Name  | Type    |
|--------------|---------|
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |

(player_id, event_date) is the primary key (combination of columns with unique values) of this table.
This table shows the activity of players of some games.
Each row is a record of a player who logged in and played a number of games (possibly 0) before logging out on someday using some device.

Write a solution to report the fraction of players that logged in again on the day after the day they first logged in, rounded to 2 decimal places. In other words, you need to count the number of players that logged in for at least two consecutive days starting from their first login date, then divide that number by the total number of players.

The result format is in the following example.

Example 1:

Input: 
Activity table:

| player_id | device_id | event_date | games_played |
|-----------|-----------|------------|--------------|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |

Output: 

| fraction  |
|-----------|
| 0.33      |

Explanation: 
Only the player with id 1 logged back in after the first day he had logged in so the answer is 1/3 = 0.33

**Решение:**

```SQL
-- вариант 1
SELECT ROUND(COUNT(player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity), 2) AS fraction
FROM (SELECT  player_id,
              event_date,
              MIN(event_date) OVER(PARTITION BY player_id) AS first_login
      FROM Activity) AS temp
WHERE DATEDIFF(event_date, first_login) = 1;


--вариант 2
SELECT ROUND(SUM(two_consecutive_days) / COUNT(DISTINCT player_id), 2) AS fraction
FROM (SELECT  player_id,
              event_date,
              DATEDIFF(event_date, MIN(event_date) OVER(PARTITION BY player_id)) = 1 AS two_consecutive_days
      FROM Activity) AS temp;
```



## [Sorting and Grouping](#решение-задач-sql-50-на-leetcode)


### [Задача 23](#решение-задач-sql-50-на-leetcode)

**2356. Number of Unique Subjects Taught by Each Teacher**

Table: Teacher

| Column Name | Type |
|-------------|------|
| teacher_id  | int  |
| subject_id  | int  |
| dept_id     | int  |

(subject_id, dept_id) is the primary key (combinations of columns with unique values) of this table.
Each row in this table indicates that the teacher with teacher_id teaches the subject subject_id in the department dept_id.

Write a solution to calculate the number of unique subjects each teacher teaches in the university.

Return the result table in any order.

The result format is shown in the following example.

Example 1:

Input: 
Teacher table:

| teacher_id | subject_id | dept_id |
|------------|------------|---------|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |

Output:  

| teacher_id | cnt |
|------------|-----|
| 1          | 2   |
| 2          | 4   |

Explanation: 
Teacher 1:
  - They teach subject 2 in departments 3 and 4.
  - They teach subject 3 in department 3.
Teacher 2:
  - They teach subject 1 in department 1.
  - They teach subject 2 in department 1.
  - They teach subject 3 in department 1.
  - They teach subject 4 in department 1.

**Решение:**

```SQL
SELECT  teacher_id,
        COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id;
```


### [Задача 24](#решение-задач-sql-50-на-leetcode)

**1141. User Activity for the Past 30 Days I**

Table: Activity

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| session_id    | int     |
| activity_date | date    |
| activity_type | enum    |

This table may have duplicate rows.
The activity_type column is an ENUM (category) of type ('open_session', 'end_session', 'scroll_down', 'send_message').
The table shows the user activities for a social media website. 
Note that each session belongs to exactly one user.

Write a solution to find the daily active user count for a period of 30 days ending 2019-07-27 inclusively. A user was active on someday if they made at least one activity on that day.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Activity table:

| user_id | session_id | activity_date | activity_type |
|---------|------------|---------------|---------------|
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | send_message  |
| 3       | 2          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |

Output: 

| day        | active_users |
|------------|--------------|
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |

Explanation: Note that we do not care about days with zero active users.

**Решение:**

```SQL
SELECT  activity_date AS day,
        COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date > DATE_SUB('2019-07-27', INTERVAL 30 DAY)
  AND activity_date <= '2019-07-27'
GROUP BY activity_date;
```


### [Задача 25](#решение-задач-sql-50-на-leetcode)

**1070. Product Sales Analysis III**

Table: Sales

| Column Name | Type  |
|-------------|-------|
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |

(sale_id, year) is the primary key (combination of columns with unique values) of this table.
product_id is a foreign key (reference column) to Product table.
Each row of this table shows a sale on the product product_id in a certain year.
Note that the price is per unit.

Table: Product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the product name of each product.

Write a solution to select the product id, year, quantity, and price for the first year of every product sold.

Return the resulting table in any order.

The result format is in the following example.

Example 1:

Input: 
Sales table:

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

Product table:

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

Output: 

| product_id | first_year | quantity | price |
|------------|------------|----------|-------|
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |

**Решение:**

```SQL
SELECT  product_id,
        first_year,
        quantity,
        price
FROM(SELECT product_id,
            year,
            quantity,
            price,
            MIN(year) OVER(PARTITION BY product_id) AS first_year
     FROM Sales) AS temp
WHERE year = first_year;
```


### [Задача 26](#решение-задач-sql-50-на-leetcode)

**596. Classes More Than 5 Students**

Table: Courses

| Column Name | Type    |
|-------------|---------|
| student     | varchar |
| class       | varchar |

(student, class) is the primary key (combination of columns with unique values) for this table.
Each row of this table indicates the name of a student and the class in which they are enrolled.

Write a solution to find all the classes that have at least five students.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Courses table:

| student | class    |
|---------|----------|
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |

Output: 

| class   |
|---------|
| Math    |

Explanation: 
- Math has 6 students, so we include it.
- English has 1 student, so we do not include it.
- Biology has 1 student, so we do not include it.
- Computer has 1 student, so we do not include it.

**Решение:**

```SQL
SELECT  class
FROM Courses
GROUP BY class
HAVING COUNT(student) >= 5;
```


### [Задача 27](#решение-задач-sql-50-на-leetcode)

**1729. Find Followers Count**

Table: Followers

| Column Name | Type |
|-------------|------|
| user_id     | int  |
| follower_id | int  |

(user_id, follower_id) is the primary key (combination of columns with unique values) for this table.
This table contains the IDs of a user and a follower in a social media app where the follower follows the user.

Write a solution that will, for each user, return the number of followers.

Return the result table ordered by user_id in ascending order.

The result format is in the following example.

Example 1:

Input: 
Followers table:

| user_id | follower_id |
|---------|-------------|
| 0       | 1           |
| 1       | 0           |
| 2       | 0           |
| 2       | 1           |

Output: 

| user_id | followers_count|
|---------|----------------|
| 0       | 1              |
| 1       | 1              |
| 2       | 2              |

Explanation: 
The followers of 0 are {1}
The followers of 1 are {0}
The followers of 2 are {0,1}

**Решение:**

```SQL
SELECT  user_id,
        COUNT(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;
```


### [Задача 28](#решение-задач-sql-50-на-leetcode)

**619. Biggest Single Number**

Table: MyNumbers

| Column Name | Type |
|-------------|------|
| num         | int  |

This table may contain duplicates (In other words, there is no primary key for this table in SQL).
Each row of this table contains an integer.

A single number is a number that appeared only once in the MyNumbers table.

Find the largest single number. If there is no single number, report null.

The result format is in the following example.

Example 1:

Input: 
MyNumbers table:

| num |
|-----|
| 8   |
| 8   |
| 3   |
| 3   |
| 1   |
| 4   |
| 5   |
| 6   |

Output: 

| num |
|-----|
| 6   |

Explanation: The single numbers are 1, 4, 5, and 6.
Since 6 is the largest single number, we return it.
Example 2:

Input: 
MyNumbers table:

| num |
|-----|
| 8   |
| 8   |
| 7   |
| 7   |
| 3   |
| 3   |
| 3   |

Output: 

| num  |
|------|
| null |

Explanation: There are no single numbers in the input table so we return null.

**Решение:**

```SQL
SELECT MAX(num) AS num
FROM (SELECT  num
      FROM MyNumbers
      GROUP BY num
      HAVING COUNT(num) = 1) AS temp;
```


### [Задача 29](#решение-задач-sql-50-на-leetcode)

**1045. Customers Who Bought All Products**

Table: Customer

| Column Name | Type    |
|-------------|---------|
| customer_id | int     |
| product_key | int     |

This table may contain duplicates rows. 
customer_id is not NULL.
product_key is a foreign key (reference column) to Product table.

Table: Product

| Column Name | Type    |
|-------------|---------|
| product_key | int     |

product_key is the primary key (column with unique values) for this table.

Write a solution to report the customer ids from the Customer table that bought all the products in the Product table.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Customer table:

| customer_id | product_key |
|-------------|-------------|
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |

Product table:

| product_key |
|-------------|
| 5           |
| 6           |

Output: 

| customer_id |
|-------------|
| 1           |
| 3           |

Explanation: 
The customers who bought all the products (5 and 6) are customers with IDs 1 and 3.

**Решение:**

```SQL
-- вариант 1 (сверяет только по количеству продуктов)
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);


-- вариант 2
WITH
t1 AS(
SELECT *
FROM (SELECT DISTINCT customer_id FROM Customer) AS c
    CROSS JOIN Product AS p
),
t2 AS(
SELECT *
FROM Customer
GROUP BY customer_id, product_key
)

SELECT DISTINCT customer_id
FROM Customer
WHERE customer_id NOT IN(SELECT DISTINCT t1.customer_id
                         FROM t1
                            LEFT JOIN t2 ON t1.customer_id=t2.customer_id
                                        AND t1.product_key=t2.product_key
                         WHERE t2.customer_id IS NULL);
```


## [Advanced Select and Joins](#решение-задач-sql-50-на-leetcode)


### [Задача 30](#решение-задач-sql-50-на-leetcode)

**1731. The Number of Employees Which Report to Each Employee**

Table: Employees

| Column Name | Type     |
|-------------|----------|
| employee_id | int      |
| name        | varchar  |
| reports_to  | int      |
| age         | int      |

employee_id is the primary key for this table.
This table contains information about the employees and the id of the manager they report to. Some employees do not report to anyone (reports_to is null). 

For this problem, we will consider a manager an employee who has at least 1 other employee reporting to them.

Write an SQL query to report the ids and the names of all managers, the number of employees who report directly to them, and the average age of the reports rounded to the nearest integer.

Return the result table ordered by employee_id.

The query result format is in the following example.

Example 1:

Input: 
Employees table:

| employee_id | name    | reports_to | age |
|-------------|---------|------------|-----|
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |

Output: 

| employee_id | name  | reports_count | average_age |
|-------------|-------|---------------|-------------|
| 9           | Hercy | 2             | 39          |

Explanation: Hercy has 2 people report directly to him, Alice and Bob. Their average age is (41+36)/2 = 38.5, which is 39 after rounding it to the nearest integer.

**Решение:**

```SQL
WITH
t1 AS(
SELECT  reports_to AS employee_id,
        COUNT(employee_id) AS reports_count,
        ROUND(AVG(age)) AS average_age
FROM Employees
WHERE reports_to IS NOT NULL
GROUP BY reports_to
)

SELECT  t1.employee_id,
        e.name,
        t1.reports_count,
        t1.average_age
FROM t1
  JOIN Employees AS e ON t1.employee_id=e.employee_id
ORDER BY t1.employee_id;
```


### [Задача 31](#решение-задач-sql-50-на-leetcode)

**1789. Primary Department for Each Employee**

Table: Employee

| Column Name   |  Type   |
|---------------|---------|
| employee_id   | int     |
| department_id | int     |
| primary_flag  | varchar |

(employee_id, department_id) is the primary key (combination of columns with unique values) for this table.
employee_id is the id of the employee.
department_id is the id of the department to which the employee belongs.
primary_flag is an ENUM (category) of type ('Y', 'N'). If the flag is 'Y', the department is the primary department for the employee. If the flag is 'N', the department is not the primary.

Employees can belong to multiple departments. When the employee joins other departments, they need to decide which department is their primary department. Note that when an employee belongs to only one department, their primary column is 'N'.

Write a solution to report all the employees with their primary department. For employees who belong to one department, report their only department.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Employee table:

| employee_id | department_id | primary_flag |
|-------------|---------------|--------------|
| 1           | 1             | N            |
| 2           | 1             | Y            |
| 2           | 2             | N            |
| 3           | 3             | N            |
| 4           | 2             | N            |
| 4           | 3             | Y            |
| 4           | 4             | N            |

Output: 

| employee_id | department_id |
|-------------|---------------|
| 1           | 1             |
| 2           | 1             |
| 3           | 3             |
| 4           | 3             |

Explanation: 
- The Primary department for employee 1 is 1.
- The Primary department for employee 2 is 1.
- The Primary department for employee 3 is 3.
- The Primary department for employee 4 is 3.

**Решение:**

```SQL
-- вариант 1
SELECT  employee_id,
        department_id
FROM (SELECT  *,
              COUNT(department_id) OVER(PARTITION BY employee_id) AS count
      FROM Employee) AS temp
WHERE (count > 1 AND primary_flag = 'Y')
    OR count = 1;


-- вариант 2
WITH
t AS (
SELECT  employee_id,
        department_id,
        COUNT(employee_id) AS count
FROM Employee
GROUP BY employee_id)

SELECT  employee_id,
        department_id
FROM t
WHERE count = 1
UNION
SELECT  employee_id,
        department_id
FROM Employee
WHERE primary_flag = 'Y';
```


### [Задача 32](#решение-задач-sql-50-на-leetcode)

**610. Triangle Judgement**

Table: Triangle

| Column Name | Type |
|-------------|------|
| x           | int  |
| y           | int  |
| z           | int  |

In SQL, (x, y, z) is the primary key column for this table.
Each row of this table contains the lengths of three line segments.

Report for every three line segments whether they can form a triangle.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Triangle table:

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

Output: 

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

**Решение:**

```SQL
SELECT  *,
        CASE
          WHEN (x >= y) and (x >= z) THEN CASE
                                            WHEN (y + z) > x THEN 'Yes'
                                            ELSE 'No'
                                          END
          WHEN (y >= z) THEN  CASE
                                WHEN (x + z) > y THEN 'Yes'
                                ELSE 'No'
                              END
          ELSE  CASE
                  WHEN (x + y) > z THEN 'Yes'
                  ELSE 'No'
                END
        END AS triangle
FROM Triangle
```


### [Задача 33](#решение-задач-sql-50-на-leetcode)

**180. Consecutive Numbers**

Table: Logs

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| num         | varchar |

In SQL, id is the primary key for this table.
id is an autoincrement column.

Find all numbers that appear at least three times consecutively.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Logs table:

| id | num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

Output: 

| ConsecutiveNums |
|-----------------|
| 1               |

Explanation: 1 is the only number that appears consecutively for at least three times.

**Решение:**

```SQL
SELECT DISTINCT num AS ConsecutiveNums
FROM (SELECT num
             , LEAD(num, 1) OVER() AS num2
             , LEAD(num, 2) OVER() AS num3
      FROM Logs) AS temp
WHERE num2 = num
  AND num3 = num;
```


### [Задача 34](#решение-задач-sql-50-на-leetcode)

**1164. Product Price at a Given Date**

Table: Products

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| new_price     | int     |
| change_date   | date    |

(product_id, change_date) is the primary key of this table.
Each row of this table indicates that the price of some product was changed to a new price at some date.

Write an SQL query to find the prices of all products on 2019-08-16. Assume the price of all products before any change is 10.

Return the result table in any order.

The query result format is in the following example.

Example 1:

Input: 
Products table:

| product_id | new_price | change_date |
|------------|-----------|-------------|
| 1          | 20        | 2019-08-14  |
| 2          | 50        | 2019-08-14  |
| 1          | 30        | 2019-08-15  |
| 1          | 35        | 2019-08-16  |
| 2          | 65        | 2019-08-17  |
| 3          | 20        | 2019-08-18  |

Output: 

| product_id | price |
|------------|-------|
| 2          | 50    |
| 1          | 35    |
| 3          | 10    |

**Решение:**

```SQL
-- вариант 1
WITH
lc AS(
SELECT product_id
      , MAX(change_date) AS last_change
FROM Products
WHERE change_date <= '2019-08-16'
GROUP BY product_id)

SELECT p.product_id
      , CASE
          WHEN new_price IS NULL THEN 10
          ELSE new_price
        END AS price
FROM (SELECT DISTINCT product_id FROM Products) AS p
    LEFT JOIN lc ON p.product_id=lc.product_id
    LEFT JOIN Products AS pr ON p.product_id=pr.product_id
                            AND lc.last_change=pr.change_date;


--вариант 2
WITH
lc AS(
    SELECT *
        , MAX(change_date) OVER(PARTITION BY product_id) AS last_change
    FROM Products
    WHERE change_date <= '2019-08-16')

SELECT p.product_id
     , COALESCE(new_price, 10) AS price
FROM (SELECT DISTINCT product_id FROM Products) AS p
    LEFT JOIN lc ON p.product_id=lc.product_id
WHERE change_date = last_change
    OR new_price IS NULL;
```


### [Задача 35](#решение-задач-sql-50-на-leetcode)

**1204. Last Person to Fit in the Bus**

Table: Queue

| Column Name | Type    |
|-------------|---------|
| person_id   | int     |
| person_name | varchar |
| weight      | int     |
| turn        | int     |

person_id column contains unique values.
This table has the information about all people waiting for a bus.
The person_id and turn columns will contain all numbers from 1 to n, where n is the number of rows in the table.
turn determines the order of which the people will board the bus, where turn=1 denotes the first person to board and turn=n denotes the last person to board.
weight is the weight of the person in kilograms.

There is a queue of people waiting to board a bus. However, the bus has a weight limit of 1000 kilograms, so there may be some people who cannot board.

Write a solution to find the person_name of the last person that can fit on the bus without exceeding the weight limit. The test cases are generated such that the first person does not exceed the weight limit.

The result format is in the following example.

Example 1:

Input: 
Queue table:

| person_id | person_name | weight | turn |
|-----------|-------------|--------|------|
| 5         | Alice       | 250    | 1    |
| 4         | Bob         | 175    | 5    |
| 3         | Alex        | 350    | 2    |
| 6         | John Cena   | 400    | 3    |
| 1         | Winston     | 500    | 6    |
| 2         | Marie       | 200    | 4    |

Output: 

| person_name |
|-------------|
| John Cena   |

Explanation: The folowing table is ordered by the turn for simplicity.

| Turn | ID | Name      | Weight | Total Weight |
|------|----|-----------|--------|--------------|
| 1    | 5  | Alice     | 250    | 250          |
| 2    | 3  | Alex      | 350    | 600          |
| 3    | 6  | John Cena | 400    | 1000         | (last person to board)
| 4    | 2  | Marie     | 200    | 1200         | (cannot board)
| 5    | 4  | Bob       | 175    | ___          |
| 6    | 1  | Winston   | 500    | ___          |

**Решение:**

```SQL
SELECT person_name
FROM (
     SELECT person_name
          , turn
          , SUM(weight) OVER(ORDER BY turn) AS sum
     FROM Queue) AS temp
WHERE sum <= 1000
ORDER BY turn DESC
LIMIT 1;
```


### [Задача 36](#решение-задач-sql-50-на-leetcode)

**1907. Count Salary Categories**

Table: Accounts

| Column Name | Type |
|-------------|------|
| account_id  | int  |
| income      | int  |

account_id is the primary key (column with unique values) for this table.
Each row contains information about the monthly income for one bank account.

Write a solution to calculate the number of bank accounts for each salary category. The salary categories are:

"Low Salary": All the salaries strictly less than $20000.
"Average Salary": All the salaries in the inclusive range [$20000, $50000].
"High Salary": All the salaries strictly greater than $50000.
The result table must contain all three categories. If there are no accounts in a category, return 0.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Accounts table:

| account_id | income |
|------------|--------|
| 3          | 108939 |
| 2          | 12747  |
| 8          | 87709  |
| 6          | 91796  |

Output: 

| category       | accounts_count |
|----------------|----------------|
| Low Salary     | 1              |
| Average Salary | 0              |
| High Salary    | 3              |

Explanation: 
Low Salary: Account 2.
Average Salary: No accounts.
High Salary: Accounts 3, 6, and 8.

**Решение:**

```SQL
-- вариант 1
WITH
cat AS (
     SELECT 'Low Salary' AS category
     UNION
     SELECT 'Average Salary' AS category
     UNION
     SELECT 'High Salary' AS category
),
c AS (
     SELECT account_id
          , CASE
               WHEN income < 20000 THEN 'Low Salary'
               WHEN income > 50000 THEN 'High Salary'
               ELSE 'Average Salary'
          END AS category
     FROM Accounts)

SELECT cat.category
     , count(account_id) AS accounts_count
FROM cat
     LEFT JOIN c ON cat.category=c.category
GROUP BY category;


-- вариант 2
SELECT 'Low Salary' AS category
     , COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income < 20000
UNION
SELECT 'Average Salary' AS category
     , COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income >= 20000
  AND income <= 50000
  UNION
SELECT 'High Salary' AS category
     , COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income > 50000;
```



## [Subqueries](#решение-задач-sql-50-на-leetcode)


### [Задача 37](#решение-задач-sql-50-на-leetcode)

**1978. Employees Whose Manager Left the Company**

Table: Employees

| Column Name | Type     |
|-------------|----------|
| employee_id | int      |
| name        | varchar  |
| manager_id  | int      |
| salary      | int      |

In SQL, employee_id is the primary key for this table.
This table contains information about the employees, their salary, and the ID of their manager. Some employees do not have a manager (manager_id is null). 

Find the IDs of the employees whose salary is strictly less than $30000 and whose manager left the company. When a manager leaves the company, their information is deleted from the Employees table, but the reports still have their manager_id set to the manager that left.

Return the result table ordered by employee_id.

The result format is in the following example.

Example 1:

Input:  
Employees table:

| employee_id | name      | manager_id | salary |
|-------------|-----------|------------|--------|
| 3           | Mila      | 9          | 60301  |
| 12          | Antonella | null       | 31000  |
| 13          | Emery     | null       | 67084  |
| 1           | Kalel     | 11         | 21241  |
| 9           | Mikaela   | null       | 50937  |
| 11          | Joziah    | 6          | 28485  |

Output: 

| employee_id |
|-------------|
| 11          |

Explanation: 
The employees with a salary less than $30000 are 1 (Kalel) and 11 (Joziah).
Kalel's manager is employee 11, who is still in the company (Joziah).
Joziah's manager is employee 6, who left the company because there is no row for employee 6 as it was deleted.

**Решение:**

```SQL
WITH
t AS (
     SELECT employee_id
          , manager_id
     FROM Employees
     WHERE salary < 30000
     AND manager_id IS NOT NULL
)

SELECT t.employee_id
FROM t
     LEFT JOIN Employees AS e ON t.manager_id=e.employee_id
WHERE e.employee_id IS NULL
ORDER BY t.employee_id;
```


### [Задача 38](#решение-задач-sql-50-на-leetcode)

**626. Exchange Seats**

Table: Seat

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| student     | varchar |

id is the primary key (unique value) column for this table.
Each row of this table indicates the name and the ID of a student.
id is a continuous increment.

Write a solution to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.

Return the result table ordered by id in ascending order.

The result format is in the following example.

Example 1:

Input: 
Seat table:

| id | student |
|----|---------|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

Output: 

| id | student |
|----|---------|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

Explanation: 
Note that if the number of students is odd, there is no need to change the last one's seat.

**Решение:**

```SQL
SELECT id
     , CASE
          WHEN id % 2 = 0 THEN LAG(student) OVER()
          WHEN LEAD(student) OVER() IS NULL THEN student
          ELSE LEAD(student) OVER()
       END AS student
FROM Seat;
```


### [Задача 39](#решение-задач-sql-50-на-leetcode)

**1341. Movie Rating**

Table: Movies

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| title         | varchar |

movie_id is the primary key (column with unique values) for this table.
title is the name of the movie.

Table: Users

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| name          | varchar |

user_id is the primary key (column with unique values) for this table.

Table: MovieRating

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| user_id       | int     |
| rating        | int     |
| created_at    | date    |

(movie_id, user_id) is the primary key (column with unique values) for this table.
This table contains the rating of a movie by a user in their review.
created_at is the user's review date. 

Write a solution to:

Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.
Find the movie name with the highest average rating in February 2020. In case of a tie, return the lexicographically smaller movie name.
The result format is in the following example.

Example 1:

Input: 
Movies table:

| movie_id    |  title       |
|-------------|--------------|
| 1           | Avengers     |
| 2           | Frozen 2     |
| 3           | Joker        |

Users table:

| user_id     |  name        |
|-------------|--------------|
| 1           | Daniel       |
| 2           | Monica       |
| 3           | Maria        |
| 4           | James        |

MovieRating table:

| movie_id    | user_id      | rating       | created_at  |
|-------------|--------------|--------------|-------------|
| 1           | 1            | 3            | 2020-01-12  |
| 1           | 2            | 4            | 2020-02-11  |
| 1           | 3            | 2            | 2020-02-12  |
| 1           | 4            | 1            | 2020-01-01  |
| 2           | 1            | 5            | 2020-02-17  | 
| 2           | 2            | 2            | 2020-02-01  | 
| 2           | 3            | 2            | 2020-03-01  |
| 3           | 1            | 3            | 2020-02-22  | 
| 3           | 2            | 4            | 2020-02-25  | 

Output: 

| results      |
|--------------|
| Daniel       |
| Frozen 2     |

Explanation: 
Daniel and Monica have rated 3 movies ("Avengers", "Frozen 2" and "Joker") but Daniel is smaller lexicographically.
Frozen 2 and Joker have a rating average of 3.5 in February but Frozen 2 is smaller lexicographically.

**Решение:**

```SQL
(SELECT name AS results
FROM MovieRating AS r
     JOIN Users AS u ON r.user_id=u.user_id
GROUP BY r.user_id
ORDER BY count(movie_id) DESC, name
LIMIT 1)
UNION ALL
(SELECT title AS results
FROM MovieRating AS r
     JOIN Movies AS m ON r.movie_id=m.movie_id
WHERE EXTRACT(YEAR_MONTH FROM created_at) = 202002
GROUP BY r.movie_id
ORDER BY AVG(rating) DESC, title
LIMIT 1);
```


### [Задача 40](#решение-задач-sql-50-на-leetcode)

**1321. Restaurant Growth**

Table: Customer

| Column Name   | Type    |
|---------------|---------|
| customer_id   | int     |
| name          | varchar |
| visited_on    | date    |
| amount        | int     |

In SQL,(customer_id, visited_on) is the primary key for this table.
This table contains data about customer transactions in a restaurant.
visited_on is the date on which the customer with ID (customer_id) has visited the restaurant.
amount is the total paid by a customer.

You are the restaurant owner and you want to analyze a possible expansion (there will be at least one customer every day).

Compute the moving average of how much the customer paid in a seven days window (i.e., current day + 6 days before). average_amount should be rounded to two decimal places.

Return the result table ordered by visited_on in ascending order.

The result format is in the following example.

Example 1:

Input: 
Customer table:

| customer_id | name         | visited_on   | amount      |
|-------------|--------------|--------------|-------------|
| 1           | Jhon         | 2019-01-01   | 100         |
| 2           | Daniel       | 2019-01-02   | 110         |
| 3           | Jade         | 2019-01-03   | 120         |
| 4           | Khaled       | 2019-01-04   | 130         |
| 5           | Winston      | 2019-01-05   | 110         | 
| 6           | Elvis        | 2019-01-06   | 140         | 
| 7           | Anna         | 2019-01-07   | 150         |
| 8           | Maria        | 2019-01-08   | 80          |
| 9           | Jaze         | 2019-01-09   | 110         | 
| 1           | Jhon         | 2019-01-10   | 130         | 
| 3           | Jade         | 2019-01-10   | 150         | 

Output: 

| visited_on   | amount       | average_amount |
|--------------|--------------|----------------|
| 2019-01-07   | 860          | 122.86         |
| 2019-01-08   | 840          | 120            |
| 2019-01-09   | 840          | 120            |
| 2019-01-10   | 1000         | 142.86         |

Explanation: 
1st moving average from 2019-01-01 to 2019-01-07 has an average_amount of (100 + 110 + 120 + 130 + 110 + 140 + 150)/7 = 122.86
2nd moving average from 2019-01-02 to 2019-01-08 has an average_amount of (110 + 120 + 130 + 110 + 140 + 150 + 80)/7 = 120
3rd moving average from 2019-01-03 to 2019-01-09 has an average_amount of (120 + 130 + 110 + 140 + 150 + 80 + 110)/7 = 120
4th moving average from 2019-01-04 to 2019-01-10 has an average_amount of (130 + 110 + 140 + 150 + 80 + 110 + 130 + 150)/7 = 142.86

**Решение:**

```SQL
-- вариант 1
SELECT c.visited_on
     , (SELECT SUM(t.amount)
        FROM Customer AS t
        WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on) AS amount
     , ROUND((SELECT SUM(t.amount)
              FROM Customer AS t
              WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on) 
             / 7, 2) AS average_amount
FROM Customer AS c
WHERE c.visited_on >= DATE_ADD((SELECT MIN(visited_on) FROM Customer), INTERVAL 6 DAY)
GROUP BY visited_on;

-- вариант 2
SELECT *
     , ROUND(amount / 7, 2) AS average_amount
FROM (
      SELECT visited_on
           , SUM(amount) OVER(ORDER BY visited_on RANGE BETWEEN INTERVAL 6 DAY PRECEDING AND CURRENT ROW) AS amount
      FROM (
           SELECT visited_on
                , SUM(amount) AS amount
           FROM Customer
           GROUP BY visited_on
           ) AS temp
     ) AS temp2
WHERE visited_on >= DATE_ADD((SELECT MIN(visited_on) FROM Customer), INTERVAL 6 DAY);
```


### [Задача 41](#решение-задач-sql-50-на-leetcode)

**602. Friend Requests II: Who Has the Most Friends**

Table: RequestAccepted

| Column Name    | Type    |
|----------------|---------|
| requester_id   | int     |
| accepter_id    | int     |
| accept_date    | date    |

(requester_id, accepter_id) is the primary key (combination of columns with unique values) for this table.
This table contains the ID of the user who sent the request, the ID of the user who received the request, and the date when the request was accepted.

Write a solution to find the people who have the most friends and the most friends number.

The test cases are generated so that only one person has the most friends.

The result format is in the following example.

Example 1:

Input: 
RequestAccepted table:

| requester_id | accepter_id | accept_date |
|--------------|-------------|-------------|
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |

Output: 

| id | num |
|----|-----|
| 3  | 3   |

Explanation: 
The person with id 3 is a friend of people 1, 2, and 4, so he has three friends in total, which is the most number than any others.

**Решение:**

```SQL
SELECT id
     , SUM(num) AS num
FROM (
     SELECT requester_id AS id
          , COUNT(accepter_id) AS num
     FROM RequestAccepted
     GROUP BY requester_id
     UNION ALL
     SELECT accepter_id AS id
          , COUNT(requester_id) AS num
     FROM RequestAccepted
     GROUP BY accepter_id
     ) AS temp
GROUP BY id
ORDER BY num DESC
LIMIT 1;
```

Follow up: In the real world, multiple people could have the same most number of friends. Could you find all these people in this case?

**Решение:**

```SQL
WITH
t AS(
     SELECT id
          , SUM(num) AS num
     FROM (
          SELECT requester_id AS id
               , COUNT(accepter_id) AS num
          FROM RequestAccepted
          GROUP BY requester_id
          UNION ALL
          SELECT accepter_id AS id
               , COUNT(requester_id) AS num
          FROM RequestAccepted
          GROUP BY accepter_id
          ) AS temp
     GROUP BY id
     )

SELECT *
FROM t
WHERE num = (SELECT MAX(num) FROM t);
```


### [Задача 42](#решение-задач-sql-50-на-leetcode)

**585. Investments in 2016**

Table: Insurance

| Column Name | Type  |
|-------------|-------|
| pid         | int   |
| tiv_2015    | float |
| tiv_2016    | float |
| lat         | float |
| lon         | float |

pid is the primary key (column with unique values) for this table.
Each row of this table contains information about one policy where:
pid is the policyholder's policy ID.
tiv_2015 is the total investment value in 2015 and tiv_2016 is the total investment value in 2016.
lat is the latitude of the policy holder's city. It's guaranteed that lat is not NULL.
lon is the longitude of the policy holder's city. It's guaranteed that lon is not NULL.

Write a solution to report the sum of all total investment values in 2016 tiv_2016, for all policyholders who:

have the same tiv_2015 value as one or more other policyholders, and
are not located in the same city as any other policyholder (i.e., the (lat, lon) attribute pairs must be unique).
Round tiv_2016 to two decimal places.

The result format is in the following example.

Example 1:

Input: 
Insurance table:

| pid | tiv_2015 | tiv_2016 | lat | lon |
|-----|----------|----------|-----|-----|
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |

Output: 

| tiv_2016 |
|----------|
| 45.00    |

Explanation: 
The first record in the table, like the last record, meets both of the two criteria.
The tiv_2015 value 10 is the same as the third and fourth records, and its location is unique.

The second record does not meet any of the two criteria. Its tiv_2015 is not like any other policyholders and its location is the same as the third record, which makes the third record fail, too.
So, the result is the sum of tiv_2016 of the first and last record, which is 45.

**Решение:**

```SQL
WITH
t1 AS (
          SELECT pid
               , tiv_2016
          FROM Insurance
          GROUP BY lat, lon
          HAVING count(pid) = 1
      ),

t2 AS (
          SELECT pid
               , tiv_2016
          FROM (
               SELECT pid
                    , tiv_2016
                    , COUNT(pid) OVER(PARTITION BY tiv_2015) AS count
               FROM Insurance
               ) AS temp
          WHERE count > 1
      )

SELECT ROUND(SUM(t1.tiv_2016), 2) AS tiv_2016
FROM t1
     INNER JOIN t2 ON t1.pid=t2.pid;
```


### [Задача 43](#решение-задач-sql-50-на-leetcode)

**185. Department Top Three Salaries**

Table: Employee

| Column Name  | Type    |
|--------------|---------|
| id           | int     |
| name         | varchar |
| salary       | int     |
| departmentId | int     |

id is the primary key (column with unique values) for this table.
departmentId is a foreign key (reference column) of the ID from the Department table.
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.

Table: Department

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID of a department and its name.

A company's executives are interested in seeing who earns the most money in each of the company's departments. A high earner in a department is an employee who has a salary in the top three unique salaries for that department.

Write a solution to find the employees who are high earners in each of the departments.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Employee table:

| id | name  | salary | departmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |

Department table:

| id | name  |
|----|-------|
| 1  | IT    |
| 2  | Sales |

Output: 

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Joe      | 85000  |
| IT         | Randy    | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

Explanation: 
In the IT department:
- Max earns the highest unique salary
- Both Randy and Joe earn the second-highest unique salary
- Will earns the third-highest unique salary

In the Sales department:
- Henry earns the highest salary
- Sam earns the second-highest salary
- There is no third-highest salary as there are only two employees

**Решение:**

```SQL
SELECT Department, Employee, Salary
FROM (
     SELECT d.name AS Department
          , e.name AS Employee
          , e.salary AS Salary
          , DENSE_RANK() OVER(PARTITION BY departmentId ORDER BY salary DESC) AS ran
     FROM Employee AS e
          JOIN Department AS d ON e.departmentId=d.id
     ) AS temp
WHERE ran <= 3;
```



## [Advanced String Functions / Regex / Clause](#решение-задач-sql-50-на-leetcode)


### [Задача 44](#решение-задач-sql-50-на-leetcode)

**1667. Fix Names in a Table**

Table: Users

| Column Name    | Type    |
|----------------|---------|
| user_id        | int     |
| name           | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains the ID and the name of the user. The name consists of only lowercase and uppercase characters.

Write a solution to fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by user_id.

The result format is in the following example.

Example 1:

Input: 
Users table:

| user_id | name  |
|---------|-------|
| 1       | aLice |
| 2       | bOB   |

Output: 

| user_id | name  |
|---------|-------|
| 1       | Alice |
| 2       | Bob   |

**Решение:**

```SQL
SELECT user_id
     , CONCAT(UPPER(LEFT(name, 1)), RIGHT(LOWER(name), LENGTH(name)-1)) AS name
FROM Users
ORDER BY user_id;
```


### [Задача 45](#решение-задач-sql-50-на-leetcode)

**1527. Patients With a Condition**

Table: Patients

| Column Name  | Type    |
|--------------|---------|
| patient_id   | int     |
| patient_name | varchar |
| conditions   | varchar |

patient_id is the primary key (column with unique values) for this table.
'conditions' contains 0 or more code separated by spaces. 
This table contains information of the patients in the hospital.

Write a solution to find the patient_id, patient_name, and conditions of the patients who have Type I Diabetes. Type I Diabetes always starts with DIAB1 prefix.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Patients table:

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

Output: 

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 | 

Explanation: Bob and George both have a condition that starts with DIAB1.

**Решение:**

```SQL
SELECT *
FROM Patients
WHERE INSTR(conditions, ' DIAB1') > 0
   OR LEFT(conditions, 5) = 'DIAB1';
```


### [Задача 46](#решение-задач-sql-50-на-leetcode)

**196. Delete Duplicate Emails**

Table: Person

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| email       | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table contains an email. The emails will not contain uppercase letters.

Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.

For SQL users, please note that you are supposed to write a DELETE statement and not a SELECT one.

For Pandas users, please note that you are supposed to modify Person in place.

After running your script, the answer shown is the Person table. The driver will first compile and run your piece of code and then show the Person table. The final order of the Person table does not matter.

The result format is in the following example.

Example 1:

Input: 
Person table:

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

Output: 

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |

Explanation: john@example.com is repeated two times. We keep the row with the smallest Id = 1.

**Решение:**

```SQL
DELETE
FROM Person
WHERE id IN(SELECT id
            FROM (SELECT id, ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) AS c FROM Person) AS t
            WHERE c > 1);
```


### [Задача 47](#решение-задач-sql-50-на-leetcode)

**176. Second Highest Salary**

Table: Employee

| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.

Write a solution to find the second highest salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).

The result format is in the following example.

Example 1:

Input: 
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

Output: 

| SecondHighestSalary |
|---------------------|
| 200                 |

Example 2:

Input: 
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |

Output: 

| SecondHighestSalary |
|---------------------|
| null                |

**Решение:**

```SQL
-- вариант 1
SELECT (
        SELECT DISTINCT salary AS SecondHighestSalary
        FROM Employee
        ORDER BY SecondHighestSalary DESC
        LIMIT 1 OFFSET 1
        ) AS SecondHighestSalary;

-- вариант 2
SELECT MAX(salary) AS SecondHighestSalary 
FROM Employee 
WHERE salary < (SELECT MAX(salary) FROM Employee);
```


### [Задача 48](#решение-задач-sql-50-на-leetcode)

**1484. Group Sold Products By The Date**

Table Activities:

| Column Name | Type    |
|-------------|---------|
| sell_date   | date    |
| product     | varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.
Each row of this table contains the product name and the date it was sold in a market.

Write a solution to find for each date the number of different products sold and their names.

The sold products names for each date should be sorted lexicographically.

Return the result table ordered by sell_date.

The result format is in the following example.

Example 1:

Input: 
Activities table:

| sell_date  | product    |
|------------|------------|
| 2020-05-30 | Headphone  |
| 2020-06-01 | Pencil     |
| 2020-06-02 | Mask       |
| 2020-05-30 | Basketball |
| 2020-06-01 | Bible      |
| 2020-06-02 | Mask       |
| 2020-05-30 | T-Shirt    |

Output: 

| sell_date  | num_sold | products                     |
|------------|----------|------------------------------|
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |

Explanation: 
For 2020-05-30, Sold items were (Headphone, Basketball, T-shirt), we sort them lexicographically and separate them by a comma.
For 2020-06-01, Sold items were (Pencil, Bible), we sort them lexicographically and separate them by a comma.
For 2020-06-02, the Sold item is (Mask), we just return it.

**Решение:**

```SQL
SELECT sell_date
     , COUNT(product) AS num_sold
     , GROUP_CONCAT(DISTINCT product ORDER BY product) AS products
FROM (SELECT DISTINCT * FROM Activities) AS u
GROUP BY sell_date
ORDER BY sell_date;
```


### [Задача 49](#решение-задач-sql-50-на-leetcode)

**1327. List the Products Ordered in a Period**

Table: Products

| Column Name      | Type    |
|------------------|---------|
| product_id       | int     |
| product_name     | varchar |
| product_category | varchar |

product_id is the primary key (column with unique values) for this table.
This table contains data about the company's products.

Table: Orders

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| order_date    | date    |
| unit          | int     |

This table may have duplicate rows.
product_id is a foreign key (reference column) to the Products table.
unit is the number of products ordered in order_date.

Write a solution to get the names of products that have at least 100 units ordered in February 2020 and their amount.

Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Products table:

| product_id  | product_name          | product_category |
|-------------|-----------------------|------------------|
| 1           | Leetcode Solutions    | Book             |
| 2           | Jewels of Stringology | Book             |
| 3           | HP                    | Laptop           |
| 4           | Lenovo                | Laptop           |
| 5           | Leetcode Kit          | T-shirt          |

Orders table:

| product_id   | order_date   | unit     |
|--------------|--------------|----------|
| 1            | 2020-02-05   | 60       |
| 1            | 2020-02-10   | 70       |
| 2            | 2020-01-18   | 30       |
| 2            | 2020-02-11   | 80       |
| 3            | 2020-02-17   | 2        |
| 3            | 2020-02-24   | 3        |
| 4            | 2020-03-01   | 20       |
| 4            | 2020-03-04   | 30       |
| 4            | 2020-03-04   | 60       |
| 5            | 2020-02-25   | 50       |
| 5            | 2020-02-27   | 50       |
| 5            | 2020-03-01   | 50       |

Output: 

| product_name       | unit    |
|--------------------|---------|
| Leetcode Solutions | 130     |
| Leetcode Kit       | 100     |

Explanation: 
Products with product_id = 1 is ordered in February a total of (60 + 70) = 130.
Products with product_id = 2 is ordered in February a total of 80.
Products with product_id = 3 is ordered in February a total of (2 + 3) = 5.
Products with product_id = 4 was not ordered in February 2020.
Products with product_id = 5 is ordered in February a total of (50 + 50) = 100.

**Решение:**

```SQL
SELECT product_name
     , SUM(unit) AS unit
FROM Orders AS o
    JOIN Products AS p ON o.product_id=p.product_id
WHERE EXTRACT(YEAR_MONTH FROM order_date) = '202002'
GROUP BY o.product_id
HAVING SUM(unit) >= 100;
```


### [Задача 50](#решение-задач-sql-50-на-leetcode)

**1517. Find Users With Valid E-Mails**

Table: Users

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| name          | varchar |
| mail          | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains information of the users signed up in a website. Some e-mails are invalid.

Write a solution to find the users who have valid emails.

A valid e-mail has a prefix name and a domain where:

The prefix name is a string that may contain letters (upper or lower case), digits, underscore '_', period '.', and/or dash '-'. The prefix name must start with a letter.
The domain is '@leetcode.com'.
Return the result table in any order.

The result format is in the following example.

Example 1:

Input: 
Users table:

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

Output: 

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |

Explanation: 
The mail of user 2 does not have a domain.
The mail of user 5 has the # sign which is not allowed.
The mail of user 6 does not have the leetcode domain.
The mail of user 7 starts with a period.

**Решение:**

```SQL
SELECT *
FROM Users
WHERE REGEXP_LIKE(mail, '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$') = 1;
```