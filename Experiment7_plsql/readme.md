# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

### Program:
```sql
DECLARE
    num1 NUMBER := 50;  -- Initialize first number
    num2 NUMBER := 80;  -- Initialize second number
BEGIN
    -- Compare the numbers
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;
/
```
**Expected Output:**  

Greater number is: 80

<img width="1263" height="537" alt="image" src="https://github.com/user-attachments/assets/15b65b44-8a86-4100-af97-56b224f78cac" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

### Program:
```sql
DECLARE
    n   NUMBER := 10;  -- Number up to which sum is calculated
    sum NUMBER := 0;   -- Initialize sum
    i   NUMBER := 1;   -- Loop counter
BEGIN
    -- WHILE loop to calculate sum
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;
    
    -- Display the result
    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/
```

**Expected Output:**  

Sum of first 10 natural numbers is: 55

<img width="1262" height="517" alt="image" src="https://github.com/user-attachments/assets/92b02d30-b346-4f53-bc15-234de0eb19c4" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

### Program:
```sql
DECLARE
    n NUMBER := 7;         -- Number of terms
    a NUMBER := 0;         -- First term
    b NUMBER := 1;         -- Second term
    c NUMBER;              -- To store next term
    i NUMBER := 3;         -- Counter starting from 3 (since first two are known)
BEGIN
    -- Display the first two terms
    DBMS_OUTPUT.PUT('Fibonacci sequence: ' || a || ', ' || b);

    -- Loop to generate remaining terms
    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT(', ' || c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.NEW_LINE;  -- Move to next line after output
END;
/
```

**Expected Output:**  

n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

<img width="1261" height="518" alt="image" src="https://github.com/user-attachments/assets/a3e78bcf-2acd-4e1d-b32e-46f7fe0110d9" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

### Program:
```sql
DECLARE
    n       NUMBER := 1535;  -- Original number
    reversed NUMBER := 0;    -- To store reversed number
    digit    NUMBER;         -- To extract each digit
    temp     NUMBER;         -- Temporary variable to hold n
BEGIN
    temp := n;  -- Copy original number to temp

    -- Loop to reverse the number
    WHILE temp > 0 LOOP
        digit := MOD(temp, 10);         -- Extract last digit
        reversed := reversed * 10 + digit;  -- Build reversed number
        temp := TRUNC(temp / 10);       -- Remove last digit
    END LOOP;

    -- Display the reversed number
    DBMS_OUTPUT.PUT_LINE('Reversed number is: ' || reversed);
END;
/
```

**Expected Output:**  

n = 1535  
Reversed number is 5351

<img width="1262" height="527" alt="image" src="https://github.com/user-attachments/assets/96c6d838-d8d4-426a-ad68-93c70ca4e8ff" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

### Program:
```sql
DECLARE
   a NUMBER := 10;  -- First number
   b NUMBER := 9;   -- Second number
   c NUMBER := 15;  -- Third number
   largest NUMBER;  -- To store the largest number
BEGIN
   -- Find the largest number using IF-ELSIF-ELSE
   IF a >= b AND a >= c THEN
       largest := a;
   ELSIF b >= a AND b >= c THEN
       largest := b;
   ELSE
       largest := c;
   END IF;

   -- Display the result
   DBMS_OUTPUT.PUT_LINE('Largest of three numbers is: ' || largest);
END;
/
```

**Expected Output:**  

a = 10, b = 9, c = 15  
Largest of three number is 15

<img width="1261" height="532" alt="image" src="https://github.com/user-attachments/assets/618b3a6a-c48c-4cfb-98f2-f0bf1eae0d6e" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
