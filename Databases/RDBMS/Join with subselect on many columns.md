# Join with subselect on many columns

```sql
SELECT DeptID, EmpName, Salary
FROM Employee
WHERE (DeptID, Salary) IN (
    SELECT DeptID, MAX(Salary)
    FROM Employee
    GROUP BY DeptID
);
```