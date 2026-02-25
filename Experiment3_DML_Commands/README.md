# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

**Question 1**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table
---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
UPDATE Products SET sell_price  = sell_price  * 1.10 WHERE  category =  'Bakery';
```

**Output:**

<img width="1237" height="612" alt="image" src="https://github.com/user-attachments/assets/5048d358-093a-42f6-b13f-d40d2550b3d9" />


**Question 2**
---
Update the 'Selling_Price' to add 10% extra margin for all products supplied by the supplier with id 6.

PRODUCTS TABLE

|name          |     type |
|----------------- | --------------- |
|product_id    |     INT  |
|product_name   |    VARCHAR(100) |
|category        |   VARCHAR(50)|
|cost_price       |  DECIMAL(10,2) |
|sell_price        | DECIMAL(10,2)|
|reorder_lvl        |INT|
|quantity       |    INT|
|supplier_id     |   INT|

<br>For example:

|Test	|   Result|
|--------|--------|
|select changes(); | changes()<br> ---------- <br> 4 |


```sql
UPDATE PRODUCTS SET sell_price  = CAST(sell_price  * 1.10 AS INTEGER) WHERE supplier_id   = 6;
```

**Output:**

<img width="1237" height="637" alt="image" src="https://github.com/user-attachments/assets/43aae81b-8f68-4ed8-9cf4-5679df5cf1f3" />


**Question 3**
---
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

Employees table
---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test<br>
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE department_id = 20;<br><br>

Result 
|EMPLOYEE_ID |  FIRST_NAME | EMAIL     |  SALARY    |  JOB_ID|
|-----------  |---------- | ---------- | ---------- |  ----------|
|201          |Michael    | MHARTSTE   | 26000    |   MK_MAN|
|202          |Pat     |    PFAY       | 6000      |  MK_REP|


```sql
UPDATE Employees SET salary = salary * 2 WHERE department_id = 20 AND job_id LIKE '%MAN';
```

**Output:**

<img width="1237" height="442" alt="image" src="https://github.com/user-attachments/assets/395bdff9-853e-4e77-948c-a5a0db9397a1" />


**Question 4**
---
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

|name         |      type |
|----------------- | ---------------|
|product_id     |    INT              |
|product_name    |   VARCHAR(100)|
|category         |  VARCHAR(50)|
|cost_price        | DECIMAL(10,2)|
|sell_price         |DECIMAL(10,2)|
|reorder_lvl    |    INT|
|quantity        |   INT|
|supplier_id      |  INT|

For example:

Test<br>
SELECT*FROM Products WHERE supplier_id = 10;<br>

Result 
|product_id | product_name |     category  |  cost_price | sell_price | reorder_lvl|  quantity  |  supplier_id|
|----------  |----------------|  ---------- | ---------- | ---------- | ----------- | ----------  |-----------|
|6     |      Detergent Powder|  Snacks   |   60    |      80    |      20      |     40     |     10|
|7      |     Surf Excel Deter | Snacks    |  85     |     100    |     10       |    40      |    10|
|8       |    Detergent Ariel   |Items      | 85      |    100     |    10        |   40       |   10|

|product_id | product_name   |   category  |  cost_price | sell_price | reorder_lvl | quantity  |  supplier_id|
|---------- | ---------------- | ---------- |  ---------- |  ---------- | ----------- |  ---------- | -----------|
|6    |       Detergent Powder | Snacks  |    60     |     81       |   20     |      40      |    10|
|7     |      Surf Excel Deter | Snacks   |   85      |    114       |  10      |     40       |   10|
|8      |     Detergent Ariel   |Items     |  85       |   114        | 10       |    40        |  10|

```sql
UPDATE Products SET sell_price  = CAST(cost_price  * 1.35 AS INTEGER) WHERE ((sell_price - cost_price) / sell_price * 100) < 30;
```

**Output:**

<img width="1237" height="587" alt="image" src="https://github.com/user-attachments/assets/5c58ee6c-b15d-41c9-aa3a-ddc8c1333c9e" />


**Question 5**
---
Create a report that shows the capitalized FirstName and capitalized LastName renamed as FirstName and Lastname respectively and EmployeeId from the employees table sorted by EmployeeId in descending order.

employees table

|cid    |     name  |      type    |    notnull    | dflt_value | pk|
|----------  |---------- |  ----------  |---------- | ---------- | ----------|
|0    |       EmployeeID | INTEGER   |   0        |               1|
|1     |      LastName    |VARCHAR(15) | 0         |              0|
|2      |     FirstName|   VARCHAR(15) | 0          |             0|
|3       |    BirthDate |  DATETIME     |0           |            0|
|4        |   Photo      | VARCHAR(25) | 0            |           0|
|5         |  Notes       |VARCHAR(10)  |0             |          0|

For example:

Result
|FirstName|   LastName |   EmployeeID|
|---------- | ---------- | ----------|
|JANET     |  LEVERLING |  3|
|ANDREW     | FULLER     | 2|
|NANCY       |DAVOLIO     |1|

```sql
SELECT UPPER(FirstName) AS FirstName,UPPER(LastName) AS LastName,EmployeeID 
FROM employees 
ORDER BY EmployeeID DESC;
```

**Output:**

<img width="1238" height="672" alt="image" src="https://github.com/user-attachments/assets/e1f96ab1-bc64-4423-ac67-12233e5d1c05" />


**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

 
Sample table: Customer
 
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
|-----------|-------------|-------------|--------------|--------------|-------|-------------|-------------|-------------|---------------|--------------|------------|
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

For example:

Test<br>
select distinct(grade)from customer;

Result

|GRADE|
|----------|
|2|
|3|
|1|
|0|
|GRADE <br> ----------|
|3|
|1|
|0|

```sql
DELETE FROM customer WHERE GRADE = 2;
```

**Output:**

<img width="1232" height="675" alt="image" src="https://github.com/user-attachments/assets/5aa3fd66-f7f5-4fd3-8d00-6781a30ce69d" />


**Question 7**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

For example:

Test<br>
SELECT * FROM doctors;

Result
|doctor_id |  first_name | last_name |  specialization|
|---------- | ---------- |  ---------- | --------------|
|1      |     John    |    Smith    |   Cardiology|
|2       |    Emily    |   Johnson   |  Orthopedics|
|3        |   Michael   |  Brown      | Pediatrics|
|4         |  Febin      | Jones|                      |

|doctor_id  | first_name|  last_name |  specialization|
|---------- | ---------- | ---------- | --------------|
|1     |      John   |     Smith  |     Cardiology|
|2      |     Emily   |    Johnson |    Orthopedics|
|3       |    Michael  |   Brown    |   Pediatrics|


```sql
DELETE FROM Doctors WHERE specialization IS NULL;
```

**Output:**

<img width="1267" height="973" alt="image" src="https://github.com/user-attachments/assets/8ed41983-fef8-4177-b124-2bccdcf145d7" />


**Question 8**
---
Write a SQL query to label rows in the Calculations table as 'Even' if value1 is even, otherwise 'Odd'.

|cid    |     name  |      type |       notnull  |   dflt_value | pk|
|---------- | ---------- | ----------  |----------|  ---------- | ----------|
|0      |     id       |   INTEGER  |   0     |                  1|
|1       |    value1    |  REAL      |  0      |                 0|
|2        |   value2     | REAL       | 0       |                0|
|3         |  base    |    INTEGER     |0        |               0|
|4          | exponent |   INTEGER  |   0         |              0|
|5           |number    |  REAL      |  0          |             0|
|6           |decimal    | REAL    |    0           |            0|
 

For example:

Result
|id  |        value1  |    parity|
|---------- | ---------- | ----------|
|1      |     -87.65 |     Odd|
|2       |    45.78   |    Odd|
|3        |   89.99    |   Odd|
|4         |  -0.005    |  Even|


```sql
SELECT id, value1,
CASE
    WHEN value1 % 2 == 0 THEN 'Even'
    ELSE 'Odd'
