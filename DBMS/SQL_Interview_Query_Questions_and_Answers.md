# SQL Interview & Written-Test Query Practice

## Frequently Asked SQL Queries --- Multiple Solutions, Explanations, and Tricky Cases

**Audience:** Fresher / campus placement interviews\
**SQL style:** Mostly standard SQL, with notes for MySQL, PostgreSQL,
SQL Server, and Oracle where syntax differs.

> **How to use this file:** For each question, first understand the
> expected result and tie-handling rule. Then practise writing the query
> without looking at the answers. Some questions have several correct
> solutions; choose the one that matches the interviewer's wording and
> the SQL dialect.

------------------------------------------------------------------------

## 0. Sample tables used in this document

### `Employee`

    EmpID EmpName     Salary   DeptID   ManagerID Email            HireDate
  ------- --------- -------- -------- ----------- ---------------- ------------
        1 Asha         90000       10        NULL asha@abc.com     2022-01-10
        2 Bharat       80000       10           1 bharat@abc.com   2022-03-15
        3 Charu        80000       20           1 charu@abc.com    2021-07-01
        4 Deepak       60000       20           3 deepak@abc.com   2023-02-20
        5 Esha         50000       30           1 esha@abc.com     2024-05-05
        6 Farhan       40000       30           3 farhan@abc.com   2024-06-12
        7 Gita         30000       10           2 gita@abc.com     2025-01-09

### `Department`

    DeptID DeptName
  -------- ----------
        10 IT
        20 HR
        30 Sales
        40 Finance

### `Orders`

    OrderID   CustomerID   Amount OrderDate
  --------- ------------ -------- ------------
        101            1     1200 2025-01-01
        102            2      800 2025-01-03
        103            1      500 2025-01-10
        104            3     1200 2025-02-01
        105            2      300 2025-02-12

**Important:** The sample data is illustrative. Your actual table/column
names may differ.

------------------------------------------------------------------------

# Part 1 --- Highest, Lowest, and Nth-Highest Salary

## 1. Find the highest salary

**Method 1 --- `MAX()` (most common)**

``` sql
SELECT MAX(Salary) AS HighestSalary
FROM Employee;
```

**Method 2 --- Sort and take one row**

``` sql
SELECT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1;
```

`LIMIT` works in MySQL and PostgreSQL. In SQL Server, use `TOP 1`; in
standard SQL, `FETCH FIRST 1 ROW ONLY` is supported by many systems.

**Method 3 --- Return the employee(s) earning the highest salary**

``` sql
SELECT *
FROM Employee
WHERE Salary = (SELECT MAX(Salary) FROM Employee);
```

**Interviewer trap:** The first two methods return the salary value; the
third returns every employee tied at the maximum.

## 2. Find the second-highest *distinct* salary

### Method 1 --- `MAX()` with a subquery

``` sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);
```

### Method 2 --- `DISTINCT`, descending sort, and offset

``` sql
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 1;
```

### Method 3 --- `DENSE_RANK()`

``` sql
SELECT Salary
FROM (
    SELECT Salary,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS salary_rank
    FROM Employee
) AS ranked
WHERE salary_rank = 2;
```

To return the employees who earn the second-highest distinct salary:

``` sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS salary_rank
    FROM Employee e
) AS ranked
WHERE salary_rank = 2;
```

### Method 4 --- Count distinct salaries above each salary

``` sql
SELECT DISTINCT e1.Salary
FROM Employee e1
WHERE 1 = (
    SELECT COUNT(DISTINCT e2.Salary)
    FROM Employee e2
    WHERE e2.Salary > e1.Salary
);
```

**Which method should you use?** `MAX()` is concise and widely
understood; `DENSE_RANK()` is especially useful for Nth-highest
questions and ties.

## 3. Find the third-highest distinct salary

**Method 1 --- `DENSE_RANK()`**

``` sql
SELECT Salary
FROM (
    SELECT Salary,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee
) x
WHERE rnk = 3;
```

**Method 2 --- Nested `MAX()`**

``` sql
SELECT MAX(Salary) AS ThirdHighestSalary
FROM Employee
WHERE Salary < (
    SELECT MAX(Salary)
    FROM Employee
    WHERE Salary < (SELECT MAX(Salary) FROM Employee)
);
```

**Method 3 --- `DISTINCT` plus offset**

``` sql
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 2;
```

## 4. Find the Nth-highest distinct salary

``` sql
-- Replace :n with the requested rank, e.g. 4
SELECT Salary
FROM (
    SELECT Salary,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee
) x
WHERE rnk = :n;
```

Alternative using distinct values:

``` sql
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 3; -- 4th-highest: offset is N - 1
```

The second version needs the offset to be calculated as `N - 1`.
Parameter syntax differs by database/client.

