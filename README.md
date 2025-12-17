# SQL Logic Operators Lab

### My Second Cyber Lab: Filtering with SQL  

---

## 🔍 Scenario
As a **security analyst**, I often need to investigate potential security issues and update computers. This involves retrieving specific information from a database by **filtering for multiple conditions**.

For this lab, my team needed data on **employees, their machines, and departments** to conduct a security investigation. This required using **logical operators** to filter the database efficiently.

---

## Task 1: Failed Logins After Business Hours
**Goal:** Find all login attempts that were **unsuccessful** and occurred **after 6:00 PM**.  
This required combining two conditions.

**Fix:** Used the `AND` operator to filter for records where:
- `login_time` > 18:00  
- `success` = 0 (false)

**Command:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;
```

---

## Task 2: Login Attempts on Specific Dates
**Goal:** Retrieve login attempts from **May 8 and May 9, 2022**, related to a suspicious event.

**Fix:** Used the `OR` operator to select records that matched either of the two dates.

**Command:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

---

## Task 3: Login Attempts Outside of Mexico
**Goal:** Find login attempts **not originating from Mexico**, where the country might be recorded as `'MEX'` or `'MEXICO'`.

**Fix:** Used the `NOT LIKE` operator to exclude any country entries starting with `'MEX'`.

**Command:**
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

---

## Task 4: Employees in Marketing
**Goal:** Retrieve information on **employees in the Marketing department** who were located in the **East building**.

**Fix:** Used `AND` to combine department and office conditions.

**Command:**
```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

---

## Task 5: Employees in Finance or Sales
**Goal:** Retrieve information for employees in **either Finance or Sales**.

**Fix:** Used `OR` to select records where the department matched either of the two.

**Command:**
```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

---

## Task 6: All Employees Not in IT
**Goal:** Get information about employees **not in the Information Technology department**.

**Fix:** Used `NOT` to exclude all IT department records.

**Command:**
```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

---

## What I Learned
This lab was a great introduction to the **power of SQL** for a security analyst.  
I gained practical experience in running complex queries to retrieve targeted data from a database and learned how to apply **logical operators**:

- `AND` for combining multiple true conditions  
- `OR` for retrieving data that matches at least one condition  
- `NOT` for excluding specific data patterns  

These skills are foundational for any analyst who needs to work with large datasets to **investigate incidents, detect anomalies, and support decision-making** in cybersecurity operations.

---

**Author:** Joan 
