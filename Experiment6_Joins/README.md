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
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

|customer_id |   cust_name    |    city    | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
|        3002 | Nick Rimando   | New York   |   100 |        5001|
|       3007 | Brad Davis     | New York   |   200 |        5001|
|      3005 | Graham Zusi    | California |   200 |        5002|
|     3008 | Julian Green   | London     |   300 |        5002|
|    3004 | Fabian Johnson | Paris      |   300 |        5006|
|   3009 | Geoff Cameron  | Berlin     |   100 |        5003|
|  3003 | Jozy Altidor   | Moscow     |   200 |        5007|
| 3001 | Brad Guzan     | London     |       |        5005|

Sample table: salesman

 |salesman_id |    name    |   city   | commission |
|-------------|------------|----------|------------|
|       5001 | James Hoog | New York |       0.15|
|      5002 | Nail Knite | Paris    |       0.13|
|     5005 | Pit Alex   | London   |       0.11|
|   5006 | Mc Lyon    | Paris    |       0.14|
|  5007 | Paul Adam  | Rome     |       0.13|
| 5003 | Lauson Hen | San Jose |       0.12|

For example:

Result
|cust_name      |  city          |   grade         |   Salesman       |  city|
|---------------  |---------------|  --------------- | --------------- | ----------|
|Brad Guzan   |    London   |        100   |           Pit Alex   |      London|
|Nick Rimando  |   Chennai   |       100    |          Bob Emily   |     New York|
|Jozy Altidore  |  Moscow     |      200     |         Paul Adam    |    Rome|
|Fabian Johns    | Paris       |     300      |        Mc Lyon       |   Paris|
|Graham Zusi      |California   |    200       |       Nail Knite     |  Paris|
|Brad Davis       |New York      |   200        |      Bob Emily       | New York|
|Julian Green     |London         |  300         |     Nail Knite       |Paris|
|Geoff Cameron    |Berlin          | 100          |    Lauson Hen      | San Jose|


```sql
SELECT 
    c.cust_name, 
    c.city,
    c.grade, 
    s.name AS Salesman, 
    s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1310" height="925" alt="Screenshot 2026-03-09 230254" src="https://github.com/user-attachments/assets/7fbeeb01-286a-4dcd-ab36-576b930c2663" />


**Question 2**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="778" height="127" alt="Screenshot 2026-03-09 230747" src="https://github.com/user-attachments/assets/f36bb620-e6e8-4bce-b6c0-61bc03dea839" />


<br>APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

<img width="778" height="125" alt="Screenshot 2026-03-09 230821" src="https://github.com/user-attachments/assets/840763dd-2af6-4598-904b-b08071f07d88" />


<br>For example:

Result
|date_of_birth  |  appointment_id |  patient_id      | doctor_id       | appointment_date|
|--------------- | --------------- | ---------------  |---------------  |-------------------|
|1980-05-12    |   1        |        1          |      1            |    2024-01-05 10:00:00|


```sql
SELECT 
    p.date_of_birth,
    a.*
FROM patients p
INNER JOIN appointments a
ON p.patient_id = a.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="1290" height="505" alt="Screenshot 2026-03-09 230937" src="https://github.com/user-attachments/assets/64f920ec-4f99-42f3-9a27-9d966b6c5589" />


**Question 3**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

| customer_id |   cust_name    |    city    | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
|        3002 | Nick Rimando   | New York   |   100 |        5001|
|       3007 | Brad Davis     | New York   |   200 |        5001|
|      3005 | Graham Zusi    | California |   200 |        5002|
|     3008 | Julian Green   | London     |   300 |        5002|
|    3004 | Fabian Johnson | Paris      |   300 |        5006|
|   3009 | Geoff Cameron  | Berlin     |   100 |        5003|
|  3003 | Jozy Altidor   | Moscow     |   200 |        5007|
| 3001 | Brad Guzan     | London     |       |        5005|

Sample table: salesman

| salesman_id |    name    |   city   | commission |
|-------------|------------|----------|------------|
|       5001 | James Hoog | New York |       0.15|
|       5002 | Nail Knite | Paris    |       0.13|
|       5005 | Pit Alex   | London   |       0.11|
|      5006 | Mc Lyon    | Paris    |       0.14|
|     5007 | Paul Adam  | Rome     |       0.13|
|    5003 | Lauson Hen | San Jose |       0.12|

For example:

