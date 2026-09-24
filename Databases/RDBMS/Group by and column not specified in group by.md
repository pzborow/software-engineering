# Group by and column not specified in group by

```sql
SELECT DeptID, EmpName, MAX(Salary) AS MaxSalary
FROM Employee
GROUP BY DeptID;
```
Do weryfikacji czy zadziała, bo EmpName nie wchodzi w skład group by