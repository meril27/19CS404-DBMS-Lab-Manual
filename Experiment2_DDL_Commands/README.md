# Experiment 2: DDL Commands

### DATE : 07.02.2026

#### NAME: MERIL GOLDLINA A (212224040189)

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
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test<br>
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);<br><br>
Result<br>
Error: FOREIGN KEY constraint fail

```sql
CREATE TABLE Shipments  
(
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER, 
    FOREIGN KEY (SupplierID)  REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)


);
```

**Output:**

<img width="1237" height="327" alt="image" src="https://github.com/user-attachments/assets/d198234a-8510-4706-8c08-adb2c570481a" />


**Question 2**
---
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

For example:

Test	<br>
SELECT * FROM Books;<br>

Result

|ISBN        |    Title                 |   Author |     Publisher  | Year|
|-------------- | ----------------------- | ---------- | ---------- | ---------|
| 978-1234567890 | Data Science Essentials | Jane Doe   | TechBooks |  2024|


```sql
INSERT INTO Books(ISBN ,  Title ,Author,Publisher  , Year)
VALUES('978-1234567890',  'Data Science Essentials',  'Jane Doe',   'TechBooks',   2024);
```

**Output:**

<img width="1237" height="327" alt="image" src="https://github.com/user-attachments/assets/c67cd910-5476-4244-a2de-ad8155ce021b" />


**Question 3**
---
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE

```sql
CREATE TABLE Tasks
(
    TaskID INTEGER,
    TaskName TEXT,
    DueDate DATE 

);
```

**Output:**

<img width="1237" height="465" alt="image" src="https://github.com/user-attachments/assets/6ddf8d02-cc82-45b4-aadc-de2e7ceff6b5" />


**Question 4**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	<br>
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");<br>
UPDATE company SET com_id='COM5' WHERE com_id='COM4';<br>
SELECT * FROM item;<br>

Result

| item_id  |   item_desc   |  rate    |    icom_id|
|---------- | ------------  |---------- | ----------|
| ITM5       | Charlie Gold  |700|

```sql
CREATE TABLE item
(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK (LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
    ON UPDATE SET NULL
    ON DELETE SET NULL
);
```

**Output:**

<img width="1235" height="442" alt="image" src="https://github.com/user-attachments/assets/a2c27468-3ddc-487e-9972-a1defa7e7906" />


**Question 5**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL
For example:

Test	<br>
INSERT INTO orders (ord_id, item_id, ord_date, ord_qty, cost) VALUES ('O001', 'I001', '2023-08-01', 10, 100);<br>
SELECT * FROM orders;<br>

Result

| ord_id   |  item_id  |   ord_date   | ord_qty |    cost|
|---------- | ----------|  ---------- | ---------- | ----------|
|O001     |   I001  |      2023|          |       |

```sql
CREATE TABLE orders
(
    ord_id TEXT CHECK (length(ord_id) = 4) NOT NULL,
    item_id TEXT NOT NULL,
    ord_date DATE,
    ord_qty INTEGER,
    cost INTEGER,
    PRIMARY KEY(item_id, ord_date)
    
);
```

**Output:**

<img width="1237" height="417" alt="image" src="https://github.com/user-attachments/assets/c8ca8321-e61f-42c5-b855-bd3a39cfff8f" />


**Question 6**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

For example:

Test	<br>
pragma table_info('Student_details');<br>

Result

|cid   | name          |   type         |   notnu | dflt_value  |pk|
|----- | ---------------  |--------------- | ----- | ----------|  ----------|
|0      RollNo     |      int          |    0             |     1  |
|1      Name        |     VARCHAR(100)  |   1              |    0|
|2      Gender       |    TEXT           |  1               |   0|
|3      Subject       |   VARCHAR(30)     | 0                |  0|
|4      MARKS          |  INT (3)          |0                 | 0|
|5      Date_of_birth   | Date             |0                  |0|


```sql
ALTER TABLE Student_details ADD
Date_of_birth Date ; 
```

**Output:**

<img width="1237" height="452" alt="image" src="https://github.com/user-attachments/assets/9757f559-12ee-4708-97d1-605ef9f676db" />


**Question 7**
---
Write a SQL Query for inserting the below values in the table Customers

|ID               |NAME         |  AGE|  ADDRESS   |  SALARY    |
|---------------  |--------------- | --- | ---------- | ----------  |
|1              |  Ramesh         |  32 |  Ahmedabad |  2000|
|2               | Khilan          | 25  | Delhi      | 1500|
|3                |Kaushik          |23   |Kota        |2000|
 

```sql
INSERT INTO Customers(ID , NAME , AGE , ADDRESS ,SALARY)
VALUES (1  ,   'Ramesh', 32,   'Ahmedabad',  2000);

INSERT INTO Customers(ID , NAME , AGE , ADDRESS ,SALARY) 
VALUES (2 ,'Khilan' ,   25,   'Delhi',       1500);


INSERT INTO Customers(ID , NAME , AGE , ADDRESS ,SALARY) 
VALUES(3  , 'Kaushik'  ,23,   'Kota',        2000);
```

**Output:**

<img width="1231" height="377" alt="image" src="https://github.com/user-attachments/assets/6517e0cb-6954-4ca6-b25f-3e0bb4355716" />


**Question 8**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	<br>
pragma table_info('Student_details');<br>

Result

|cid   | name          |   type         |    notnu | dflt_value | pk|
|----- | --------------- | --------------- | -----|  ----------  |---------|
|0   |   RollNo     |      int            |  0    |          |    1|
|1    |  Name       |      VARCHAR(100)    | 1     |        |     0|
|2     | Gender     |      TEXT             |1      |         |   0|
|3      |Subject     |     VARCHAR(30)    |  0       |       |    0|
|4      |MARKS        |    INT (3)         | 0        |       |   0|
|5     | MobileNumber  |   NUMBER           |0         |       |  0|
|6     | Address        |  VARCHAR(100)     |0          |       | 0|


```sql
ALTER TABLE Student_details ADD
MobileNumber NUMBER;

ALTER TABLE Student_details ADD 
Address VARCHAR(100);
```

**Output:**

<img width="1233" height="376" alt="image" src="https://github.com/user-attachments/assets/cfc8ecb5-8849-41c6-834f-658fb92753a7" />


**Question 9**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	<br>
select * from Books;<br>

Result

|ISBN          |  Title      |     Author       |      Publisher  |    YearPublished|
-------------- | --------------|  ------------------ | -------------  |-------------|
|978-1234567890 | The Lost World | Arthur Conan Doyle | Vintage Books | 1912|
|978-0987654321 | Gone with the  | Margaret Mitchell  | Macmillan      |1936|
|978-1122334455  |Moby Dick    |   Herman Melville    | Harper & Brot  |1851|


```sql
INSERT INTO  Books (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished 
FROM Out_of_print_books;
```

**Output:**

<img width="1237" height="478" alt="image" src="https://github.com/user-attachments/assets/2cc8011d-77da-4379-a5b6-0cd83cf99353" />


**Question 10**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	<br>
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');<br>
SELECT * FROM Attendance;<br>

Result
|AttendanceID | EmployeeID|  AttendanceDate  |Status|
|------------|  ---------- | -------------- | ----------|
|1     |        1 |          202|

```sql

CREATE TABLE Attendance 
(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN('Present', 'Absent', 'Leave')), 
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)


);
```

**Output:**

<img width="1238" height="378" alt="image" src="https://github.com/user-attachments/assets/eed06bfb-e979-408d-8bf1-8db4ec4db828" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
