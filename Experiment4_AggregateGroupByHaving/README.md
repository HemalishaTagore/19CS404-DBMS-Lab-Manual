# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
```
How many prescriptions were written for each medication?

Sample tablePrescriptions Table

<img width="1082" height="154" alt="image" src="https://github.com/user-attachments/assets/d43f6179-d817-405f-a590-a966e4c8eb45" />


For example:

Result
Medication     TotalPrescriptions
-------------  ------------------
Ciprofloxacin  1
Doxorubicin    1
Ibuprofen      1
Levothyroxine  1
Lisinopril     1
MMR            1
Pending        1
Prenatal vita  1
Sertraline     1
Topiramate     1

```

```sql
SELECT Medication, COUNT(*) AS TotalPrescriptions FROM Prescriptions GROUP BY Medication ORDER BY Medication;
```

**Output:**

<img width="812" height="822" alt="image" src="https://github.com/user-attachments/assets/d3eb8cf4-a282-4a72-9a1d-20bc30b78602" />


**Question 2**
---
```
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3

```

```sql
SELECT PatientID, COUNT(*) AS TotalAppointments FROM Appointments GROUP BY PatientID ORDER BY PatientID;
```

**Output:**

<img width="814" height="713" alt="image" src="https://github.com/user-attachments/assets/fa4a32a3-a524-4329-93b0-f026f957b438" />


**Question 3**
---
```
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
avg_income
----------
5000000.0


```

```sql
SELECT AVG(income) AS avg_income FROM employee WHERE name LIKE 'A%';
```

**Output:**
<img width="821" height="740" alt="image" src="https://github.com/user-attachments/assets/f7c1e4be-3214-4d5d-af01-ffb9cc2779b4" />



**Question 4**
---
```
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
avg_income
----------
5000000.0

```

```sql
SELECT AVG(income) AS avg_income FROM employee WHERE name LIKE 'A%';
```

**Output:**

<img width="813" height="396" alt="image" src="https://github.com/user-attachments/assets/2d7355ac-0f53-450e-bf4d-85bed29156ce" />


**Question 5**
---
```
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8

```

```sql
SELECT grade, COUNT(*) AS COUNT FROM customer GROUP BY grade ORDER BY COUNT LIMIT 1;
```

**Output:**

<img width="815" height="436" alt="image" src="https://github.com/user-attachments/assets/dc37d499-8d4d-4e29-863e-25c6c524b8a8" />



**Question 6**
---
```
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
age_difference
--------------
13

```

```sql
SELECT MAX(age) - MIN(age) AS age_difference FROM employee;
```

**Output:**

<img width="805" height="395" alt="image" src="https://github.com/user-attachments/assets/376e6c4f-2f66-4b22-b2bf-6b66c36af2bf" />


**Question 7**
---
```
Write a SQL query to find the number of employees whose age is greater than 32.
Sample table: employee

For example:

Result
COUNT
----------
5

```

```sql
SELECT COUNT(*) AS COUNT FROM employee WHERE age>32;
```

**Output:**
<img width="809" height="396" alt="image" src="https://github.com/user-attachments/assets/c1d3ebe4-f7b3-4a8d-bce5-5c69b3a0ced9" />

**Question 8**
---
```
Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.

Sample table: employee
<img width="1011" height="215" alt="image" src="https://github.com/user-attachments/assets/25683ac8-7b12-46e6-a2cf-9bd793c98ba3" />

For example:

Result
city        AVG(income)
----------  -----------
Arizona     1000000.0
California  2650000.0
Florida     2675000.0


```

```sql
SELECT city, AVG(income) FROM employee GROUP BY city HAVING AVG(income)> 500000;
```

**Output:**

<img width="807" height="513" alt="image" src="https://github.com/user-attachments/assets/b22a7f91-f792-4eb8-b642-699cc96ba0e3" />


**Question 9**
---
```
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee
<img width="1011" height="215" alt="image" src="https://github.com/user-attachments/assets/6ba5c0d8-081d-4086-929e-2a91136e93e6" />

For example:

Result
age         Income
----------  ----------
32          200000
40          350000
45          450000

```

```sql
SELECT age, MIN(income) AS Income FROM employee GROUP BY age HAVING MIN(income) < 1000000;
```

**Output:**

<img width="813" height="524" alt="image" src="https://github.com/user-attachments/assets/4fd8c3f2-4ff4-438d-a9ea-c8f221dafaec" />


**Question 10**
---
```
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/9058da63-94b2-401e-9d18-e3021ff9c9fd" />
For example:

Result
age_group   MIN(salary)
----------  -----------
25          1500

```

```sql
SELECT (age/5) * 5 AS age_group, MIN(salary) FROM customer1 GROUP BY age_group HAVING MIN(salary)<2000;
```

**Output:**

<img width="816" height="415" alt="image" src="https://github.com/user-attachments/assets/62ce4609-cc5b-4095-b422-454dc3c8b9d3" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