## 5. Find the second row by salary, including duplicate salaries

If the question means the **second employee after sorting**, not the
second distinct salary:

``` sql
SELECT *
FROM Employee
ORDER BY Salary DESC, EmpID
LIMIT 1 OFFSET 1;
```

This may return another employee with the same salary as the first. Add
a deterministic tie-breaker such as `EmpID`.

## 6. Find employees who earn the second-highest salary

``` sql
SELECT *
FROM Employee
WHERE Salary = (
    SELECT MAX(Salary)
    FROM Employee
    WHERE Salary < (SELECT MAX(Salary) FROM Employee)
);
```

Or:

``` sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee e
) x
WHERE rnk = 2;
```

## 7. Find employees earning the highest salary in each department

**Method 1 --- Join to grouped maximum**

``` sql
SELECT e.*
FROM Employee e
JOIN (
    SELECT DeptID, MAX(Salary) AS MaxSalary
    FROM Employee
    GROUP BY DeptID
) d
  ON d.DeptID = e.DeptID
 AND d.MaxSalary = e.Salary;
```

**Method 2 --- Window function**

``` sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY DeptID
               ORDER BY Salary DESC
           ) AS rnk
    FROM Employee e
) x
WHERE rnk = 1;
```

Both return all employees tied for the department's highest salary.

## 8. Find the top 3 salaries in each department

``` sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY DeptID
               ORDER BY Salary DESC
           ) AS rnk
    FROM Employee e
) x
WHERE rnk <= 3;
```

Use `ROW_NUMBER()` instead if you need exactly up to three employee rows
per department. `DENSE_RANK()` includes all ties and ranks distinct
salary values.

## 9. Find employees earning more than the company average

``` sql
SELECT *
FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

## 10. Find employees earning more than their department average

**Method 1 --- Correlated subquery**

``` sql
SELECT e.*
FROM Employee e
WHERE e.Salary > (
    SELECT AVG(e2.Salary)
    FROM Employee e2
    WHERE e2.DeptID = e.DeptID
);
```

**Method 2 --- Window function**

``` sql
SELECT *
FROM (
    SELECT e.*,
           AVG(Salary) OVER (PARTITION BY DeptID) AS DeptAvgSalary
    FROM Employee e
) x
WHERE Salary > DeptAvgSalary;
```

------------------------------------------------------------------------

# Part 2 --- `GROUP BY`, Aggregates, and `HAVING`

## 11. Count employees in each department

``` sql
SELECT DeptID, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY DeptID;
```

To show department names, including departments with zero employees:

``` sql
SELECT d.DeptID, d.DeptName, COUNT(e.EmpID) AS EmployeeCount
FROM Department d
LEFT JOIN Employee e ON e.DeptID = d.DeptID
GROUP BY d.DeptID, d.DeptName;
```

**Trap:** Use `COUNT(e.EmpID)`, not `COUNT(*)`, with this `LEFT JOIN`;
`COUNT(*)` counts the preserved department row even when no employee
matches.

## 12. Find departments with more than 5 employees

``` sql
SELECT DeptID, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY DeptID
HAVING COUNT(*) > 5;
```

**Why `HAVING`, not `WHERE`?** `WHERE` filters rows before grouping;
`HAVING` filters groups after aggregation.

## 13. Find departments whose average salary is greater than 60,000

``` sql
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DeptID
HAVING AVG(Salary) > 60000;
```

## 14. Find the total salary paid by each department

``` sql
SELECT DeptID, SUM(Salary) AS TotalSalary
FROM Employee
GROUP BY DeptID;
```

## 15. Find the minimum and maximum salary in each department

``` sql
SELECT DeptID,
       MIN(Salary) AS MinSalary,
       MAX(Salary) AS MaxSalary
