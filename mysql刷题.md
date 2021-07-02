##### 2020.08.07

1.[组合两个表](https://leetcode-cn.com/problems/combine-two-tables/)

```mssql
表1: Person
+-------------+---------+
| 列名         | 类型     |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId 是上表主键

表2: Address
+-------------+---------+
| 列名         | 类型    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId 是上表主键
 
编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：
FirstName, LastName, City, State

# Write your MySQL query statement below
select FirstName,LastName,City,State 
from Person p left join Address a
on p.PersonId = a.PersonId
```



2.[第二高的薪水](https://leetcode-cn.com/problems/second-highest-salary/)

```mysql
编写一个 SQL 查询，获取 Employee 表中第二高的薪水（Salary） 。

+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
例如上述 Employee 表，SQL查询应该返回 200 作为第二高的薪水。如果不存在第二高的薪水，那么查询应返回 null。

+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+

# Write your MySQL query statement below
# 需要注意重点ifnull，limit offset
select ifnull(
    (select distinct Salary 
    from Employee order by Salary desc
    limit 1 offset 1),null) 
as 'SecondHighestSalary'

```