END AS parity 
FROM Calculations;
```

**Output:**

<img width="1235" height="572" alt="image" src="https://github.com/user-attachments/assets/e32a7358-2b26-4b3d-ab8b-3e0ab0bf3ba2" />



**Question 9**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors WHERE specialization = 'Pediatrics' AND first_name = 'Michael'; 
```

**Output:**

<img width="1242" height="475" alt="image" src="https://github.com/user-attachments/assets/f5ff6e4b-ac8a-45a8-a7a9-245791d3eda3" />


**Question 10**
---
Write a query to Select all the records from the EmployeeInfo table, where the departments are either HR or Account.

| EmpID | EmpFname | EmpLname | Department | Project | Address | DOB | Gender |
|---------- | ----------  |----------  |------------|---------- | ----------  |----------  |------------|
| 1 | Sanjay | Mehra | HR | P1 | Hyderabad(HYD) | 01/12/1976 | M |
|2|Ananya|Mishra|Admin|P2|Delhi(DEL)|02/05/1968|F|

For example:

Result
|EmpID|       EmpFname  |  EmpLname  |  Department  |Project |    Address    |     DOB   |      Gender|
|---------- |  ---------- | ----------  |---------- | ---------- | -------------- | ----------  |----------|
|1   |        Sanjay  |    Mehra  |     HR      |    P1      |    Hyderabad(HYD) |  1976-12-01 | M |
|3    |       Rohan    |   Diwan   |    Account  |   P3        |  Mumbai(BOM)     |1980-01-01 | M|
|4     |      Sonia     |  Kulkarni |   HR        |  P1    |    Hyderabad(HYD) | 1992-05-02 | F|


```sql
SELECT EmpID,EmpFname,EmpLname,Department,Project,Address,DOB,Gender 
FROM EmployeeInfo 
WHERE TRIM(UPPER(Address)) = 'DELHI(DEL)';
```

**Output:**
<img width="1238" height="347" alt="image" src="https://github.com/user-attachments/assets/083604c8-d8c2-43a5-8005-0baefc72f8cc" />






## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