Result
|cust_name      |  city            | grade           | Salesman       |  city|
|--------------- | ---------------  |---------------  |--------------- | ----------|
|Brad Guzan  |     London   |        100   |           Pit Alex   |      London|
|Nick Rimando |    Chennai   |       100    |          Bob Emily   |     New York|
|Jozy Altidore |   Moscow     |      200     |         Paul Adam    |    Rome|
|Graham Zusi    |  California  |     200      |        Nail Knite    |   Paris|
|Brad Davis      | New York     |    200       |       Bob Emily      |  New York|
|Geoff Cameron    |Berlin        |   100        |      Lauson Hen      | San Jose|


```sql
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1290" height="875" alt="Screenshot 2026-03-09 231028" src="https://github.com/user-attachments/assets/e8653aa6-6904-40d9-9dbb-9bcbfa166bb5" />


**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="779" height="126" alt="Screenshot 2026-03-09 231510" src="https://github.com/user-attachments/assets/3d92f684-caf6-40c8-8b4e-32552bf7c369" />


<br>TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

<img width="778" height="122" alt="Screenshot 2026-03-09 231535" src="https://github.com/user-attachments/assets/ad7f7058-c08c-4ab3-9b33-e0b11122eff2" />


<br>For example:

Result
|patient_name   |  result_id      |  patient_id      | test_name      |  result    |  test_date|
|--------------- | --------------- | ---------------  |--------------- | ---------- | ----------|
|Alice      |      1      |          1     |           Blood Pressure |  120/80   |   2024-01-20|
|Bob         |     2       |         2      |          X-Ray           | Normal    |  2024-03-05|
|Charlie      |    3        |        3       |         Blood Test      | Within Nor | 2024-04-01|


```sql
SELECT 
    p.first_name AS patient_name,
    t.*
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id;
```

**Output:**

<img width="1283" height="657" alt="Screenshot 2026-03-09 231742" src="https://github.com/user-attachments/assets/519f5d6d-e777-41c3-971c-d88512dfd45f" />


**Question 5**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

| customer_id |   cust_name    |    city    | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
|       3002 | Nick Rimando   | New York   |   100 |        5001|
|      3007 | Brad Davis     | New York   |   200 |        5001|
|     3005 | Graham Zusi    | California |   200 |        5002|
|    3008 | Julian Green   | London     |   300 |        5002|
|   3004 | Fabian Johnson | Paris      |   300 |        5006|
|  3009 | Geoff Cameron  | Berlin     |   100 |        5003|
| 3003 | Jozy Altidor   | Moscow     |   200 |        5007|
|3001 | Brad Guzan     | London     |       |        5005|

Sample table: salesman

| salesman_id |    name    |   city   | commission |
|-------------|------------|----------|------------|
|        5001 | James Hoog | New York |       0.15|
|       5002 | Nail Knite | Paris    |       0.13|
|      5005 | Pit Alex   | London   |       0.11|
|      5006 | Mc Lyon    | Paris    |       0.14|
|      5007 | Paul Adam  | Rome     |       0.13|
|      5003 | Lauson Hen | San Jose |       0.12|

For example:

Result
|Customer Name |   city            | Salesman        | commission|
|---------------|  ---------------  |---------------  |---------------|
|Nick Rimando |    Chennai    |      Bob Emily  |      0.15|
|Graham Zusi   |   California  |     Nail Knite  |     0.13|
|Brad Guzan     |  London       |    Pit Alex     |    0.11|
|Fabian Johns    | Paris         |   Mc Lyon       |   0.14|
|Brad Davis      | New York       |  Bob Emily      |  0.15|
|Geoff Cameron   | Berlin          | Lauson Hen      | 0.12|
|Julian Green    | London           |Nail Knite       |0.13|
|Jozy Altidore   | Moscow           |Paul Adam        |0.13|

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS city,
    s.name AS "Salesman",
    s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1311" height="904" alt="Screenshot 2026-03-09 231946" src="https://github.com/user-attachments/assets/10fb33f7-6ca0-48ec-b70f-539d105ef8aa" />


**Question 6**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

Result
|cust_name      |  commission|
---------------  |---------------|
|Nick Rimando |    0.15|
|Graham Zusi   |   0.13|
|Brad Guzan     |  0.11|
|Fabian Johns    | 0.14|
|Brad Davis       |0.15|
|Geoff Cameron    |0.12|
|Julian Green     |0.13|
|Jozy Altidore    |0.13|


```sql
SELECT c.cust_name, s.commission
FROM customer c
LEFT JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1311" height="907" alt="Screenshot 2026-03-09 232437" src="https://github.com/user-attachments/assets/f68149e0-4d5d-4081-b17a-3b2b48f69712" />


