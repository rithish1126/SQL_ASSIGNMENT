# SQL_ASSIGNMENT
<img width="622" alt="Screenshot 2023-02-13 at 12 39 41 PM" src="https://user-images.githubusercontent.com/122535424/218393367-07ba2274-c8a7-4e2f-8979-b52eee50bdcd.png">

<img width="627" alt="Screenshot 2023-02-13 at 12 39 53 PM" src="https://user-images.githubusercontent.com/122535424/218393430-7a1e3a5b-1efe-4586-ab95-93d74f2153e6.png">

###SQL COMMANDS

####Create and use database

'''
CREATE database `Sqlassignment` ;
USE `Sqlassignment`;
'''

#### Create the table employee given in the question

'''
create table employees (
empid integer(4) not null unique,
emp_name varchar(30),
Gender varchar(10),
department varchar(30),
check(Gender in ("Male","Female")));
'''

"emp_id" - An integer column with a maximum size of 4 digits. It cannot be NULL and must be unique across all records in the table, which is used to identify every record.
"emp_name" - A column with a maximum length of 30 characters to represent employee names.
"Gender" - a column to represent gender of the employee which has a check in place to only allow "male" or "female" inputs.
"Department" - a column to represent the department of the employee.

#### Insertion into table - 

'''
Insert into employees values(1,'X','Female','Finance'),(2,'Y','Male','IT'),(3,'Z','Male','HR'),(4,'W','Female','IT');
'''
####checking null values for departments
Insert into employees values(5,'X','Female',null);

####Query to find the number of employees per department at the same time trying to handle the above case where department is null by displaying “not assigned”

'''
SELECT IFNULL(Department,'Not Assigned') as Department,
    COUNT(CASE WHEN UPPER(Gender)='MALE' THEN 1 END) AS 'Num of Male',
    COUNT(CASE WHEN UPPER(Gender)='FEMALE' THEN 1 END) AS 'Num of Female'
FROM employees GROUP BY Department;

'''
#### using procedures

<img width="387" alt="Screenshot 2023-02-13 at 3 25 58 PM" src="https://user-images.githubusercontent.com/122535424/218435337-74ae4692-ae36-41cd-bf9b-86c666ed3c67.png">

'''
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
 '''

As we see above while inserting we can give null values to department so to handle cases where department is not given we use the function IFNULL to replace where ever there is a null to "Not Assigned".

Upper function here is used to make all the values in the gender column to uppercase to make it easy to equate if "FEMALE" or "MALE"

<img width="534" alt="Screenshot 2023-02-13 at 4 06 20 PM" src="https://user-images.githubusercontent.com/122535424/218435555-aafb4980-b6d6-4977-82f2-5aa0fdb222be.png">

<img width="894" alt="Screenshot 2023-02-13 at 4 09 03 PM" src="https://user-images.githubusercontent.com/122535424/218436204-e3876163-e1dc-46bf-8dc8-04e28c156b65.png">

###To create table employeesalaries like above









