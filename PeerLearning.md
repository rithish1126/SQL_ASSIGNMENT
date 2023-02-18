# Peer Learning

Question 1: 
<img width="526" alt="Screenshot 2023-02-18 at 5 11 06 PM" src="https://user-images.githubusercontent.com/122535424/219862002-93b5bab4-93c3-4bf7-8ecc-b6f813b4ce0d.png">

Pankaj's Approach
```
SELECT Department,
SUM(CASE WHEN Gender = 'Male' THEN 1 ELSE 0 END) AS "Num of male",
SUM(CASE WHEN Gender = 'Female' THEN 1 ELSE 0 END) AS "Num of Female"
FROM employees
GROUP BY Department;
```
Kushagra's Approach
```
SELECT department, 
       SUM(CASE WHEN gender = 'male' THEN 1 ELSE 0 END) AS Num_of_male, 
       SUM(CASE WHEN gender = 'female' THEN 1 ELSE 0 END) AS Num_of_female
FROM employees
GROUP BY department;
```


Here Pankaj has selected 3 columns and has used "CASE" statements to find when the record is male and female but hasn't accounted if inputs are in different case and then used "SUM" statement to find the sum of the number of males and females. And Kushagra on the other hand has used the simillar approach.

Question 2:

<img width="534" alt="Screenshot 2023-02-18 at 5 21 54 PM" src="https://user-images.githubusercontent.com/122535424/219864153-471bd813-e0ca-4a46-9d69-5743cf60c412.png">
Pankaj's approach
```
SELECT Name, 
  ANY_VALUE(CASE 
    WHEN Jan = GREATEST(Jan, Feb, Mar) THEN 'Jan'
    WHEN Feb = GREATEST(Jan, Feb, Mar) THEN 'Feb'
    WHEN Mar = GREATEST(Jan, Feb, Mar) THEN 'Mar'
  END) AS Month,
  GREATEST(Jan, Feb, Mar) AS Value
FROM emp_salary
```
Kushagra's approach
```
SELECT Name,
GREATEST(Jan, Feb, Mar) AS Value,
ANY_VALUE(CASE
  WHEN Jan = GREATEST(Jan, Feb, Mar) THEN 'Jan'
  WHEN Feb = GREATEST(Jan, Feb, Mar) THEN 'Feb'
  WHEN Mar = GREATEST(Jan, Feb, Mar) THEN 'Mar'
  END) AS Month
FROM salary;
```

Here Pankaj has selected three columns from the table emp_salary and has used a "CASE" statement to go per 




