# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**

- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

<img width="1405" height="554" alt="image" src="https://github.com/user-attachments/assets/39b4e20e-a53c-4d31-bf87-e1a6633eb6c6" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**

- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

<img width="1409" height="598" alt="image" src="https://github.com/user-attachments/assets/93a42770-49ae-4319-89fa-2fbe5bb8bde9" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**

- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

<img width="1394" height="636" alt="image" src="https://github.com/user-attachments/assets/b47b8e14-571e-48a9-9595-93781de2db8a" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**

- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

<img width="1388" height="569" alt="image" src="https://github.com/user-attachments/assets/3c4386b5-f8f8-4f8f-a875-cb1454166b7f" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**

- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

<img width="1402" height="639" alt="image" src="https://github.com/user-attachments/assets/32bdaf0e-447a-4989-8259-d134ffcc3b48" />

<img width="1404" height="599" alt="image" src="https://github.com/user-attachments/assets/5105d56f-c93b-4e8b-b054-95d69d55c57c" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
