# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
```
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT
For example:

Test	Result
pragma table_info('Departments');
cid    name             type        notnull     dflt_value  pk
-----  ---------------  ----------  ----------  ----------  ----------
0      DepartmentID     INTEGER     0                       0
1      DepartmentName   TEXT        0                       0
```
```sql
create table Departments(
DepartmentID INTEGER,
DepartmentName TEXT);
```

**Output:**

<img width="878" height="438" alt="Screenshot 2026-08-20 115051" src="https://github.com/user-attachments/assets/42b6c368-43fb-41f7-833a-6ccee876fcc3" />


**Question 2**
---
```
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;

Result
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York

```
```sql
CREATE TABLE Department(DepartmentID INTEGER PRIMARY KEY, DepartmentName TEXT UNIQUE NOT NULL, Location TEXT);
```

**Output:**

<img width="1230" height="369" alt="Screenshot 2026-08-20 115307" src="https://github.com/user-attachments/assets/1c190533-c8d6-4020-aafb-27ed0610d67a" />


**Question 3**
---
```
Create a new table named item with the following specifications and constraints:
  item_id as TEXT and as primary key.
  item_desc as TEXT.
  rate as INTEGER.
  icom_id as TEXT with a length of 4.
  icom_id is a foreign key referencing com_id in the company table.
  The foreign key should cascade updates and deletes.
  item_desc and rate should not accept NULL.

For example:

Test	
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;

Result

item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5
```

```sql

```

**Output:**

![Output3](output.png)

**Question 4**
---
```
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	
pragma table_info('customer');

Result
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           location     varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0   
```

```sql
ALTER TABLE customer RENAME COLUMN city TO location;
```

**Output:**

![Output4](output.png)

**Question 5**
---
```
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```

```sql
INSERT INTO student_details SELECT * FROM Archived_students;
```

**Output:**

![Output5](output.png)

**Question 6**
---
```
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```

```sql
INSERT INTO Books(ISBN, Title, Author)
VALUES('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

![Output6](output.png)

**Question 7**
---
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700
```

```sql
CREATE TABLE item(item_id TEXT PRIMARY KEY, 
item_desc TEXT NOT NULL, rate INTEGER NOT NULL, icom_id TEXT CHECK (LENGTH(icom_id)=4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE SET NULL 
ON DELETE SET NULL);
```

**Output:**

![Output7](output.png)

**Question 8**
---
```
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           designatio  varchar(50  0                       0

```

```sql
ALTER TABLE employee ADD designation varchar(50);
```

**Output:**

![Output8](output.png)

**Question 9**
---
```
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
For example:

Test	Result
INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;
```

```sql
CREATE TABLE Bonuses(BonusID INTEGER PRIMARY KEY, EmployeeID INTEGER, BonusAmount REAL CHECK (BonusAmount > 0),
BonusDate DATE, Reason TEXT NOT NULL, FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID))
```

**Output:**

![Output9](output.png)

**Question 10**
---
```
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
 

For example:

Test	Result
SELECT * FROM Customers;
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000

```
```sql
INSERT INTO Customers (ID, NAME, AGE, ADDRESS, SALARY)
VALUES
(1, 'Ramesh', 32, 'Ahmedabad', 2000),
(2, 'Khilan', 25, 'Delhi', 1500),
(3, 'Kaushik', 23, 'Kota', 2000);
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
