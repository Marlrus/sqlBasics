# Learning SQL Basics

SQL is a standard language for storing, manipulating, and retrieving data in databases. There are variations of SQL, but they all support the major commands. **RDBMS** stands for *relational database management system* and it stores data in tables, which are collections of related data entries in colums and rows.

```SQL
SELECT * FROM Customers;
```

This is one of the most basic commands and it will select all the fields from customers. Tables are broken down into **fields**, which are the columns of the table, and **records**, which are the rows of the table.

## SQL Syntax

SQL is not case sensitive, however the standard practice is to CAPITALIZE. Some databases require a semicolon after each statement.

Command     | Action
-------- | -----
SELECT | Extracts data from db
UPDATE | Updates data in db
DELETE | Deletes data from db
INSERT INTO | Inserts new data into a db
CREATE DATABASE | Creates a new db
ALTER DATABASE | Modifies a db
CREATE TABLE | Creates a new table
ALTER TABLE | Modifies a table
DROP TABLE | Deletes a table
CREATE INDEX | Creates an index
DROP INDEX | Deletes an index

### SELECT

SELECT is used to extract data from a db. We can select by Fields or the entirety of the dataset:

```SQL
SELECT field1, field2 FROM table_name;

SELECT * FROM table_name;
```

### SELECT DISTINCT

This statement will only return values that are different, this will omit duplicate values from a field:

```SQL
SELECT DISTINCT Country FROM Customers;

SELECT COUNT(DISTINCT Country) FROM Customers;
```

Here we use **COUNT** to get the number of records from our statements. It these queries we will get a table with all the **unique** country records and the number of unique country records from our table.

## WHERE

This statement is used to extract only records that fulfill a specified condition:

```SQL
SELECT field1, field2 FROM table_name WHERE condition;
```

The condition we specify can have operators and does not need quotes for numeric values.

```SQL
SELECT * FROM Custmoers WHERE CustomerID=1;

SELECT * FROM Custmoers WHERE Country='Mexico';
```

This first query will get a table with all the customers where the CustomerID is one. The second query will get a table with all the customers that have the Country field set to Mexico. 

### List of Operators

Operator     | Description
-------- | -----
= | Equal
\> | Greater than
\< | Less Than
\>= | Greater than or Equal
\<= | Less Than or equal
\<\> | Not Equal
BETWEEN | Between a certain range
LIKE | Search for a pattern
IN | Specify multiple possible values for a column