FROM Employee
GROUP BY DeptID;
```

## 16. Count employees whose salary is greater than 50,000

``` sql
SELECT COUNT(*) AS EmployeeCount
FROM Employee
WHERE Salary > 50000;
```

## 17. Find duplicate salaries

``` sql
SELECT Salary, COUNT(*) AS Occurrences
FROM Employee
GROUP BY Salary
HAVING COUNT(*) > 1;
```

## 18. Find duplicate email addresses

``` sql
SELECT Email, COUNT(*) AS Occurrences
FROM Employee
GROUP BY Email
HAVING COUNT(*) > 1;
```

If `Email` can be `NULL` and you only want actual email values, add
`WHERE Email IS NOT NULL`.

## 19. Find rows with duplicate values but return the full employee records

``` sql
SELECT *
FROM Employee
WHERE Salary IN (
    SELECT Salary
    FROM Employee
    GROUP BY Salary
    HAVING COUNT(*) > 1
);
```

This finds employees whose salary value appears more than once; it does
**not** mean their entire records are duplicates.

------------------------------------------------------------------------

# Part 3 --- Joins

## 20. Display each employee with their department name

**Method 1 --- `INNER JOIN`**

``` sql
SELECT e.EmpName, d.DeptName
FROM Employee e
INNER JOIN Department d ON d.DeptID = e.DeptID;
```

**Method 2 --- `LEFT JOIN`**

``` sql
SELECT e.EmpName, d.DeptName
FROM Employee e
LEFT JOIN Department d ON d.DeptID = e.DeptID;
```

Use `LEFT JOIN` when employees without a matching department must still
appear. Use `INNER JOIN` when only matched rows are needed.

## 21. Find employees who do not belong to a valid department

``` sql
SELECT e.*
FROM Employee e
LEFT JOIN Department d ON d.DeptID = e.DeptID
WHERE d.DeptID IS NULL;
```

Equivalent `NOT EXISTS` approach:

``` sql
SELECT e.*
FROM Employee e
WHERE NOT EXISTS (
    SELECT 1
    FROM Department d
    WHERE d.DeptID = e.DeptID
);
```

## 22. Show all departments, even if they have no employees

``` sql
SELECT d.DeptName, e.EmpName
FROM Department d
LEFT JOIN Employee e ON e.DeptID = d.DeptID;
```

## 23. Find employees and their managers (self join)

``` sql
SELECT e.EmpName AS Employee,
       m.EmpName AS Manager
FROM Employee e
LEFT JOIN Employee m ON m.EmpID = e.ManagerID;
```

A self join joins a table to itself using different aliases. `LEFT JOIN`
keeps employees whose `ManagerID` is `NULL` or has no match.

## 24. Find employees working in the same department as Asha

``` sql
SELECT *
FROM Employee
WHERE DeptID = (
    SELECT DeptID
    FROM Employee
    WHERE EmpName = 'Asha'
)
AND EmpName <> 'Asha';
```

Join alternative:

``` sql
SELECT e2.*
FROM Employee e1
JOIN Employee e2 ON e1.DeptID = e2.DeptID
WHERE e1.EmpName = 'Asha'
  AND e2.EmpName <> 'Asha';
```

If more than one employee can be named Asha, identify the employee by a
unique ID instead.

## 25. Find pairs of employees in the same department

``` sql
SELECT e1.EmpName AS Employee1,
       e2.EmpName AS Employee2,
       e1.DeptID
FROM Employee e1
JOIN Employee e2
  ON e1.DeptID = e2.DeptID
 AND e1.EmpID < e2.EmpID;
```

`e1.EmpID < e2.EmpID` avoids pairing an employee with themselves and
avoids duplicate reversed pairs.

## 26. Explain the difference between a join condition and a filter

``` sql
-- Keeps every employee; only matching department details are attached
SELECT e.EmpName, d.DeptName
FROM Employee e
LEFT JOIN Department d
  ON e.DeptID = d.DeptID
 AND d.DeptName = 'IT';
```

``` sql
-- Removes employees without an IT department match; often behaves like INNER JOIN here
SELECT e.EmpName, d.DeptName
FROM Employee e
LEFT JOIN Department d ON e.DeptID = d.DeptID
WHERE d.DeptName = 'IT';
```

**Interview point:** A condition on the right-side table in `WHERE` can
remove `NULL`-extended rows from a `LEFT JOIN`. Put the condition in
`ON` when you want to preserve all left-side rows.

------------------------------------------------------------------------

# Part 4 --- `WHERE`, `NULL`, and Conditions

## 27. Find employees whose salary is between 40,000 and 80,000

``` sql
SELECT *
FROM Employee
WHERE Salary BETWEEN 40000 AND 80000;
```

`BETWEEN` includes both endpoints.

## 28. Find employees whose names start with A

``` sql
SELECT *
FROM Employee
WHERE EmpName LIKE 'A%';
```

Other common patterns: - Ends with `a`: `LIKE '%a'` - Contains `ar`:
`LIKE '%ar%'` - Exactly four characters: `LIKE '____'`

Case sensitivity depends on the database and collation.

## 29. Find employees with no manager

``` sql
SELECT *
FROM Employee
WHERE ManagerID IS NULL;
```

Do **not** use `ManagerID = NULL`. `NULL` must be tested with `IS NULL`
or `IS NOT NULL`.

## 30. Replace a missing value in output

``` sql
SELECT EmpName,
       COALESCE(CAST(ManagerID AS VARCHAR(20)), 'No manager') AS Manager
FROM Employee;
```

Casting syntax varies by database. If you only need a numeric default,
for example:

``` sql
SELECT EmpName, COALESCE(ManagerID, 0) AS ManagerID
FROM Employee;
```

Choose a default that cannot be mistaken for a real ID.

## 31. Find employees hired in 2024

Portable date-range pattern:

``` sql
SELECT *
FROM Employee
WHERE HireDate >= '2024-01-01'
  AND HireDate <  '2025-01-01';
