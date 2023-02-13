# SQL_ASSIGNMENT
<img width="622" alt="Screenshot 2023-02-13 at 12 39 41 PM" src="https://user-images.githubusercontent.com/122535424/218393367-07ba2274-c8a7-4e2f-8979-b52eee50bdcd.png">

<img width="627" alt="Screenshot 2023-02-13 at 12 39 53 PM" src="https://user-images.githubusercontent.com/122535424/218393430-7a1e3a5b-1efe-4586-ab95-93d74f2153e6.png">

### SQL COMMANDS

#### Create and use database

```
CREATE database `Sqlassignment` ;
USE `Sqlassignment`;
```

#### Create the table employee given in the question

```
create table employees (
empid integer(4) not null unique,
emp_name varchar(30),
Gender varchar(10),
department varchar(30),
check(Gender in ("Male","Female")));
```

"emp_id" - An integer column with a maximum size of 4 digits. It cannot be NULL and must be unique across all records in the table, which is used to identify every record.
"emp_name" - A column with a maximum length of 30 characters to represent employee names.
"Gender" - a column to represent gender of the employee which has a check in place to only allow "male" or "female" inputs.
"Department" - a column to represent the department of the employee.

#### Insertion into table - 

```
Insert into employees values(1,'X','Female','Finance'),(2,'Y','Male','IT'),(3,'Z','Male','HR'),(4,'W','Female','IT');
```
#### Checking null values for departments
```
Insert into employees values(5,'X','Female',null);
```

#### Query to find the number of employees per department at the same time trying to handle the above case where department is null by displaying “not assigned”

```
SELECT IFNULL(Department,'Not Assigned') as Department,
    COUNT(CASE WHEN UPPER(Gender)='MALE' THEN 1 END) AS 'Num of Male',
    COUNT(CASE WHEN UPPER(Gender)='FEMALE' THEN 1 END) AS 'Num of Female'
FROM employees GROUP BY Department;
```

#### Using Procedures

<img width="387" alt="Screenshot 2023-02-13 at 3 25 58 PM" src="https://user-images.githubusercontent.com/122535424/218435337-74ae4692-ae36-41cd-bf9b-86c666ed3c67.png">

```
DELIMITER &&  
mysql> CREATE PROCEDURE get_num_of_male_and_female ()
    -> BEGIN  
    -> SELECT 
    ->   IFNULL(Department, 'Not Assigned') as Department, 
    ->   COUNT(
    ->     CASE WHEN UPPER(Gender)= 'MALE' THEN 1 END
    ->   ) AS 'Num of Male', 
    ->   COUNT(
    ->     CASE WHEN UPPER(Gender)= 'FEMALE' THEN 1 END
    ->   ) AS 'Num of Female' 
    -> FROM 
    ->   employees 
    -> GROUP BY 
    ->   Department 
    -> order by 
    ->   Department;
    -> END &&
 ```

As we see above while inserting we can give null values to department so to handle cases where department is not given we use the function IFNULL to replace where ever there is a null to "Not Assigned".

Upper function here is used to make all the values in the gender column to uppercase to make it easy to equate if "FEMALE" or "MALE"

<img width="534" alt="Screenshot 2023-02-13 at 4 06 20 PM" src="https://user-images.githubusercontent.com/122535424/218435555-aafb4980-b6d6-4977-82f2-5aa0fdb222be.png">

<img width="894" alt="Screenshot 2023-02-13 at 4 09 03 PM" src="https://user-images.githubusercontent.com/122535424/218436204-e3876163-e1dc-46bf-8dc8-04e28c156b65.png">

#### To create table employeesalaries like above

```
create table employeesalaries (
    -> emp_name varchar(30) not null,
    -> Jan Float(15,2) Not null default 0,
    -> Feb Float(15,2) Not null default 0,
    -> March Float(15,2) Not null default 0,
    -> check(Jan>=0 
             and Feb >=0 
             and March >=0));
```

->the above table has 4 columns, 
1)empname as varchar to represnt employee names and the other 3 columns Jan,Feb and March to show the salaries on that month of the employee which can not be null and is deafulted to 0 if no value is entered in that column and the check constraint are imposed on these three columns to avoid values being less than zero.

