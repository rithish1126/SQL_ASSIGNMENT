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

Here Pankaj has selected three columns from the table emp_salary , The name as in the employee name , the value by finding the greatest value from the three columns, and then he maps the greatest value in the record to the month it belongs by using the case statement. While the same thing is done by kushagra. 

<img width="623" alt="Screenshot 2023-02-19 at 5 31 37 PM" src="https://user-images.githubusercontent.com/122535424/219946595-1b883ea0-1fd5-4fe6-a22a-268bf741dff7.png">

Pankaj's approach
```
SELECT Marks, 
       DENSE_RANK() OVER (ORDER BY Marks DESC) AS `Ranking`, 
       GROUP_CONCAT(Candidate_ID ORDER BY Candidate_ID ASC) AS Candidate_ID
FROM candidate_marks
GROUP BY Marks
ORDER BY `Ranking`;
```
Kushagra's Approach
```
SELECT Marks,
DENSE_RANK() OVER (ORDER BY Marks DESC) AS `Rank`,
GROUP_CONCAT(Candidate_ID ORDER BY Candidate_ID ASC) AS
Candidate_ID
FROM marks
GROUP BY Marks
ORDER BY `Rank`;

```
Here Pankaj has used a similar approach as me he has first used dense rank function to rank all the records given to it, here he has given the marks in the descending order to the dense function and then has used the group_concat function  that agregates multiple row values in one field.

<img width="611" alt="Screenshot 2023-02-19 at 6 15 58 PM" src="https://user-images.githubusercontent.com/122535424/219948824-d4225aff-e195-4875-ad45-e7d844f4bbf9.png">

Pankaj's Approach

```
DELETE c1
FROM candidate_emails c1
JOIN candidate_emails c2
ON c1.Email = c2.Email AND c1.Candidate_ID > c2.Candidate_ID;
```
Kushagra's Approach
```
DELETE c1
FROM ID c1
JOIN ID c2
ON c1.Email = c2.Email AND c1.Candidate_ID > c2.Candidate_ID;

```
Here pankaj and kushagra have used a very simple approach contradictory to mine where I've used multiple subqueries to find the duplicate mail_ids and then deleted them except for the mail ids with minimum candidate id while pankaj and kushagra just did an inner join and set condidtions on this join.