```

This range also works well if the column contains timestamps. Avoid
wrapping the date column in a function when a range can use an index.

## 32. Find employees whose salary is not 50,000

``` sql
SELECT *
FROM Employee
WHERE Salary <> 50000;
```

Rows where `Salary` is `NULL` are not returned because the comparison is
unknown. If the requirement includes `NULL` salaries:

``` sql
SELECT *
FROM Employee
WHERE Salary <> 50000 OR Salary IS NULL;
```

## 33. Find rows matching any value from a list

``` sql
SELECT *
FROM Employee
WHERE DeptID IN (10, 30);
```

Equivalent for this example:

``` sql
SELECT *
FROM Employee
WHERE DeptID = 10 OR DeptID = 30;
```

## 34. Find employees whose salary is above the average salary of their department

See Question 10. This is a common correlated-subquery test.

------------------------------------------------------------------------

# Part 5 --- Window Functions and Ranking

## 35. Explain `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`

``` sql
SELECT EmpName, Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS row_num,
       RANK()       OVER (ORDER BY Salary DESC) AS salary_rank,
       DENSE_RANK() OVER (ORDER BY Salary DESC) AS dense_rank
FROM Employee;
```

For salaries `90000, 80000, 80000, 60000`:

    Salary   ROW_NUMBER (one possible ordering)   RANK   DENSE_RANK
  -------- ------------------------------------ ------ ------------
     90000                                    1      1            1
     80000                                    2      2            2
     80000                                    3      2            2
     60000                                    4      4            3

`ROW_NUMBER()` assigns a unique number to each row, `RANK()` leaves gaps
after ties, and `DENSE_RANK()` does not leave gaps. To make
`ROW_NUMBER()` deterministic, add a tie-breaker such as `EmpID`.

## 36. Get the latest order for each customer

**Method 1 --- `ROW_NUMBER()`**

``` sql
SELECT *
FROM (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY CustomerID
               ORDER BY OrderDate DESC, OrderID DESC
           ) AS rn
    FROM Orders o
) x
WHERE rn = 1;
```

**Method 2 --- Join to each customer's maximum date**

``` sql
SELECT o.*
FROM Orders o
JOIN (
    SELECT CustomerID, MAX(OrderDate) AS LatestDate
    FROM Orders
    GROUP BY CustomerID
) x
  ON x.CustomerID = o.CustomerID
 AND x.LatestDate = o.OrderDate;
