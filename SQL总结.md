# SQL W3Schools Review

### Preword:

I have been used SQL since 2015 ever since I acted as an entry-level specialist. At that time, SQL was most often used together with Oracle system to get teh most up-to-dated sales data. Later on in my master, SQL was instructed in several courses such as Business Intelligence and Data programming.

Here I would like to review the basic SQL knowlwdge in a scientific and structured way quickly.

---

### Tutorial:

[https://www.w3schools.com/sql/default.asp](https://www.w3schools.com/sql/default.asp)

---

### SQL Notes:

- Structured Query Language to access and manipulate databases.
- RDBMS is the basis for SQL
- table, field (column), record (row)
- not case sensitive
- Semicolon to separate statememts
- Aliases (could reaname both column and table name) 

**Note:** It requires double quotation marks or square brackets if the alias name contains spaces ```SELECT CustomerName AS Customer, ContactName AS [Contact Person] FROM Customers;``` 

Or we could  **create an alias named "Address" that combine four columns** (Address, PostalCode, City and Country): ```SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address FROM Customers;``` or in MySQL     Join 2 tables:```SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address FROM Customers;``` Join 3 tables: ```SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName FROM ((Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID) INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);```

- **Join**

  - **(INNER) JOIN**: Returns records that have matching values in both tables
  - **LEFT (OUTER) JOIN**: Return all records from the left table, and the matched records from the right table
  - **RIGHT (OUTER) JOIN**: Return all records from the right table, and the matched records from the left table
  - **FULL (OUTER) JOIN**: Return all records when there is a match in either left or right table
  - **SELF JOIN** The following SQL statement matches customers that are from the same city: ```SELECT A.CustomerName AS CustomerName1, B.CustomerName ASCustomerName2, A.City FROM Customers A, Customers B WHERE A.CustomerID <> B.CustomerID AND A.City = B.City  ORDER BY A.City;```

- **UNION** used to combine the result-set of two or more SELECT statements; 

  The **UNION** operator selects only distinct values by default. To allow duplicate values, use **UNION ALL**. ```SELECT *column_name(s)* FROM *table1* UNION SELECT *column_name(s)* FROM *table2*;```

  selects all the different German cities (only distinct values) from "Customers" and "Suppliers":  

  `SELECT City, Country FROM Customers WHERE Country='Germany' UNION SELECT City, Country FROM Suppliers WHERE Country='Germany' ORDER BY City; Try it Yourself `

- **GROUP BY** The GROUP BY statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns.

  SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country ORDER BY COUNT(CustomerID) DESC;` SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country ORDER BY COUNT(CustomerID) DESC;`

- **HAVING **The HAVING clause was added to SQL because the ***WHERE keyword could not be used with [aggregate functions](https://baike.baidu.com/item/%E8%81%9A%E9%9B%86%E5%87%BD%E6%95%B0)***. Count sum avg max and min; solutions: [SQL中关于where后面不能放聚合函数（如sum等）的解决办法](https://blog.csdn.net/z479403374/article/details/51781639) where 子句的作用是在对查询结果进行分组前，将不符合where条件的行去掉，即在分组之前过滤数据，条件中不能包含聚组函数，使用where条件显示特定的行。having 子句的作用是筛选满足条件的组，即在分组之后过滤数据，条件中经常包含聚组函数，使用having 条件显示特定的组，也可以使用多个分组标准进行分组。

  lists the number of customers in each country, sorted high to low (Only include countries with more than 5 customers):

  `SELECT COUNT(CustomerID), Country FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5 ORDER BY COUNT(CustomerID) DESC;`

  `SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID WHERE LastName = 'Davolio' OR LastName = 'Fuller' GROUP BY LastName HAVING COUNT(Orders.OrderID) > 25;`

- **EXIST**T he EXISTS operator is used to test for the existence of any record in a subquery.

  The EXISTS operator returns true if the subquery returns one or more records.

   Please returns TRUE and lists the suppliers with a product price less than 20:

  `SELECT SupplierName FROM Suppliers WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price < 20);`

- **ANY AL**

  The ANY and ALL operators are used with a WHERE or HAVING clause.

  The ANY operator returns true if any of the subquery values meet the condition.

  The ALL operator returns true if all of the subquery values meet the condition.

  **Note:** The *operator* must be a standard comparison operator (=, <>, !=, >, >=, <, or <=).

  `SELECT ProductName FROM Products WHERE ProductID = ALL (SELECT ProductID FROM OrderDetails WHEREQuantity = 10);`

##### Some of The Most Important SQL Commands

- **SELECT** - extracts column(s) from a database; **Distinct, WHERE, ORDER BY, TOP, LIMIT, ROWNUM; **

  (MySQL supports the LIMIT clause to select a limited number of records, while Oracle uses ROWNUM)

  **Functions:  MIN() and MAX(); COUNT(), AVG(), SUM()**

  ``` English
  SELECT Distinct column1, column2 FROM table WHERE condition ORDER BY column1 ASC, column2 DESC;
  SELECT COUNT(DISTINCT Country)as CountA FROM Customers ORDER BY CountA ASC|DESC;
  ```

  ```SELECT MIN(Price) AS SmallestPrice FROM Products;```

  ** Server / MS Access Syntax:**

  > SELECT **TOP *number*|*percent*** *column_name(s)* FROM *table_name* WHERE *condition*;

  **MySQL Syntax:**

  > SELECT *column_name(s)* FROM *table_name* WHERE *condition* **LIMIT** *number*;

  **Oracle Syntax:**

  > SELECT *column_name(s)* FROM *table_name* **WHERE ROWNUM <= *number***

- **SELECT INTO**  The SELECT INTO statement copies data from one table into a new table.

  `SELECT * INTO *newtable* [IN *externaldb*] FROM *oldtable*WHERE *condition*;`

- **INSERT INTO SELECT ** The INSERT INTO SELECT statement copies data from one table and inserts it into another table. `INSERT INTO Customers (CustomerName, City, Country) SELECT SupplierName, City, Country FROM Suppliers`

- **SQL IFNULL(), ISNULL(), COALESCE(), and NVL() Functions** Mysql uses 

  `SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0)) FROM Products`

- **Comments** Single line comments start with —. Multi-line comments start with /* and end with */.

- **Operators could be used in WHERE** consitions

  | Operator              | Description                                                  |
  | --------------------- | ------------------------------------------------------------ |
  | =                     | Equal                                                        |
  | <>                    | Not equal. **Note:** In some versions of SQL this operator may be written as != |
  | >                     | Greater than                                                 |
  | <                     | Less than                                                    |
  | >=                    | Greater than or equal                                        |
  | <=                    | Less than or equal                                           |
  | (not) BETWEEN         | Between an inclusive range **BETWEEN AND** 1. Numbers``` SELECT * FROM Products WHERE (Price BETWEEN 10 AND 20) AND NOT CategoryID IN (1,2,3);``` 2. Text ``` SELECT * FROM Products WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni' ORDER BY ProductName;```; 3. date ``` SELECT * FROM Orders WHERE OrderDate BETWEEN #07/04/1996# AND #07/09/1996#;``` |
  | LIKE                  | Search for a pattern    wildcards 1. **%** The percent sign represents zero, one, or **multiple characters**    2.  **_ **The underscore represents **a single character**  (MS Access uses a question mark (?) instead of the underscore(_) 3. **[charlist] Wildcard and [!charlist] Wildcard **            ```WHERE CustomerName LIKE 'a%' / '%a' /  '%or%' /  '_r%' /  'a_%_%' /  'a%o' ```WHERE City LIKE '[!bsp]%' ```( select all customers with a City NOT starting with "b", "s", or "p":) |
  | IN                    | To specify multiple possible values for a column ``` SELECT * FROM Customers WHERE Country IN (SELECT Country FROM Suppliers);``` |
  | And                   |                                                              |
  | Or                    |                                                              |
  | Not                   | **AND, OR and NOT could be combined**       ```SELECT * FROM Customers WHERE Country='Germany' AND (City='Berlin' OR City='München');``` ```SELECT * FROM Customers WHERE NOT Country='Germany' AND NOT Country='USA';``` |
  | IS NULL / IS NOT NULL | A field with a NULL value is a field with no value. ( A field with a NULL value is one that has been left blank during record creation!)  It is not possible to test for NULL values with comparison operators, such as =, <, or <>. ``` WHERE Address IS NOT NULL;``` |

- **UPDATE** - updates data in a database **UPDATE SET (WHERE)   **

  ```UPDATE Customers SET ContactName = 'Alfred Schmidt', City= 'Frankfurt' WHERE CustomerID = 1;```

- **DELETE** - deletes data from a database

   ```DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';```

  It is possible to delete all rows in a table without deleting the table. This means that the table structure, attributes, and indexes will be intact: ```DELETE FROM table_name;```or: ```DELETE * FROM table_name;```

- **INSERT INTO** - inserts new data into a database

   ```INSERT INTO *table_name* (*column1*, *column2*, *column3*, ...) VALUES (*value1*, *value2*, *value3*, …);```(insert into all or selected columns) ```INSERT INTO *table_name* VALUES (*value1*, *value2*, *value3*, …);```(insert into all columns)

- **CREATE DATABASE** - creates a new database

- **ALTER DATABASE** - modifies a database

- **CREATE TABLE** - creates a new table

- **ALTER TABLE** - modifies a table

- **DROP TABLE** - deletes a table

- **CREATE INDEX** - creates an index (search key)

- **DROP INDEX** - deletes an index

- 

---

### SQL Database Tutorial

- CREATE DATABASE *databasename*;

- DROP DATABASE *databasename*;

- >CREATE TABLE Persons (     
  >
  >​          PersonID int,     
  >
  >​          LastName varchar(255),     
  >
  >​          FirstName varchar(255),     
  >
  >​          Address varchar(255),     City varchar(255)  
  >
  >);

- Create Table Using Another Table

- > CREATE TABLE *new_table_name* AS     
  >
  > ​            SELECT *column1, column2,...*     
  >
  > ​            FROM *existing_table_name*     
  >
  > ​            WHERE ....;

- DROP TABLE Shippers;

- TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself.

- > TRUNCATE TABLE *table_name*;

- > ALTER TABLE *table_name* ADD *column_name datatype*;
  >
  > ALTER TABLE *table_name* DROP COLUMN *column_name*;
  >
  > ALTER TABLE *table_name* MODIFY COLUMN *column_name datatype*;

- **SQL Create Constraints**

> CREATE TABLE *table_name* (     
>
> ​        *column1 datatype* *constraint*,     
>
> ​       *column2 datatype* *constraint*,     
>
> ​       *column3 datatype* *constraint*,     .... 
>
> );

- The following constraints are commonly used in SQL:

  + **NOT NULL** - Ensures that a column cannot have a NULL value

  > CREATE TABLE Persons (     
  >
  > ID int NOT NULL,     
  >
  > LastName varchar(255) NOT NULL,     
  >
  > FirstName varchar(255) NOT NULL,     
  >
  > Age int 
  >
  > );

  + **UNIQUE** - Ensures that all values in a column are different

  + > CREATE TABLE Persons (     
    >
    > ID int NOT NULL UNIQUE,     
    >
    > LastName varchar(255) NOT NULL,     
    >
    > FirstName varchar(255),     
    >
    > Age int 
    >
    > );

  + **PRIMARY KEY** - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table

  + > CREATE TABLE Persons (     ID int NOT NULL,     LastName varchar(255) NOT NULL,     FirstName varchar(255),     Age int,     PRIMARY KEY (ID) );

  + **FOREIGN KEY** - Uniquely identifies a row/record in another table; A FOREIGN KEY is a key used to link two tables together.

    A FOREIGN KEY is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

    The table containing the foreign key is called the **child table**, and the table containing the candidate key is called **the referenced or parent table**.

  + **CHECK** - Ensures that all values in a column satisfies a specific condition

  + **DEFAULT** - Sets a default value for a column when no value is specified

  + **INDEX** - Used to create and retrieve data from the database very quickly

  + **AUTO INCREMENT **

  + **Date Data Types** Mysql:

    - DATE - format YYYY-MM-DD
    - DATETIME - format: YYYY-MM-DD HH:MI:SS
    - TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
    - YEAR - format YYYY or YY















---

### References:

#### 1. Quick Refernece：

| SQL Statement   | SyntaxSyntax                                                 |
| --------------- | ------------------------------------------------------------ |
| AND / OR        | SELECT column_name(s) FROM table_name WHERE condition AND\|OR condition |
| ALTER TABLE     | ALTER TABLE table_name  ADD column_name datatypeorALTER TABLE table_name  DROP COLUMN column_name |
| AS (alias)      | SELECT column_name AS column_alias FROM table_nameorSELECT column_name FROM table_name  AS table_alias |
| BETWEEN         | SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2 |
| CREATE DATABASE | CREATE DATABASE database_name                                |
| CREATE TABLE    | CREATE TABLE table_name ( column_name1 data_type, column_name2 data_type, column_name3 data_type, ... ) |
| CREATE INDEX    | CREATE INDEX index_name ON table_name (column_name)orCREATE UNIQUE INDEX index_name ON table_name (column_name) |
| CREATE VIEW     | CREATE VIEW view_name AS SELECT column_name(s) FROM table_name WHERE condition |
| DELETE          | DELETE FROM table_name WHERE some_column=some_valueorDELETE FROM table_name  (**Note:** Deletes the entire table!!)DELETE * FROM table_name  (**Note:** Deletes the entire table!!) |
| DROP DATABASE   | DROP DATABASE database_name                                  |
| DROP INDEX      | DROP INDEX table_name.index_name (SQL Server) DROP INDEX index_name ON table_name (MS Access) DROP INDEX index_name (DB2/Oracle) ALTER TABLE table_name DROP INDEX index_name (MySQL) |
| DROP TABLE      | DROP TABLE table_name                                        |
| EXISTS          | IF EXISTS (SELECT * FROM table_name WHERE id = ?) BEGIN --do what needs to be done if exists END ELSE BEGIN --do what needs to be done if not END |
| GROUP BY        | SELECT column_name, aggregate_function(column_name) FROM table_name WHERE column_name operator value GROUP BY column_name |
| HAVING          | SELECT column_name, aggregate_function(column_name) FROM table_name WHERE column_name operator value GROUP BY column_name HAVING aggregate_function(column_name) operator value |
| IN              | SELECT column_name(s) FROM table_name WHERE column_name IN (value1,value2,..) |
| INSERT INTO     | INSERT INTO table_name VALUES (value1, value2, value3,....)*or*INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,....) |
| INNER JOIN      | SELECT column_name(s) FROM table_name1 INNER JOIN table_name2  ON table_name1.column_name=table_name2.column_name |
| LEFT JOIN       | SELECT column_name(s) FROM table_name1 LEFT JOIN table_name2  ON table_name1.column_name=table_name2.column_name |
| RIGHT JOIN      | SELECT column_name(s) FROM table_name1 RIGHT JOIN table_name2  ON table_name1.column_name=table_name2.column_name |
| FULL JOIN       | SELECT column_name(s) FROM table_name1 FULL JOIN table_name2  ON table_name1.column_name=table_name2.column_name |
| LIKE            | SELECT column_name(s) FROM table_name WHERE column_name LIKE pattern |
| ORDER BY        | SELECT column_name(s) FROM table_name ORDER BY column_name [ASC\|DESC] |
| SELECT          | SELECT column_name(s) FROM table_name                        |
| SELECT *        | SELECT * FROM table_name                                     |
| SELECT DISTINCT | SELECT DISTINCT column_name(s) FROM table_name               |
| SELECT INTO     | SELECT * INTO new_table_name [IN externaldatabase] FROM old_table_name*or*SELECT column_name(s) INTO new_table_name [IN externaldatabase] FROM old_table_name |
| SELECT TOP      | SELECT TOP number\|percent column_name(s) FROM table_name    |
| TRUNCATE TABLE  | TRUNCATE TABLE table_name                                    |
| UNION           | SELECT column_name(s) FROM table_name1 UNION SELECT column_name(s) FROM table_name2 |
| UNION ALL       | SELECT column_name(s) FROM table_name1 UNION ALL SELECT column_name(s) FROM table_name2 |
| UPDATE          | UPDATE table_name SET column1=value, column2=value,... WHERE some_column=some_value |
| WHERE           | SELECT column_name(s) FROM table_name WHERE column_name operator value |

#### 2. SQL Data Types

**Note:** Data types might have different names in different database. Differnet data types guide how SQL will interact with the stored data.  And even if the name is the same, the size and other details may be different! Always check the documentation!

Try to find differnet definitions  for various kinds of datatbase such as MySQL, SQLServcer and MS Access

[https://www.w3schools.com/sql/sql_datatypes.asp](https://www.w3schools.com/sql/sql_datatypes.asp)

**For My SQL:**

| Text Data type   | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| CHAR(size)       | Holds a fixed length string (can contain letters, numbers, and special characters). The fixed size is specified in parenthesis. Can store up to 255 characters |
| VARCHAR(size)    | Holds a variable length string (can contain letters, numbers, and special characters). The maximum size is specified in parenthesis. Can store up to 255 characters. **Note:** If you put a greater value than 255 it will be converted to a TEXT type |
| TINYTEXT         | Holds a string with a maximum length of 255 characters       |
| TEXT             | Holds a string with a maximum length of 65,535 characters    |
| BLOB             | For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data |
| MEDIUMTEXT       | Holds a string with a maximum length of 16,777,215 characters |
| MEDIUMBLOB       | For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data |
| LONGTEXT         | Holds a string with a maximum length of 4,294,967,295 characters |
| LONGBLOB         | For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of data |
| ENUM(x,y,z,etc.) | Let you enter a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted.**Note:** The values are sorted in the order you enter them.You enter the possible values in this format: ENUM('X','Y','Z') |
| SET              | Similar to ENUM except that SET may contain up to 64 list items and can store more than one choice |

| Number Data type | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| TINYINT(size)    | -128 to 127 normal. 0 to 255 UNSIGNED*. The maximum number of digits may be specified in parenthesis |
| SMALLINT(size)   | -32768 to 32767 normal. 0 to 65535 UNSIGNED*. The maximum number of digits may be specified in parenthesis |
| MEDIUMINT(size)  | -8388608 to 8388607 normal. 0 to 16777215 UNSIGNED*. The maximum number of digits may be specified in parenthesis |
| INT(size)        | -2147483648 to 2147483647 normal. 0 to 4294967295 UNSIGNED*. The maximum number of digits may be specified in parenthesis |
| BIGINT(size)     | -9223372036854775808 to 9223372036854775807 normal. 0 to 18446744073709551615 UNSIGNED*. The maximum number of digits may be specified in parenthesis |
| FLOAT(size,d)    | A small number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter |
| DOUBLE(size,d)   | A large number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter |
| DECIMAL(size,d)  | A DOUBLE stored as a string , allowing for a fixed decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter |

---

### SQL QUIZ

Points: 24 out of 25

**1. What does SQL stand for?****You answered:**Structured Query Language Correct Answer!**

2. Which SQL statement is used to extract data from a database?You answered:**SELECT Correct Answer!**
3. Which SQL statement is used to update data in a database?You answered:**UPDATE Correct Answer!**
4. Which SQL statement is used to delete data from a database?You answered:**DELETE Correct Answer!**
5. Which SQL statement is used to insert new data in a database?You answered:**INSERT INTO Correct Answer!**
6. With SQL, how do you select a column named "FirstName" from a table named "Persons"?You answered:**SELECT FirstName FROM Persons Correct Answer!**
7. With SQL, how do you select all the columns from a table named "Persons"?You answered:**SELECT * FROM Persons Correct Answer!**
8. With SQL, how do you select all the records from a table named "Persons" where the value of the column "FirstName" is "Peter"?You answered:**SELECT * FROM Persons WHERE FirstName='Peter' Correct Answer!**
9. With SQL, how do you select all the records from a table named "Persons" where the value of the column "FirstName" starts with an "a"?You answered:**SELECT * FROM Persons WHERE FirstName LIKE 'a%' Correct Answer!**
10. The OR operator displays a record if ANY conditions listed are true. The AND operator displays a record if ALL of the conditions listed are trueYou answered:**True Correct Answer!**
11. With SQL, how do you select all the records from a table named "Persons" where the "FirstName" is "Peter" and the "LastName" is "Jackson"?You answered:**SELECT * FROM Persons WHERE FirstName='Peter' AND LastName='Jackson' Correct Answer!**
12. With SQL, how do you select all the records from a table named "Persons" where the "LastName" is alphabetically between (and including) "Hansen" and "Pettersen"?You answered:**SELECT * FROM Persons WHERE LastName BETWEEN 'Hansen' AND 'Pettersen' Correct Answer!**
13. Which SQL statement is used to return only different values?You answered:**SELECT DISTINCT Correct Answer!**
14. Which SQL keyword is used to sort the result-set?You answered:**ORDER BY Correct Answer!**
15. With SQL, how can you return all the records from a table named "Persons" sorted descending by "FirstName"?You answered:**SELECT * FROM Persons SORT BY 'FirstName' DESC Wrong Answer!**
16. With SQL, how can you insert a new record into the "Persons" table?You answered:**INSERT INTO Persons VALUES ('Jimmy', 'Jackson') Correct Answer!**
17. With SQL, how can you insert "Olsen" as the "LastName" in the "Persons" table?You answered:**INSERT INTO Persons (LastName) VALUES ('Olsen') Correct Answer!**
18. How can you change "Hansen" into "Nilsen" in the "LastName" column in the Persons table?You answered:**UPDATE Persons SET LastName='Nilsen' WHERE LastName='Hansen' Correct Answer!**
19. With SQL, how can you delete the records where the "FirstName" is "Peter" in the Persons Table?You answered:**DELETE FROM Persons WHERE FirstName = 'Peter' Correct Answer!**
20. With SQL, how can you return the number of records in the "Persons" table?You answered:**SELECT COUNT(*) FROM Persons Correct Answer!**
21. What is the most common type of join?You answered:**INNER JOIN Correct Answer!**
22. Which operator is used to select values within a range?You answered:**BETWEEN Correct Answer!**
23. The NOT NULL constraint enforces a column to not accept null values.You answered:**True Correct Answer!**
24. Which operator is used to search for a specified pattern in a column?You answered:**LIKE Correct Answer!**
25. Which SQL statement is used to create a table in a database?You answered:**CREATE TABLE Correct Answer!