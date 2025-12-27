# SQL Security Filtering & Incident Investigation

### Technical Objective: Security Data Mining & Investigative Querying

---

## Scenario:
As a security analyst, I was tasked with investigating several red flags in our authentication logs. My objective was to filter through the `log_in_attempts` and `employees` tables to isolate indicators of compromise (IoC). This investigation focused on identifying persistent failed logins outside of business hours, suspicious international activity, and potential lateral movement by auditing department-level access.

---

## Task 1: Investigation of Post-Business Hour Brute-Force Attempts
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

## Task 2: Analysis of Suspicious May Incident Window
**Goal:** Retrieve login attempts from **May 8 and May 9, 2022**, related to a suspicious event.

**Fix:** Used the `OR` operator to select records that matched either of the two dates.

**Command:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

---

## Task 3: Geofencing Audit: Detection of Non-Regional Traffic
**Goal:** Find login attempts **not originating from Mexico**, where the country might be recorded as `'MEX'` or `'MEXICO'`.

**Fix:** Used the `NOT LIKE` operator to exclude any country entries starting with `'MEX'`.

**Command:**
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

---

## Task 4: Access Correlation for Targeted Departmental Monitoring
**Goal:** Retrieve information on **employees in the Marketing department** who were located in the **East building**.

**Fix:** Used `AND` to combine department and office conditions.

**Command:**
```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

---

## Task 5: High-Value Target (HVT) Identification: Finance & Sales
**Goal:** Retrieve information for employees in **either Finance or Sales**.

**Fix:** Used `OR` to select records where the department matched either of the two.

**Command:**
```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

---

## Task 6: Privilege Silo Auditing: Identifying Non-IT Staff Access
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
- Incident Triage: Learned to rapidly isolate high-priority security events using complex `WHERE` clause predicates.

- Boolean Investigative Logic: Applied `AND`, `OR`, and `NOT` operators to refine large datasets and reduce "noise" during forensics.

- Pattern Recognition: Utilized SQL wildcards (`LIKE 'MEX%'`) to detect anomalous activity patterns originating from untrusted regions.

- Resource Correlation: Gained experience mapping user identities to specific departments to verify the Principle of Least Privilege.

---

**Author:** Joan 

---