```

Method 2 returns multiple rows if a customer has multiple orders on
their latest date. Method 1 returns one row per customer due to the
tie-breaker.

## 37. Calculate a running total of order amounts

``` sql
SELECT OrderID, CustomerID, OrderDate, Amount,
       SUM(Amount) OVER (
           PARTITION BY CustomerID
           ORDER BY OrderDate, OrderID
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS RunningTotal
FROM Orders;
```

Remove `PARTITION BY CustomerID` for one running total across all
orders.

## 38. Find the first order for each customer

``` sql
SELECT *
FROM (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY CustomerID
               ORDER BY OrderDate, OrderID
           ) AS rn
    FROM Orders o
) x
WHERE rn = 1;
```

## 39. Find the top 2 orders by amount for each customer

``` sql
SELECT *
FROM (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY CustomerID
               ORDER BY Amount DESC, OrderID
           ) AS rn
    FROM Orders o
) x
WHERE rn <= 2;
```

Use `RANK()` or `DENSE_RANK()` instead if ties should share rank.

------------------------------------------------------------------------

# Part 6 --- Subqueries, `EXISTS`, and Set Operations

## 40. Find employees who earn more than at least one employee in department 30

``` sql
SELECT *
FROM Employee
WHERE Salary > ANY (
    SELECT Salary
    FROM Employee
    WHERE DeptID = 30
);
```

`ANY` means the comparison is true for at least one value. Support and
exact behavior should be checked for your database.

Equivalent, often easier to read:

``` sql
SELECT *
FROM Employee
WHERE Salary > (
    SELECT MIN(Salary)
    FROM Employee
    WHERE DeptID = 30
);
```

## 41. Find employees who earn more than every employee in department 30

``` sql
SELECT *
FROM Employee
WHERE Salary > ALL (
    SELECT Salary
    FROM Employee
    WHERE DeptID = 30
);
```

Alternative:

``` sql
SELECT *
FROM Employee
WHERE Salary > (
    SELECT MAX(Salary)
    FROM Employee
    WHERE DeptID = 30
);
```

These are equivalent when the subquery returns non-`NULL` salaries and
at least one row. Empty-set and `NULL` behavior can make `ANY`/`ALL`
logic subtle.

## 42. Find customers who have placed at least one order

``` sql
SELECT DISTINCT CustomerID
FROM Orders;
```

Alternative using `EXISTS` against a `Customer` table:

``` sql
SELECT c.CustomerID
FROM Customer c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.CustomerID = c.CustomerID
);
```

## 43. Find customers who have never placed an order

**Method 1 --- `NOT EXISTS` (recommended)**

``` sql
SELECT c.CustomerID
FROM Customer c
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.CustomerID = c.CustomerID
);
```

**Method 2 --- `LEFT JOIN`**

``` sql
SELECT c.CustomerID
FROM Customer c
LEFT JOIN Orders o ON o.CustomerID = c.CustomerID
WHERE o.OrderID IS NULL;
```

**Method 3 --- `NOT IN` (use with caution)**

``` sql
SELECT c.CustomerID
FROM Customer c
WHERE c.CustomerID NOT IN (
    SELECT o.CustomerID
    FROM Orders o
    WHERE o.CustomerID IS NOT NULL
);
```

If the subquery used with `NOT IN` contains a `NULL`, the result may be
unexpectedly empty. `NOT EXISTS` is usually safer.

## 44. Find orders whose amount is above the average order amount

``` sql
SELECT *
FROM Orders
WHERE Amount > (SELECT AVG(Amount) FROM Orders);
```

## 45. Combine two query results

``` sql
-- UNION removes duplicate rows
SELECT EmpName AS Name FROM Employee
UNION
SELECT DeptName AS Name FROM Department;
```

``` sql
-- UNION ALL preserves duplicates and is usually cheaper
SELECT EmpName AS Name FROM Employee
UNION ALL
SELECT DeptName AS Name FROM Department;
```

The queries must return the same number of columns with compatible data
types. `UNION` is not the same as a join.

------------------------------------------------------------------------

# Part 7 --- Data Cleaning and Common Coding-Test Tasks

## 46. Delete duplicate rows while keeping one row per email

**Preferred pattern when `EmpID` uniquely identifies a row:**

``` sql
DELETE FROM Employee
WHERE EmpID IN (
    SELECT EmpID
    FROM (
        SELECT EmpID,
               ROW_NUMBER() OVER (
                   PARTITION BY Email
                   ORDER BY EmpID
               ) AS rn
        FROM Employee
        WHERE Email IS NOT NULL
    ) x
    WHERE rn > 1
);
```

Some database systems restrict modifying a table while selecting from
it, so syntax may need adaptation. Always preview the rows with a
`SELECT` first and run destructive operations in a transaction or test
database. This example treats duplicate email as the duplicate criterion
and keeps the smallest `EmpID`.

## 47. Update salary by 10% for department 10

``` sql
UPDATE Employee
SET Salary = Salary * 1.10
WHERE DeptID = 10;
```

Before updating, preview the affected rows:

``` sql
SELECT *
FROM Employee
WHERE DeptID = 10;
```

## 48. Delete employees with a salary below 20,000

``` sql
DELETE FROM Employee
WHERE Salary < 20000;
```

Check the target rows with a `SELECT` first. `NULL` salaries will not
match this condition.

## 49. Find the second occurrence of a repeated value

For example, label repeated salaries in occurrence order:

``` sql
SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY Salary
               ORDER BY EmpID
           ) AS occurrence_no
    FROM Employee e
) x
WHERE occurrence_no = 2;
```

This finds the second row within each salary group, not the
second-highest salary.

## 50. Swap two column values in one row

``` sql
UPDATE SomeTable
SET ColumnA = ColumnB,
    ColumnB = ColumnA
WHERE ID = 1;
```

**Caution:** This is not portable. SQL Server generally evaluates
assignments using the old row values, but behavior can differ across
systems. A safer portable approach uses a temporary variable in a
transaction or database-specific syntax. Do not assume this one-liner
works identically in every SQL engine.

## 51. Find records that appear in one table but not another

**Method 1 --- `NOT EXISTS`**

``` sql
SELECT a.*
FROM TableA a
WHERE NOT EXISTS (
    SELECT 1
    FROM TableB b
    WHERE b.ID = a.ID
);
```

**Method 2 --- `LEFT JOIN`**

``` sql
SELECT a.*
FROM TableA a
LEFT JOIN TableB b ON b.ID = a.ID
WHERE b.ID IS NULL;
```

Use a non-nullable key from `TableB` in the `IS NULL` test.

## 52. Find the percentage of employees in each department

``` sql
SELECT DeptID,
       COUNT(*) AS EmployeeCount,
       100.0 * COUNT(*) / (SELECT COUNT(*) FROM Employee) AS Percentage
