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