#### Insertion into the table employeesalaries
```
Insert into employeesalaries values
('X',5200,9093,3832),
('Y',9023,8942,4000),
('Z',9834,8197,9903),
('W',3244,4321,0293);

Insert into employeesalaries values('V',100,100,null);
//ERROR IS THROWN as march column is marked not null
```
### Query to get salaries of employees of different months , find the max amount from the rows with month name 
```
select emp_name as Name,value,case when idx=1 then 'Jan' when idx=2 then 'Feb' when idx=3 then 'Mar' end as Month from (select emp_name,greatest(Jan, Feb, March) as value,field(greatest(Jan, Feb, March), Jan, Feb, March) as idx from  employeesalaries) emps;
```
### Procedure to run above query
```
DELIMITER &&  
mysql> CREATE PROCEDURE max_amount_from_rows_with_month_name()  
    -> BEGIN  
    -> select 
    ->   emp_name as Name, 
    ->   value, 
    ->   case when idx = 1 then 'Jan' when idx = 2 then 'Feb' when idx = 3 then 'Mar' end as Month 
    -> from 
    ->   (
    ->     select 
    ->       emp_name, 
    ->       greatest(Jan, Feb, March) as value, 
    ->       field(
    ->         greatest(Jan, Feb, March), 
    ->         Jan, 
    ->         Feb, 
    ->         March
    ->       ) as idx 
    ->     from 
    ->       employeesalaries
    ->   ) emps;
    -> END &&  

```
The above procedure selects three columns, name of the employee, value to store the largest salary , and month.
The greatest function is used to get the highest salary per employee in the columns in Jan, Feb and March.
the feild function is used to get the month where the highest salary exists

<img width="730" alt="Screenshot 2023-02-13 at 5 01 00 PM" src="https://user-images.githubusercontent.com/122535424/218446567-f7dd2aab-e85e-4559-a21a-d3dfebc90e2c.png">

<img width="633" alt="Screenshot 2023-02-13 at 5 01 23 PM" src="https://user-images.githubusercontent.com/122535424/218446626-6547854a-ed89-45d2-ac2e-f8fa98b7e423.png">

<img width="626" alt="Screenshot 2023-02-13 at 5 01 48 PM" src="https://user-images.githubusercontent.com/122535424/218446744-fcb69845-fede-4b37-a4b9-0b65dfeab382.png">

### Create table test like above
```
create table test (
    -> candidate_id integer(4) not null unique,
    -> marks float(10,2) default 0);
 ```
 ### Insert the above values into the table test
 
 ```
 Insert into test values 
 (1,98),
 (2,78),
 (3,87),
 (4,98),
 (5,78);
 ```

### Query to rank students based on the marks and showing student id.

```
SELECT Marks,GROUP_CONCAT(Candidate_id) as Candidate_id, dense_rank() OVER (order by marks desc ) as 'rank'
    ->    FROM test
    -> GROUP BY marks;
```

### Procedure
```
DELIMITER &&  
mysql> CREATE PROCEDURE rank_in_order ()  
    -> BEGIN  
    -> SELECT 
    ->   Marks, 
    ->   dense_rank() OVER (
    ->     order by 
    ->       marks desc
    ->   ) as 'Rank', 
    ->   GROUP_CONCAT(Candidate_id) as Candidate_id 
    -> FROM 
    ->   test 
    -> GROUP BY 
    ->   marks;
    -> END &&  
DELIMITER ; 
```
The above procedure selects the three columns Marks, Rank and candidate id
the dense rank function calculates the rank of the students on the marks achieved
the ranks are grouped together so that two students who score the same marks are given the same rank instead of different ranks


<img width="383" alt="Screenshot 2023-02-13 at 5 37 33 PM" src="https://user-images.githubusercontent.com/122535424/218453763-8be229fa-f7b1-4b88-ab5f-b53d562f7415.png">

<img width="1440" alt="Screenshot 2023-02-13 at 5 43 26 PM" src="https://user-images.githubusercontent.com/122535424/218454812-33d146d0-b35b-4621-86c0-025d41ff3f5e.png">




 











