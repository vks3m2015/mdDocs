
Employee(ID, Name, Salary)

| ID | NAME | SALARY | 
| -- | -- | -- |
| 1	| Jai | 3000 |
| 2	| Raj |	2000 |
| 3	| Karan | 4000 |
| 4	| Manoj | 3000 |
| 5	| Raju | 1000 |

Find Employee having max salary-

Method 1 Sorting 
---------
```sh
SELECT * 
FROM Employee 
ORDER BY salary DESC 
LIMIT 1 
```

Method 2  Using max function
----------

using max function we can not get entire row info without any subquery
```sh

SELECT * 
FROM Employee 
WHERE salary = (SELECT MAX(salary) FROM Employee)

```
it will be long query if there is any other derived table instead of Employee table. Also then we need to use that derived table at two places (like here using Employee table in Query and subquery also)  


Method 3 Self Join
--------------------
```sh
SELECT e1.id, e1.name, e1.salary 
FROM Employee e1 
  LEFT JOIN Employee e2 ON e1.salary < e2.salary 
WHERE e2.salary IS NULL
```