**Question 7**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

|ord_no    |  purch_amt  | ord_date  |  customer_id | salesman_id |
|---------- | ----------  |---------- | -----------  |-----------|
|70001  |     150.5 |      2012-10-05 | 3005  |       5002|
|70009   |    270.65 |     2012-09-10  |3001   |      5005|
|70002    |   65.26   |    2012-10-05  |3002    |     5001|
|70004     |  110.5    |   2012-08-17  |3009     |    5003|
|70007      | 948.5     |  2012-09-10  |3005      |   5002|
|70005  |     2400.6     | 2012-07-27  |3007       |  5001|
|70008   |    5760       | 2012-09-10  |3002        | 5001|
|70010    |   1983.43    | 2012-10-10  |3004         |5006|
|70003     |  2480.4     | 2012-10-10  |3009         |5003|
|70012      | 250.45     | 2012-06-27  |3008         5002
|70011       |75.29      | 2012-08-17  |3003         5007
|70013     |  3045.6     | 2012-04-25  |3002         5001

Sample table: customer

| customer_id |   cust_name    |    city    | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
|       3002 | Nick Rimando   | New York   |   100 |        5001|
|      3007 | Brad Davis     | New York   |   200 |        5001|
|     3005 | Graham Zusi    | California |   200 |        5002|
|    3008 | Julian Green   | London     |   300 |        5002|
|   3004 | Fabian Johnson | Paris      |   300 |        5006|
|  3009 | Geoff Cameron  | Berlin     |   100 |        5003|
| 3003 | Jozy Altidor   | Moscow     |   200 |        5007|
|3001 | Brad Guzan     | London     |       |        5005|

Sample table : salesman

 |salesman_id |    name    |   city   | commission |
|-------------|------------|----------|------------|
|        5001 | James Hoog | New York |       0.15|
|       5002 | Nail Knite | Paris    |       0.13|
|      5005 | Pit Alex   | London   |       0.11|
|     5006 | Mc Lyon    | Paris    |       0.14|
|    5007 | Paul Adam  | Rome     |       0.13|
|   5003 | Lauson Hen | San Jose |       0.12|

For example:

Result
|ord_no         |  purch_amt       | ord_date       |  cust_name      |  customer_city  |grade      | salesman_name | salesman_city | commission|
|--------------- | ---------------  |--------------- | --------------- | -------------  |----------  |-------------  |-------------  |----------|
|70001    |        150.5  |          2012-10-05   |    Graham Zusi|      California |    200  |       Nail Knite |    Paris |         0.13|
|70009     |       270.65  |         2012-09-10    |   Brad Guzan  |     London      |   100   |      Pit Alex    |   London |        0.11|
|70002      |      65.26   |         2012-10-05     |  Nick Rimando |    Chennai      |  100    |     Bob Emily    |  New York|       0.15|
|70004       |     110.5   |         2012-08-17      | Geoff Cameron |   Berlin        | 100     |    Lauson Hen |    San Jose |      0.12|
|70007        |    948.5   |         2012-09-10       |Graham Zusi    |  California     |200   |      Nail Knite  |   Paris     |     0.13|
|70005     |       2400.6  |         2012-07-27      | Brad Davis      | New York  |     200   |      Bob Emily    |  New York   |    0.15|
|70008      |      5760.0  |         2012-09-10      | Nick Rimando   |  Chennai    |    100   |      Bob Emily     | New York    |   0.15|
|70010       |     1983.43 |         2012-10-10      | Fabian Johns   |  Paris       |   300   |      Mc Lyon     |   Paris        |  0.14|
|70003        |    2480.4  |         2012-10-10      | Geoff Cameron  |  Berlin       |  100   |      Lauson Hen  |   San Jose      | 0.12|
|70012         |   250.45  |         2012-06-27      | Julian Green   |  London        | 300    |     Nail Knite  |   Paris    |      0.13|
|70011          |  75.29    |        2012-08-17      | Jozy Altidore  |  Moscow         |200     |    Paul Adam   |   Rome      |     0.13|
|70013           | 3045.6    |       2012-04-25      | Nick Rimando   |  Chennai        |100      |   Bob Emily   |   New York   |    0.15|

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
JOIN salesman s ON o.salesman_id = s.salesman_id
ORDER BY 
    CASE o.ord_no
        WHEN 70001 THEN 1
        WHEN 70009 THEN 2
        WHEN 70002 THEN 3
        WHEN 70004 THEN 4
        WHEN 70007 THEN 5
        WHEN 70005 THEN 6
        WHEN 70008 THEN 7
        WHEN 70010 THEN 8
        WHEN 70003 THEN 9
        WHEN 70012 THEN 10
        WHEN 70011 THEN 11
        WHEN 70013 THEN 12
    END;
