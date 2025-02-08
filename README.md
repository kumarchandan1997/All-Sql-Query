# Important Sql Query

### Create computer table used for JOINS problem.
```sql
 CREATE TABLE COMPUTER (
    COMPID INT PRIMARY KEY AUTO_INCREMENT,
    BRAND VARCHAR(50),
    COMPMODEL VARCHAR(50),
    MANUFACTUREDATE DATE
);
```

### Create EMPLOYEE table
```sql

    CREATE TABLE EMPLOYEE (
        EMPID INT(5) PRIMARY KEY,
        FIRSTNAME VARCHAR(50),
        LASTNAME VARCHAR(50),
        SALARY DECIMAL(8,2),
        EMAILID VARCHAR(50),
        MANAGERID INT(5),
        DATEOFJOINING DATE,
        DEPT VARCHAR(10),
        COMPID INT(10),
        CONSTRAINT FK_COMPID FOREIGN KEY (COMPID) REFERENCES COMPUTER(COMPID)
    );

```


### 1. SQL Query to update DateOfJoining to 15-jul-2012 for empid =1.

```sql
  UPDATE EMPLOYEE SET DATEOFJOINING = ’15-JUL-2012’ WHERE EMPID =1;
```

### 2. SQL Query to select all student name where age is greater than 22

```sql
 SELECT * FROM STUDENT WHERE AGE > 22;
```

### 3.SQL Query to Find all employee with Salary between 40000 and 80000?

```sql
  SELECT * FROM EMPLOYEE WHERE SALARY BETWEEN 40000 AND 80000;

  SELECT * FROM EMPLOYEE WHERE SALARY >=40000 AND SALARY <=80000;
```

### 4.SQL Query to display full name?
```sql
    SELECT CONCAT (FIRSTNAME, LASTNAME) FROM EMPLOYEE;

```

### 5.SQL Query to find name of employee beginning with S?

```sql
   SELECT * FROM EMPLOYEE WHERE FIRSTNAME LIKE ‘S%’;
  ```

  ### 6.Write a query to fetch details of employees whose firstname ends with an alphabet ‘A’ and contains exactly five alphabets ?

  ```sql
    SELECT * FROM EMPLOYEE WHERE FIRSTNAME LIKE ‘____A’;
  ```

  ### 7.Write a query to fetch details of all employees excluding few Employees 

  ```sql
   SELECT * FROM EMPLOYEE WHERE FIRSTNAME NOT IN (‘BIPLAB’,’DISHA’);
  ```

  ### 8.Write an SQL query to fetch the domain from an email address:
  ```sql
    SELECT SUBSTRING (EMAILID, INSTR(EMAILID,"@")+1) FROM EMPLOYEE;

  ```
  ### 9.Write an SQL query to fetch all the Employees details from Employee table who joined in the Year 2020:
  ```sql
   SELECT * FROM EMPLOYEE WHERE TO_CHAR(DATEOFJOINING,’YYYY’)=2020;
  ```

  ### 10.Write an SQL query to fetch only odd rows / Even rows from the table :
  ```sql
   SELECT * FROM EMPLOYEE WHERE mod(EMPID,2) = 0;
  ```

  ### 11.Write an SQL query to create a new table with data and structure copied from another table:
  ```sql
  CREATE TABLE EMP AS (SELECT * FROM EMPLOYEE);
   
  ```
  ### 12.Write an SQL query to create an empty table with the same structure as some other table :
  ```sql
   CREATE TABLE EMP2 AS (SELECT * FORM EMPLOYEE WHERE 1=2);
   ```

 ### 13.Find the first employee and last employee from employee table :
 ```sql
  SELECT * FROM EMPLOYEE WHERE EMPID = (SELECT MIN(EMPID) FROM EMPLOYEE);

  SELECT * FROM EMPLOYEE WHERE EMPID = (SELECT MAX(EMPID) FROM EMPLOYEE);

 ```

 ### 14.Write a query to fetch the department-wise count of employees sorted by department’s count in ascending order:
 ```sql
  SELECT DEPT, COUNT (*) FROM EMPLOYEE GROUP BY DEPT ORDER BY COUNT(*);
 ```

 ### 15.Write a query to retrieve Departments who have less than 4 employees working in it :
 ```sql
 SELECT DEPT, COUNT (*) FROM EMPLOYEE GROUP BY DEPT HAVING COUNT(*) < 4;
   ```

   ### 15.Write a query to retrieve Department wise Maximum salary:
   ```sql
    SELECT DEPT, MAX(SALARY) FROM EMPLOYEE GROUP BY DEPT;

   ```

   ### 16.Write a query to Employee earning maximum salary in his department :

   ```sql
   SELECT * FROM EMPLOYEE E1 JOIN (
    SELECT DEPT, MAX(SALARY) SAL FROM EMPLOYEE GROUP BY DEPT) E2
    ON E1.DEPT = E2.DEPT AND E1.SALARY = E2.SAL;
    ```

    ### 17.Write an SQL query to fetch the first 50% records from a table:
    ```sql
    SELECT * FROM Customers LIMIT (select COUNT(*)/2 from Customers);
```

 ### 17.Query to fetch details of employees not having computer:
 ```sql
  SELECT * FROM EMPLOYEE WHERE COMPID IS NULL;
```

### 18.Query to fetch employee details along with the computer details who have been assigned with a computer :
```sql
    SELECT * FROM EMPLOYEE E JOIN COMPUTER C ON E.COMPID = C.COMPID;

```

 ### 19.Find Nth Highest salary :
