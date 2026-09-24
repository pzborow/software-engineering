# Window funciton and name of employee with max salary

```sql
WITH RankedEmployees AS (
    SELECT DeptID, EmpName, Salary,
           ROW_NUMBER() OVER(PARTITION BY DeptID ORDER BY Salary DESC) AS RowNum
    FROM Employee
)
SELECT DeptID, EmpName, Salary
FROM RankedEmployees
WHERE RowNum = 1;
```