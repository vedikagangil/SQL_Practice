# SQL_Practice

show databases;

create database VIT;

drop database VIT;

use VIT;

create table CSE(
s_id int,
s_name varchar(30),
s_mark int
);

show tables from VIT;

drop table CSE;

select * from CSE;

insert into CSE values(10001, 'Vedika', 8);

create database COLLEGE;

use COLLEGE;
create table STUDENT_DATA(
std_id int,
std_name varchar(30),
std_cgpa int
);

show tables from COLLEGE;

select * from STUDENT_DATA;

insert into STUDENT_DATA
values
(10001, 'Vedika Gangil', 9),
(10002, 'Asmita Sakhare', 9),
(10003, 'Nihalika Kumari', 9),
(10004, 'Rishav Raj', 8),
(10005, 'Krishna Sahu', 7);

alter table STUDENT_DATA add(
std_age int);

desc STUDENT_DATA;

alter table STUDENT_DATA drop column std_age;

alter table STUDENT_DATA add(
s_country varchar(25) default 'India'
);

alter table STUDENT_DATA rename column
s_country to std_country;

delete from STUDENT_DATA where std_id=10004;

update STUDENT_DATA set std_cgpa = 6 where std_id = 10005;

update STUDENT_DATA set std_cgpa = std_cgpa + 1;

select std_name from STUDENT_DATA;

select std_name, std_cgpa from STUDENT_DATA;

select std_name from STUDENT_DATA where std_cgpa = 10;





CREATE DATABASE practice1;

USE practice1;

CREATE TABLE mech(s_id int, s_name varchar(25));

START TRANSACTION;

INSERT INTO mech VALUES(1001, 'Vedika');

SAVEPOINT A;

UPDATE mech SET s_id = 1002 WHERE s_id = 1001;

SAVEPOINT B;

INSERT INTO mech VALUES(1003, 'Asmita');

SELECT * FROM mech;

SAVEPOINT C;





CREATE DATABASE ORG123;

SHOW DATABASES;

USE ORG123;

CREATE TABLE Worker (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT(15),
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'),
		(008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');
        
SELECT * FROM worker WHERE salary BETWEEN 100000 AND 300000;

SELECT * FROM worker WHERE salary > 100000 AND department = 'HR';

SELECT * FROM worker WHERE salary > 200000;

SELECT * FROM worker WHERE salary NOT BETWEEN 100000 AND 300000;

SELECT * FROM worker WHERE salary BETWEEN 200000 AND 400000
AND worker_id IN (1, 2, 3, 4, 5);

SELECT MIN(salary) FROM worker WHERE department = 'HR';

SELECT * FROM worker WHERE department = 'HR'
AND salary = (SELECT MIN(salary) FROM worker where department = 'HR');

SELECT * FROM worker;

SELECT * FROM worker WHERE department = 'Admin' OR 'HR' OR 'Account'
AND salary = (SELECT MAX(salary) FROM worker where department = 'Admin' OR 'HR' OR 'Account');

SELECT * FROM Worker w
WHERE SALARY = (
    SELECT MAX(SALARY) 
    FROM Worker 
    WHERE DEPARTMENT = w.DEPARTMENT);

SELECT * FROM Worker 
WHERE DEPARTMENT = 'Account' 
AND (SALARY = (SELECT MAX(SALARY) FROM Worker WHERE DEPARTMENT = 'Account') 
OR SALARY = (SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT = 'Account'));

USE org123;

SELECT * FROM worker;

SELECT DISTINCT(department) FROM worker;

SELECT worker_id AS emp_code FROM worker;

SELECT department, worker_id FROM worker WHERE department = 'HR'
UNION
SELECT department, worker_id FROM worker WHERE department = 'Account';

SELECT worker_id, first_name, department,
CASE
    WHEN salary > 300000 THEN 'Upper class'
    WHEN salary <=300000 && salary >=100000 THEN 'Middle class'
    ELSE 'Lower class'
END 
AS People_stage_wise
FROM worker;

SELECT * FROM worker WHERE department = 'Admin' ORDER BY salary;

SELECT * FROM worker WHERE department = 'Admin' ORDER BY salary DESC;

SELECT * FROM worker WHERE department = 'Admin' ORDER BY salary LIMIT 1;





SHOW DATABASES;

USE practice1;

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

ALTER TABLE Persons
MODIFY Age int NOT NULL;

ALTER TABLE Persons
ADD UNIQUE (ID);

ALTER TABLE Persons
ADD UNIQUE (LastName);

ALTER TABLE Persons
ADD UNIQUE (FirstName);

ALTER TABLE Persons
DROP CONSTRAINT LastName;

ALTER TABLE Persons
DROP CONSTRAINT FirstName;

ALTER TABLE Persons
ADD PRIMARY KEY (ID);

ALTER TABLE Persons
DROP PRIMARY KEY;

SELECT * FROM Persons;

DESC Persons;
SELECT department, COUNT(department) AS total_employees FROM worker
where department = 'HR' OR department = 'Account' GROUP BY department;

SELECT department, COUNT(department) AS total_employees FROM worker
GROUP BY department
ORDER BY total_employees DESC LIMIT 2;
