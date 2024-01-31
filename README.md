# SQL-Case-Study

Objective:
Generate an output table using UiPath to identify employees from different departments
who have the
same highest salary. The goal is to list employees alongside their departments and salaries in the output table


Query writing:
use college;

Create Tables and Insert values:

create table department(department_ID int, name varchar(50), primary
key(department_ID));

create table employee(department_ID int, name varchar(50), salary int, foreign key(department_ID) references department(department_ID));

insert into department(department_ID,name) values(1,'IT'),(2,'Sales');

insert into employee(name,salary,department_ID)
values('Joe',70000,1),('Jim',90000,1),('Henry',80000,2),('Sam',60000,2),('max',90000,1);


Display Tables:
select * from department;
+---------------+-------+
| department_ID | name  |
+---------------+-------+
|      1        | IT    |
|      2        | Sales |
+---------------+-------+

select * from employee;

Query for final Output which displaying Highest salary from Different department:

select d.name as Department, e.name as Employee, e.salary from
department d right join employee e on d.department_ID=e.department_ID where e.salary
in (select max(e.salary) from employee e group by d.name, e.department_ID);
