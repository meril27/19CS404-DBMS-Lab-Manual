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
How many appointments are scheduled for each doctor?

Sample table:Appointments Table

<img width="968" height="158" alt="image" src="https://github.com/user-attachments/assets/ababe034-746f-4759-92f5-3501540d2849" />

<br>For example:

Result
|DoctorID  |  TotalAppointments |
|---------- |  -----------------|
|3   |        3|
|4    |       2|
|6     |      1|
|7      |     3|
|10     |    1|


```sql
SELECT DoctorID, COUNT(AppointmentID) AS TotalAppointments 
FROM Appointments 
GROUP BY DoctorID;
```

**Output:**

<img width="1235" height="718" alt="image" src="https://github.com/user-attachments/assets/983d7e2a-9c88-4224-a91c-0166d908b73d" />


**Question 2**
---
How many patients are there in each city?

Sample table: Patients Table

<img width="954" height="143" alt="Screenshot 2026-02-26 090424" src="https://github.com/user-attachments/assets/9df2962e-e9cd-4e48-946c-134cf8413e52" />

<br>For example:

Result
|Address  |   TotalPatients |
|---------- | ------------- |
|Berlin   |   3|
|Chicago   |  4|
|Mexico     | 3|


```sql
SELECT Address, COUNT(*) AS TotalPatients 
FROM Patients
GROUP BY Address;
```

**Output:**

<img width="1232" height="496" alt="image" src="https://github.com/user-attachments/assets/e9b253fd-3186-4bca-a7bd-d7b0a0d0f1e5" />


**Question 3**
---
How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

|name                 |             type|
|-------------------- |         ----------|
|AppointmentID    |           INTEGER|
|PatientID         |                INTEGER|
|DoctorID           |              INTEGER|
|AppointmentDateTime |  DATETIME|
|Purpose              |             TEXT|
|Status                |              TEXT  |   

For example:

Result
|HourOfDay  | TotalAppointments|
|---------- | -----------------|
|09     |     2|
|10      |    5|
|11       |   1|
|14        |  1|
|16         | 1|


```sql
SELECT strftime('%H', AppointmentDateTime) AS HourOfDay, COUNT(AppointmentID) AS TotalAppointments 
FROM Appointments 
GROUP BY HourOfDay  
ORDER BY HourOfDay;
```

**Output:**

<img width="1235" height="617" alt="image" src="https://github.com/user-attachments/assets/3dba23fd-a007-46ac-9779-a9bee8d8a9aa" />


**Question 4**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

|id  | name|age|address|salary
|-----|-----|------|-----|-----|
|1|Paul|32|California|20000|
|4|Mark|25|Richtown|65000|
|5|David|27|Texas|85000|

 

For example:

Result
|COUNT <br>----------|
|----------| 
|4|


```sql
SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="1237" height="398" alt="image" src="https://github.com/user-attachments/assets/d2f1e7f1-7ee5-4ec6-9041-9d7a49f9c28c" />


**Question 5**
---
Write a SQL query to find  how many employees work in California?

Table: employee

|name   |     type|
|---------- | ----------|
|id    |      INTEGER|
|name   |     TEXT|
|age     |    INTEGER|
|city     |   TEXT|
|income    |  INTEGER|
 

For example:

Result
|employees_in_california <br>---------------------------|
|---------------------------| 
|2|


```sql
SELECT COUNT(*) AS employees_in_california 
FROM employee 
WHERE city = 'California';
```

**Output:**

<img width="1237" height="401" alt="image" src="https://github.com/user-attachments/assets/959229a6-13ea-4d10-af0d-87c640a39390" />


**Question 6**
---
Write a SQL query to find Who has the highest income among employee living in California?

Table: employee

|name   |     type|
|---------- | ----------|
|id    |      INTEGER|
|name   |     TEXT|
|age     |    INTEGER|
|city     |   TEXT|
|income    |  INTEGER|
For example:

Result
|name      |  max(income)|
|---------- | -----------|
|Adam        |5000000|


```sql
SELECT name,max(income) 
FROM employee 
WHERE city = 'California';
```

**Output:**

<img width="1237" height="397" alt="image" src="https://github.com/user-attachments/assets/3e959a88-0705-4df9-a404-4c2adc3cee69" />


**Question 7**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

|name    |    type|
|----------|  ----------|
|id     |     INTEGER|
|name    |    TEXT|
|age      |   INTEGER|
|city      |  TEXT|
|income     | INTEGER|

For example:

Result
|total_income <br> ---------------|
|------------|
|1800000|


```sql
SELECT SUM(income) AS total_income 
FROM employee 
WHERE age >= 40;
```

**Output:**

<img width="1237" height="395" alt="image" src="https://github.com/user-attachments/assets/1cf102e4-0a0b-43cc-947f-03848c09d558" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1

<img width="1057" height="180" alt="image" src="https://github.com/user-attachments/assets/175bf9ed-bf8e-469c-9f20-2be4f55ce7ff" />


<br>For example:

Result
|age_group  | AVG(age)|
|---------- | ----------|
|20          |23.0|


```sql
SELECT (age/5)*5 as age_group,AVG(age) 
FROM customer1 
GROUP BY (age/5)*5
HAVING AVG(age) < 24;
```

**Output:**
<img width="1233" height="392" alt="image" src="https://github.com/user-attachments/assets/6ccc5794-cf7d-4985-9cec-4c8e1e33be14" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee

<img width="777" height="162" alt="image" src="https://github.com/user-attachments/assets/cb8ccd69-302e-4762-9f0c-274e867f7c98" />


<br>For example:

Result
|age        | Income|
|----------  |----------|
|32      |    200000|
|40       |   350000|
|45        |  450000|


```sql
SELECT age,MIN(Income) AS Income 
FROM employee 
GROUP BY age
HAVING MIN(Income) < 1000000;
```

**Output:**

<img width="1235" height="521" alt="image" src="https://github.com/user-attachments/assets/859eb201-c294-4905-a72f-1140bd7a656c" />


**Question 10**
---
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

|name    |    type|
|---------- | ----------|
|RecordID  |  INTEGER|
|PatientID  | INTEGER|
|DoctorID    |INTEGER|
|Date        |DATE|
|Diagnosis   |TEXT|
|Treatment   |TEXT|
|Medication  |TEXT|
For example:

Result
|PatientID  | TotalRecords|
|----------  |------------|
|1           |4|

```sql
SELECT PatientID, COUNT(RecordID) AS TotalRecords 
FROM MedicalRecords 
GROUP BY PatientID  
HAVING COUNT(RecordID) > 3;
```

**Output:**
<img width="1232" height="426" alt="image" src="https://github.com/user-attachments/assets/db9fb01f-0e6f-4e07-9143-cc3663dffb76" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