FROM Employee
GROUP BY DeptID;
```

`100.0` helps avoid integer division in systems that perform integer
arithmetic for integer operands.

## 53. Pivot categories into columns using conditional aggregation

Count employees by department in one row:

``` sql
SELECT
    SUM(CASE WHEN DeptID = 10 THEN 1 ELSE 0 END) AS IT_Count,
    SUM(CASE WHEN DeptID = 20 THEN 1 ELSE 0 END) AS HR_Count,
    SUM(CASE WHEN DeptID = 30 THEN 1 ELSE 0 END) AS Sales_Count
FROM Employee;
```

This is portable conditional aggregation. Dedicated `PIVOT` syntax
varies by database.

## 54. Find consecutive or gap-free dates (advanced)

For consecutive date sequences, use `LAG()` to compare each date with
the previous one. Exact logic depends on whether dates are unique and
whether weekends count.

``` sql
SELECT OrderDate,
       LAG(OrderDate) OVER (ORDER BY OrderDate) AS PreviousDate
FROM Orders;
```

Then compare the current date with the prior date using your database's
date arithmetic.

------------------------------------------------------------------------

# Part 8 --- Classic Written-Test Questions

## 55. Find the highest salary without using `MAX()`

``` sql
SELECT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1;
```

Another way:

``` sql
SELECT e1.Salary
FROM Employee e1
WHERE NOT EXISTS (
    SELECT 1
    FROM Employee e2
    WHERE e2.Salary > e1.Salary
);
```

The `NOT EXISTS` version returns every employee row tied at the highest
salary unless `DISTINCT` is added.

## 56. Find the minimum salary without using `MIN()`

``` sql
SELECT Salary
FROM Employee
ORDER BY Salary ASC
LIMIT 1;
```

Alternative:

``` sql
SELECT e1.Salary
FROM Employee e1
WHERE NOT EXISTS (
    SELECT 1
    FROM Employee e2
    WHERE e2.Salary < e1.Salary
);
```

## 57. Find the employees with an even `EmpID`

``` sql
SELECT *
FROM Employee
WHERE MOD(EmpID, 2) = 0;
```

In many SQL dialects, `%` is also used: `EmpID % 2 = 0`.
Function/operator support varies.

## 58. Find employees with an odd `EmpID`

``` sql
SELECT *
FROM Employee
WHERE MOD(EmpID, 2) = 1;
```

## 59. Find the first and last employee by ID

``` sql
(SELECT * FROM Employee ORDER BY EmpID ASC LIMIT 1)
UNION ALL
(SELECT * FROM Employee ORDER BY EmpID DESC LIMIT 1);
```

Parentheses and `ORDER BY` rules vary by database. A window-function
alternative can label first and last rows.

## 60. Find the department with the most employees

**Method 1 --- Sort aggregate results**

``` sql
SELECT DeptID, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY DeptID
ORDER BY EmployeeCount DESC
LIMIT 1;
```

**Method 2 --- Return all tied departments**

``` sql
SELECT DeptID, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY DeptID
HAVING COUNT(*) = (
    SELECT MAX(cnt)
    FROM (
        SELECT COUNT(*) AS cnt
        FROM Employee
        GROUP BY DeptID
    ) x
);
```

Method 1 returns one row (tie selection may be arbitrary without a
secondary sort); Method 2 returns all departments tied for the maximum
count.

## 61. Find the customer who spent the most

``` sql
SELECT CustomerID, SUM(Amount) AS TotalSpent
FROM Orders
GROUP BY CustomerID
ORDER BY TotalSpent DESC
LIMIT 1;
```

To return all customers tied for the highest total, rank the grouped
totals using `DENSE_RANK()` and filter for rank 1.

## 62. Find customers with more than one order

``` sql
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY CustomerID
HAVING COUNT(*) > 1;
```

## 63. Find orders placed in the same month as another order (date grouping)

For portable month-based reporting, use a database-specific month
expression or a date range. For example, in MySQL:

``` sql
SELECT YEAR(OrderDate) AS OrderYear,
       MONTH(OrderDate) AS OrderMonth,
       COUNT(*) AS OrderCount
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate);
```

In PostgreSQL, use `DATE_TRUNC('month', OrderDate)`. Include the year so
January from different years is not combined.

## 64. Find employees whose name contains exactly one letter `a` (case-insensitive caveat)

A simple pattern such as `LIKE '%a%'` only checks whether the name
contains `a`; it does not count occurrences. Counting characters
requires dialect-specific functions or regular expressions. In MySQL,
one approach is:

``` sql
SELECT *
FROM Employee
WHERE CHAR_LENGTH(LOWER(EmpName))
    - CHAR_LENGTH(REPLACE(LOWER(EmpName), 'a', '')) = 1;
