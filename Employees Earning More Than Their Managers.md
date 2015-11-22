# Employees Earning More Than Their Managers

https://leetcode.com/problems/employees-earning-more-than-their-managers/
<pre>
Employees Earning More Than Their Managers

The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.

+----------+
| Employee |
+----------+
| Joe      |
+----------+
</pre>

思考分解问题，如何得到该员工的manager的工资？

Solution:

My solution:select emp1.name from Employee emp1, Employee emp2 where emp1.ManagerId=emp2.Id and (emp1.salary>emp2.salary);

SELECT employer.Name
    FROM  Employee employer JOIN Employee manager ON (employer.ManagerId = manager.Id )
      WHERE employer.Salary > manager.Salary ;
      

select Name as Employee from Employee e where Salary>(select Salary from Employee where Id=e.ManagerId);


select E1.Name from Employee E1 inner join Employee E2 on E1.ManagerID=E2.ID where E1.Salary>E2.Salary;      
      