```sql
  SELECT DISTINCT SALARY FROM EMPLOYEE E1
    WHERE N = (SELECT COUNT(DISTINCT SALARY)
    FROM EMPLOYEE E2 WHERE E2.SALARY > E1.SALARY);
  ```

  ### 20.Full Outer join in mysql
  ```sql
    SELECT e.employee_id, e.employee_name, e.salary, d.department_name
FROM Employees e
LEFT JOIN Departments d ON e.department_id = d.department_id

UNION

SELECT e.employee_id, e.employee_name, e.salary, d.department_name
FROM Employees e
RIGHT JOIN Departments d ON e.department_id = d.department_id

LIMIT 25;
```

### 21. CROSS JOIN (Returns Cartesian product - all combinations)
```sql
SELECT e.employee_name, d.department_name
FROM Employees e
CROSS JOIN Departments d;
```
### 22.SELF JOIN (Comparing Employees with Higher Salaries in the Same Department)
```sql
SELECT e1.employee_name AS Employee, e1.salary, e2.employee_name AS Higher_Salary_Employee, e2.salary
FROM Employees e1
JOIN Employees e2 ON e1.department_id = e2.department_id AND e1.salary < e2.salary;
```
### 23.List out department_id having atleast 3 employees
```sql
  select department_id , count(*) from employee GROUP by department_id having count(*) >=3;
```
### 24.How many employees who are working in different departments wise in organization
```sql
  select department_id , count(*) from employee GROUP by department_id;
  ```
### 25.Dispaly employee who got maximum salary
```sql  
    select * from employee where salary = (select max(salary) from employee);
```
### 26.Dispaly the employee who are working in sales department ?
```sql
 select * from employee where department_id in (select department_id from department where name='sales');
 ```
### 26.Dispaly the employee who are working in "new York" ?
 ## table structure are
  1.employee(employee_id,last_name,first_name,department_id)
  2.department(department_id,name,location_id)
  3.location(loaction_id,regional_group)
  ```sql
  select * from employee where department_id =
   (select department_id from department where loaction_id
   =(select location_id from location where regional_group="new york"));
  ```
### 27.update the employee salary , who are working as manager by base of 10%
```sql
 update employee set salary = salary*10/100 where  job_id=(select job_id from job where function ='manager');
 ```
 ### 28.Delete employee who are working in Accounting department ?
 ```sql
  delete from employee where department_id = (select department_id from department
    where name = 'Accounting');
```
### 29.Dispaly second higest salary from employee table
```sql
 select salary from employee order by salary desc limit 1,1;

 select salary from employee e1 where N-1 =(select count(distinct salary) from employee e2 
 where e2.salary>e1.salary);
```
### 30.Linit and offset
```sql
SELECT * FROM Employees
LIMIT 5 OFFSET 10;  -- Skips first 10 rows, then returns the next 5 rows
```
### 31.Delete Dublicate records from employee
```sql
Delete e1
from employee e1 join employee e2
on e1.employee_name = e2.employee_name
and e1.department_id <=> e2.department_id
and e1.salary=e2.salary
and e1.employee_id > e2.employee_id;

-- Second approch

DELETE FROM Employees 
WHERE employee_id NOT IN (
    SELECT * FROM (
        SELECT MIN(employee_id) FROM Employees 
        GROUP BY employee_name, department_id, salary
    ) AS keep_records
);

-- third approch


create table employee_dup as select distinct * from employee;
delete employee;
insert into employee select * from employee_dup;
delete employee_dup;
select * from employee;
```
### 32.Write sql query to dispalay country name from country table that do not start with vowels and do not end with vowels.Result not contain dublicate.
```sql
 select distinct country_name from country where substr(country_name,1,1) not in ('a','e','i','o','u''A','E','I','O','U')
 and
 substr(country_name-1,1) not in ('a','e','i','o','u''A','E','I','O','U');
 ```
 ### 33.Write an sql query to find the current DateOfJoining
 ```sql
   select now();
   select CURRENT_DATE;
   ```
### 34.write an sql query to fetch all the department_id which are present in either of the tables -employees and departments

--union give me unique data from both table and union all give all data . 
```sql
 select department_id from employee
 UNION
 select department_id from department;
 ```   
### 35.Write sql query to find dublicate rows in a table
```sql
select * , count(empid) from employee GROUP by empid having count(empid)>1;
```
### 36. employee details with the maximum and minimum salary in a single query 
```sql
 select employee_id,employee_name,department_id,department_name ,salary,
 case
  when salary = (select max(salary) from employee) then 'maz salary'
  when salary = (select min(salary) from employee) then 'min salary'
  end as salary_type
  from employee
  where salary = (select max(salary) from employee)
  or salary = (select min(salary) from employee);
  ```
### 36.Assigning Bonus Based on Experience
```sql
  select employee_id,employee_name,years_of_experience,salary,
  case
  when years_of_experience >=10 then salary * 0.20
  when years_of_experience between 5 and 9 then salary * 0.10
  else salary * 0.05
  end as Bonus
  from employee;
  ```
 ### 37.Checking Even or Odd Employee ID
 ```sql
 select employee_id ,employee_name,
 case 
 when employee_id %2==0 then 'Even Id'
 else 'odd Id' 
 end as id_type
 from employee;
 ``` 
### 38. query using if
```sql
SELECT 
    employee_id, 
    employee_name, 
    salary,
    IF(salary > 70000, 'High Salary', 'Low Salary') AS Salary_Status
FROM Employees;
```


