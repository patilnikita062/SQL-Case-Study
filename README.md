# SQL-Case-Study

Objective:
Generate an output table using UiPath to identify employees from different departments
who have the
same highest salary. The goal is to list employees alongside their departments and salaries in the output table
------------------------------------------------------------------------------------------------------------------------- Query writing:
C:\Users\patil>cd\
C:\>cd xampp\mysql\bin
C:\xampp\mysql\bin>mysql -h localhost -u root
Welcome to the MariaDB monitor. Commands end with ; or \g. Your MariaDB connection id is 26
Server version: 10.4.32-MariaDB mariadb.org binary distribution
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others. Type 'help;' or '\h' for help. Type '\c' to clear the current input statement. MariaDB [(none)]> use college;
Database changed
-------------------------------------------------------------------------------------------------------------------------- Create Tables and Insert values:
MariaDB [college]> create table department(department_ID int, name varchar(50), primary
key(department_ID));
Query OK, 0 rows affected (0.023 sec)
MariaDB [college]> create table employee(department_ID int, name varchar(50), salary int, foreign key(department_ID) references department(department_ID));
Query OK, 0 rows affected (0.047 sec)
MariaDB [college]> insert into department(department_ID,name) values(1,'IT'),(2,'Sales');
Query OK, 2 rows affected (0.014 sec)
Records: 2 Duplicates: 0 Warnings: 0
MariaDB [college]> insert into employee(name,salary,department_ID)
values('Joe',70000,1),('Jim',90000,1),('Henry',80000,2),('Sam',60000,2),('max',90000,1);
Query OK, 5 rows affected (0.018 sec)
Records: 5 Duplicates: 0 Warnings: 0

Display Tables:
MariaDB [college]> select * from department;
+---------------+-------+
| department_ID | name |
+---------------+-------+
| 1 | IT |
| 2 | Sales |
+---------------+-------+
2 rows in set (0.000 sec)
MariaDB [college]> select * from employee;
+---------------+-------+--------+
| department_ID | name | salary |
+---------------+-------+--------+
| 1 | Joe | 70000 |
| 1 | Jim | 90000 |
| 2 | Henry | 80000 |
| 2 | Sam | 60000 |
| 1 | max | 90000 |
+---------------+-------+--------+
5 rows in set (0.000 sec) 
---------------------------------------------------------------------------------------------------------------------- Query for final Output which displaying Highest salary from Different department:
MariaDB [college]> select d.name as Department, e.name as Employee, e.salary from
department d right join employee e on d.department_ID=e.department_ID where e.salary
in (select max(e.salary) from employee e group by d.name, e.department_ID);
+------------+----------+--------+
| Department | Employee | salary |
+------------+----------+--------+
| IT | Jim | 90000 |
| Sales | Henry | 80000 |
| IT | max | 90000 |
+------------+----------+--------+
3 rows in set (0.001 sec)
