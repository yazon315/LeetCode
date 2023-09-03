# Решение задач ['SQL 50'](https://leetcode.com/studyplan/top-sql-50/) на LeetCode


## Select


### Задача 1

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


### Задача 2

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


### Задача 3

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


### Задача 4

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


### Задача 5

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


## Basic Joins


### Задача 6

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


### Задача 7

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


### Задача 8

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


### Задача 9

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


### Задача 10

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


### Задача 11

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


### Задача 12

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
ORDER BY st.student_id, s.subject_name
```


### Задача 13

****


**Решение:**

```SQL

```


### Задача 14

****


**Решение:**

```SQL

```


### Задача 15

****


**Решение:**

```SQL

```


### Задача 16

****


**Решение:**

```SQL

```


### Задача 17

****


**Решение:**

```SQL

```


### Задача 18

****


**Решение:**

```SQL

```


### Задача 19

****


**Решение:**

```SQL

```


### Задача 20

****


**Решение:**

```SQL

```


### Задача 21

****


**Решение:**

```SQL

```


### Задача 22

****


**Решение:**

```SQL

```


### Задача 23

****


**Решение:**

```SQL

```


### Задача 24

****


**Решение:**

```SQL

```


### Задача 25

****


**Решение:**

```SQL

```


### Задача 26

****


**Решение:**

```SQL

```


### Задача 27

****


**Решение:**

```SQL

```


### Задача 28

****


**Решение:**

```SQL

```


### Задача 29

****


**Решение:**

```SQL

```


### Задача 30

****


**Решение:**

```SQL

```


### Задача 31

****


**Решение:**

```SQL

```


### Задача 32

****


**Решение:**

```SQL

```


### Задача 33

****


**Решение:**

```SQL

```


### Задача 34

****


**Решение:**

```SQL

```


### Задача 35

****


**Решение:**

```SQL

```


### Задача 36

****


**Решение:**

```SQL

```


### Задача 37

****


**Решение:**

```SQL

```


### Задача 38

****


**Решение:**

```SQL

```


### Задача 39

****


**Решение:**

```SQL

```


### Задача 40

****


**Решение:**

```SQL

```


### Задача 41

****


**Решение:**

```SQL

```


### Задача 42

****


**Решение:**

```SQL

```


### Задача 43

****


**Решение:**

```SQL

```


### Задача 44

****


**Решение:**

```SQL

```


### Задача 45

****


**Решение:**

```SQL

```


### Задача 46

****


**Решение:**

```SQL

```


### Задача 47

****


**Решение:**

```SQL

```


### Задача 48

****


**Решение:**

```SQL

```


### Задача 49

****


**Решение:**

```SQL

```


### Задача 50

****


**Решение:**

```SQL

```