```

**Output:**

<img width="1338" height="980" alt="Screenshot 2026-03-09 232655" src="https://github.com/user-attachments/assets/9daa6b6f-b919-47b8-9cab-39b49e37b005" />


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="1128" height="185" alt="image" src="https://github.com/user-attachments/assets/dd3386ff-f5e3-4fe8-8726-a9ba186eeb30" />


APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

<img width="1130" height="181" alt="image" src="https://github.com/user-attachments/assets/9c985020-8942-44e2-bf08-4fb8de3ced1f" />


<br>For example:

Result
|patient_id      | first_name      | last_name      |  date_of_birth  |  admission_date|  discharge_date|  doctor_id|
|---------------  |---------------  |--------------- | --------------- | -------------- | -------------- | ----------|
|2                |Bob              |Miller           |1995-08-23       |2024-02-15     | 2024-03-01     | 2|


```sql
SELECT p.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-02-01' AND '2024-02-28';
```

**Output:**

<img width="1287" height="510" alt="image" src="https://github.com/user-attachments/assets/300c1d95-f308-4912-bfa6-491f5d700eca" />


**Question 9**
---
Write an SQL query to select the 'cust_name' column from the 'customer' table (aliased as 'c'), using a LEFT JOIN with the 'orders' table based on the 'customer_id' column.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

For example:

Result
|cust_name|
|---------------|
|Nick Rimando|
|Nick Rimando|
|Nick Rimando|
|Graham Zusi|
|Graham Zusi|
|Brad Guzan|
|Fabian Johns|
|Brad Davis|
|Geoff Cameron|
|Geoff Cameron|
|Julian Green|
|Jozy Altidore|


```sql
SELECT c.cust_name
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id;
```

**Output:**

<img width="1290" height="872" alt="image" src="https://github.com/user-attachments/assets/a105b9bb-04eb-44a7-b61e-48c06ab4060d" />


**Question 10**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

| salesman_id |    name    |   city   | commission |
|-------------|------------|----------|------------|
|        5001 | James Hoog | New York |       0.15|
|       5002 | Nail Knite | Paris    |       0.13|
|      5005 | Pit Alex   | London   |       0.11|
|     5006 | Mc Lyon    | Paris    |       0.14|
|    5007 | Paul Adam  | Rome     |       0.13|
|   5003 | Lauson Hen | San Jose |       0.12|

Sample table: customer

| customer_id |   cust_name    |    city    | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
|       3002 | Nick Rimando   | New York   |   100 |        5001|
|      3007 | Brad Davis     | New York   |   200 |        5001|
|     3005 | Graham Zusi    | California |   200 |        5002|
|    3008 | Julian Green   | London     |   300 |        5002|
|   3004 | Fabian Johnson | Paris      |   300 |        5006|
|  3009 | Geoff Cameron  | Berlin     |   100 |        5003|
| 3003 | Jozy Altidor   | Moscow     |   200 |        5007|
|3001 | Brad Guzan     | London     |       |        5005|

For example:

Result
|Salesman       |  cust_name       | city|
|--------------- | ---------------  |---------------|
|Bob Emily   |     Brad Davis    |   New York|
|Nail Knite   |    Fabian Johns   |  Paris|
|Pit Alex      |   Brad Guzan      | London|
|Pit Alex      |   Julian Green    | London|
|Mc Lyon       |   Fabian Johns    | Paris|


```sql
SELECT s.name AS Salesman, c.cust_name, s.city
FROM salesman s
INNER JOIN customer c
ON s.city = c.city;
```

**Output:**

<img width="1287" height="782" alt="image" src="https://github.com/user-attachments/assets/46d83fa1-50b8-4611-9028-0bba3a676795" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