```

Function names and case behavior can vary by database.

------------------------------------------------------------------------

# Part 9 --- Query Output and Logic Traps

## 65. What does this query do?

``` sql
SELECT *
FROM Employee
INNER JOIN Department
ON Employee.DeptID = 10;
```

This is **not** a normal department match: the condition refers only to
`Employee`. Each employee with `DeptID = 10` joins to every row in
`Department`, because the join condition does not connect the department
row to the employee's department. This can multiply rows unexpectedly.

Correct join:

``` sql
SELECT *
FROM Employee e
INNER JOIN Department d
  ON e.DeptID = d.DeptID;
```

## 66. What is the difference between `COUNT(*)`, `COUNT(column)`, and `COUNT(DISTINCT column)`?

``` sql
SELECT COUNT(*) AS AllRows,
       COUNT(Email) AS NonNullEmails,
       COUNT(DISTINCT Email) AS UniqueNonNullEmails
FROM Employee;
```

-   `COUNT(*)`: counts rows.
-   `COUNT(column)`: counts non-`NULL` values in that column.
-   `COUNT(DISTINCT column)`: counts distinct non-`NULL` values.

## 67. What happens if you use `WHERE COUNT(*) > 2`?

This is invalid in ordinary SQL because aggregates are evaluated after
row filtering. Use:

``` sql
SELECT DeptID, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY DeptID
HAVING COUNT(*) > 2;
```

## 68. What happens when a scalar subquery returns multiple rows?

Example:

``` sql
SELECT *
FROM Employee
WHERE Salary = (SELECT Salary FROM Employee WHERE DeptID = 10);
```

If department 10 has multiple employees, the subquery returns multiple
salaries and `=` generally raises a scalar-subquery error. Use `IN` if
multiple values are intended:

``` sql
SELECT *
FROM Employee
WHERE Salary IN (SELECT Salary FROM Employee WHERE DeptID = 10);
```

Or use a single-value aggregate if that matches the requirement.

## 69. Why can `NOT IN` return no rows unexpectedly?

``` sql
SELECT *
FROM Employee
WHERE EmpID NOT IN (SELECT ManagerID FROM Employee);
```

If the subquery includes `NULL` (for example, the top manager has no
manager), comparisons can evaluate to unknown and filter out rows
unexpectedly. Safer pattern:

``` sql
SELECT e.*
FROM Employee e
WHERE NOT EXISTS (
    SELECT 1
    FROM Employee x
    WHERE x.ManagerID = e.EmpID
);
```

This example returns employees who are not listed as anyone's manager;
it is not the same as finding employees with no manager.

## 70. Why does a `LEFT JOIN` sometimes act like an `INNER JOIN`?

``` sql
SELECT e.EmpName, d.DeptName
FROM Employee e
LEFT JOIN Department d ON d.DeptID = e.DeptID
WHERE d.DeptName = 'IT';
```

The `WHERE` condition rejects rows where `d.DeptName` is `NULL`. If you
need all employees but only want IT details when they match, put the
filter in the `ON` clause instead.

------------------------------------------------------------------------

# Part 10 --- Quick Practice Set (Try Before Reading Answers)

Write a query for each task:

1.  Find the 4th-highest distinct salary.
2.  Find all employees tied for the maximum salary.
3.  Find the department with the lowest average salary.
4.  Find employees who earn less than their department average.
5.  Find the second order by date for every customer.
6.  Find customers with no orders.
7.  Count how many employees have a manager.
8.  Find duplicate emails, ignoring `NULL`.
9.  Show every department and its employee count, including zero.
10. Find the top 2 distinct salaries in each department.
11. Find each employee's salary rank within their department.
12. Find orders whose amount is greater than the average amount.
13. Find employees hired in the last 30 days (date syntax depends on
    DB).
14. Increase salaries by 5% for employees below the company average
    (think carefully about how to use the average in an `UPDATE`).
15. Find rows in `TableA` that do not have a matching key in `TableB`.

## Answer key

### 1. 4th-highest distinct salary

``` sql
SELECT Salary
FROM (
    SELECT Salary,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee
) x
WHERE rnk = 4;
```

### 2. All employees tied for maximum salary

``` sql
SELECT *
FROM Employee
WHERE Salary = (SELECT MAX(Salary) FROM Employee);
```

### 3. Department with lowest average salary

``` sql
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DeptID
ORDER BY AvgSalary ASC
LIMIT 1;
```

To return all tied departments, rank the department averages and filter
for rank 1.

### 4. Employees below their department average

``` sql
SELECT e.*
FROM Employee e
WHERE e.Salary < (
    SELECT AVG(e2.Salary)
    FROM Employee e2
    WHERE e2.DeptID = e.DeptID
);
```

### 5. Second order by date for every customer

``` sql
SELECT *
FROM (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY CustomerID
               ORDER BY OrderDate, OrderID
           ) AS rn
    FROM Orders o
) x
WHERE rn = 2;
```

### 6. Customers with no orders

``` sql
SELECT c.CustomerID
FROM Customer c
WHERE NOT EXISTS (
    SELECT 1 FROM Orders o
    WHERE o.CustomerID = c.CustomerID
);
```

Requires a `Customer` table.

### 7. Count employees who have a manager

``` sql
SELECT COUNT(*) AS EmployeesWithManager
FROM Employee
WHERE ManagerID IS NOT NULL;
```

### 8. Duplicate non-NULL emails

``` sql
SELECT Email, COUNT(*) AS Occurrences
FROM Employee
WHERE Email IS NOT NULL
GROUP BY Email
HAVING COUNT(*) > 1;
```

### 9. Every department with count, including zero

``` sql
SELECT d.DeptID, d.DeptName, COUNT(e.EmpID) AS EmployeeCount
FROM Department d
LEFT JOIN Employee e ON e.DeptID = d.DeptID
GROUP BY d.DeptID, d.DeptName;
```

### 10. Top 2 distinct salaries per department

``` sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY DeptID
               ORDER BY Salary DESC
           ) AS rnk
    FROM Employee e
) x
WHERE rnk <= 2;
```

### 11. Salary rank in department

``` sql
SELECT EmpName, DeptID, Salary,
       DENSE_RANK() OVER (
           PARTITION BY DeptID
           ORDER BY Salary DESC
       ) AS DeptSalaryRank
