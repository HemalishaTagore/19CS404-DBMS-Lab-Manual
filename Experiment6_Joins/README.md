# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
```
Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

 

For example:

Result
cust_name        city             ord_no           ord_date         purch_amt
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           70009            2012-09-10       270.65
Julian Green     London           70012            2012-06-27       250.45

```

```sql
SELECT c.cust_name,
       c.city,
       o.ord_no,
       o.ord_date,
       o.purch_amt
FROM customer c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE c.city = 'London';
```

**Output:**

<img width="902" height="570" alt="image" src="https://github.com/user-attachments/assets/3772d694-d072-48ee-a9d0-423fa93bb88f" />


**Question 2**
---
```
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13

```

```sql
SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
FROM customer c
JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

<img width="909" height="856" alt="image" src="https://github.com/user-attachments/assets/e1c9a9d0-99bb-4685-96d0-31a9d0ddb060" />


**Question 3**
---
```
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/766c5495-17fc-41a3-ad7f-29d16ee444ab" />

APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

<img width="1039" height="169" alt="image" src="https://github.com/user-attachments/assets/26d553ae-f4a2-4170-811d-2ea32a8523fc" />


For example:

Result
date_of_birth    appointment_id   patient_id       doctor_id        appointment_date
---------------  ---------------  ---------------  ---------------  -------------------
1980-05-12       1                1                1                2024-01-05 10:00:00

```

```sql
SELECT p.date_of_birth,
       a.*
FROM patients p
INNER JOIN appointments a
    ON p.patient_id = a.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="897" height="507" alt="image" src="https://github.com/user-attachments/assets/d73186ba-7057-4c89-995e-6ba12d43829c" />


**Question 4**
---
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/5564ce8c-7489-4c91-a969-e5215872a161" />



TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

<img width="1060" height="171" alt="image" src="https://github.com/user-attachments/assets/cb79b9e1-91a8-47b6-ade8-3500bcab5d8f" />


For example:

Result
patient_name     result_id        patient_id       test_name        result      test_date
---------------  ---------------  ---------------  ---------------  ----------  ----------
Alice            1                1                Blood Pressure   120/80      2024-01-20
Bob              2                2                X-Ray            Normal      2024-03-05
Charlie          3                3                Blood Test       Within Nor  2024-04-01

```

```sql
SELECT p.first_name AS patient_name,
       t.*
FROM patients p
INNER JOIN test_results t
    ON p.patient_id = t.patient_id;
```

**Output:**
<img width="903" height="655" alt="image" src="https://github.com/user-attachments/assets/fc641a08-5076-4958-83b0-e6af7bffe047" />


**Question 5**
---
```
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

Result
customer_id      cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
3004             Fabian Johns     Paris            300              5006

```

```sql
SELECT c.*
FROM customer c
LEFT JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE s.name = 'Mc Lyon';
```

**Output:**

<img width="898" height="504" alt="image" src="https://github.com/user-attachments/assets/d7b32ecb-3a59-4d15-bbe0-9bf49c186517" />


**Question 6**
---
```
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
<img width="1060" height="171" alt="image" src="https://github.com/user-attachments/assets/d17ae422-3592-40de-acb6-bd9691f4618a" />



TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/bbc60524-b622-4deb-8b21-1f2313afe1ca" />



For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01 
```

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t
    ON p.patient_id = t.patient_id
WHERE t.test_date BETWEEN '2024-03-01' AND '2024-03-31';
```

**Output:**

<img width="896" height="509" alt="image" src="https://github.com/user-attachments/assets/7681af63-c1be-45c2-99c9-059da3f4adca" />


**Question 7**
---
```
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             grade            Salesman         city
---------------  ---------------  ---------------  ---------------  ----------
Brad Guzan       London           100              Pit Alex         London
Nick Rimando     Chennai          100              Bob Emily        New York
Jozy Altidore    Moscow           200              Paul Adam        Rome
Fabian Johns     Paris            300              Mc Lyon          Paris
Graham Zusi      California       200              Nail Knite       Paris
Brad Davis       New York         200              Bob Emily        New York
Julian Green     London           300              Nail Knite       Paris
Geoff Cameron    Berlin           100              Lauson Hen       San Jose

```

```sql
SELECT c.cust_name,
       c.city,
       c.grade,
       s.name AS Salesman,
       s.city
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="885" height="840" alt="image" src="https://github.com/user-attachments/assets/0ce6d05b-7489-4c62-acf0-46a06aa7c774" />


**Question 8**
---
```
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
ord_no           ord_date         purch_amt        Customer Name    grade       Salesman    commission
---------------  ---------------  ---------------  ---------------  ----------  ----------  ----------
70001            2012-10-05       150.5            Graham Zusi      200         Nail Knite  0.13
70009            2012-09-10       270.65           Brad Guzan       100         Pit Alex    0.11
70002            2012-10-05       65.26            Nick Rimando     100         Bob Emily   0.15
70004            2012-08-17       110.5            Geoff Cameron    100         Lauson Hen  0.12
70007            2012-09-10       948.5            Graham Zusi      200         Nail Knite  0.13
70005            2012-07-27       2400.6           Brad Davis       200         Bob Emily   0.15
70008            2012-09-10       5760.0           Nick Rimando     100         Bob Emily   0.15
70010            2012-10-10       1983.43          Fabian Johns     300         Mc Lyon     0.14
70003            2012-10-10       2480.4           Geoff Cameron    100         Lauson Hen  0.12
70012            2012-06-27       250.45           Julian Green     300         Nail Knite  0.13
70011            2012-08-17       75.29            Jozy Altidore    200         Paul Adam   0.13
70013            2012-04-25       3045.6           Nick Rimando     100         Bob Emily   0.15
```

```sql
SELECT o.ord_no,
       o.ord_date,
       o.purch_amt,
       c.cust_name AS "Customer Name",
       c.grade,
       s.name AS Salesman,
       s.commission
FROM orders o
INNER JOIN customer c
    ON o.customer_id = c.customer_id
INNER JOIN salesman s
    ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="910" height="789" alt="image" src="https://github.com/user-attachments/assets/d0b0959b-b14a-4bda-9397-907139b1a171" />


**Question 9**
---
```
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Brad Guzan       London           Pit Alex         0.11
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Geoff Cameron    Berlin           Lauson Hen       0.12
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13
```


```sql
SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS Salesman,
       s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="907" height="597" alt="image" src="https://github.com/user-attachments/assets/7475080b-19a5-46db-9412-7a59645d6d74" />


**Question 10**
---
```
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             ord_no           ord_date         Order Amount  name        commission
---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------
Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13
```

```sql
SELECT c.cust_name,
       c.city,
       o.ord_no,
       o.ord_date,
       o.purch_amt AS "Order Amount",
       s.name,
       s.commission
FROM customer c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
LEFT JOIN salesman s
    ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="898" height="778" alt="image" src="https://github.com/user-attachments/assets/2b14e26f-0bf9-4664-9073-ca9789729528" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