FROM Employee;
```

### 12. Orders above average amount

``` sql
SELECT *
FROM Orders
WHERE Amount > (SELECT AVG(Amount) FROM Orders);
```

### 13. Hired in last 30 days

The exact date expression varies. In MySQL:

``` sql
SELECT *
FROM Employee
WHERE HireDate >= CURRENT_DATE - INTERVAL 30 DAY;
```

In PostgreSQL:

``` sql
SELECT *
FROM Employee
WHERE HireDate >= CURRENT_DATE - INTERVAL '30 days';
```

### 14. Raise salaries below company average

``` sql
UPDATE Employee
SET Salary = Salary * 1.05
WHERE Salary < (SELECT AvgSalary
                FROM (SELECT AVG(Salary) AS AvgSalary FROM Employee) x);
```

Some database engines restrict this form of subquery in an update. Adapt
it to your DBMS and preview affected rows before updating.

### 15. Rows in `TableA` without a matching key in `TableB`

``` sql
SELECT a.*
FROM TableA a
WHERE NOT EXISTS (
    SELECT 1 FROM TableB b
    WHERE b.ID = a.ID
);
```

------------------------------------------------------------------------

# Final Interview Revision: Which technique should I choose?

  ------------------------------------------------------------------------------------
  Requirement             Strong default technique             Watch out for
  ----------------------- ------------------------------------ -----------------------
  Highest / lowest value  `MAX()` / `MIN()`                    Returns a value, not
                                                               employee details

  Nth-highest distinct    `DENSE_RANK()`                       Handles ties as one
  salary                                                       salary rank

  Exactly Nth row         `ROW_NUMBER()` or `LIMIT/OFFSET`     Add a deterministic
                                                               tie-breaker

  Aggregate filter        `HAVING`                             `WHERE` filters
                                                               individual rows

  Keep unmatched          `LEFT JOIN`                          Right-side filters in
  left-side rows                                               `WHERE` may remove them

  Find missing related    `NOT EXISTS`                         Usually safer than
  rows                                                         `NOT IN` with `NULL`

  Find latest/first row   `ROW_NUMBER()`                       Define tie-breaker
  per group                                                    behavior

  Running total           `SUM() OVER (...)`                   Specify ordering and
                                                               frame

  Find duplicates         `GROUP BY ... HAVING COUNT(*) > 1`   Decide which columns
                                                               define a duplicate

  Count rows including    `LEFT JOIN` +                        Avoid `COUNT(*)` for
  unmatched groups        `COUNT(right_table.key)`             empty groups
  ------------------------------------------------------------------------------------

## Last-minute reminders

-   Learn `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, joins,
    subqueries, and window functions thoroughly.
-   Clarify whether "second highest" means **second distinct value** or
    **second row after sorting**.
-   Clarify how ties should be handled.
-   `NULL` is not equal to anything, including another `NULL`; use
    `IS NULL`.
-   `WHERE` filters rows; `HAVING` filters groups.
-   `UNION` removes duplicate result rows; `UNION ALL` preserves them.
-   `INNER JOIN` returns matching rows; `LEFT JOIN` preserves all rows
    from the left table.
-   Always test `UPDATE` and `DELETE` conditions with a `SELECT` first.
-   Syntax for `LIMIT`, date arithmetic, casting, and `DELETE` with
    window functions can vary by SQL engine.
