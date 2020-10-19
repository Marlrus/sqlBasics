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

# Switch to DS4A Class

This is a course for sql basics by Jimmy Jing. A query is just a way of calling searches. This is just a way to communicate queries to a computer. We will be using the notebook provided by the class. We will be converting the data into tables using pandas **dataframes**. It is important to know the structure of our db. I will be skipping re writing things that I already know. He makes an interesting distinction about WHERE calling it a filter for FROM, where it filters the tables before choosing the columns that where selected. 

## GROUP BY, HAVING, ORDER BY, and LIMIT

This merges the data that has the same values. For example we can have a table with the population of cities in multiple countries and we can unify the data to have a row with the population by country using GROUP BY. 

HAVING is the filter for GROUP BY where you can set conditions for the data.

ORDER BY is how you want the data to be organized, ascending or descending. The default value is ascending.

LIMIT is how many rows the query can return. 

```SQL
SELECT COUNT(INCIDENT_NUMBER), OFFENSE_CODE 
       
FROM crime 
    
WHERE DAY_OF_WEEK = 'Monday' 
    
GROUP BY OFFENSE_CODE_GROUP
    
HAVING COUNT(INCIDENT_NUMBER) > 15
    
ORDER BY COUNT(INCIDENT_NUMBER) DESC
    
LIMIT 10

```
This query will return a table that shows the number of incidents and the offense code they belong to from the crime table. Then it filters the results that are only on mondays, and groups them by offense code only taking the offenses where there are more than 15 occurences and orders them in descending order by the ammount of incidences.

The query I might have to write is:

```SQL
SELECT zona_media, zona_grande

FROM tabla_inmueble_v2
```

Debugging is the main thing you will have to do in a database.

## AS

We can use the AS keyword to change the name that will be shown from a column. Choose a name that is obvious for easier understanding.

## MODIFIERS: SUM, MIN, MAX

We will run the following query:

```SQL
SELECT DISTRICT, SUM(LAT), MIN(LAT), MAX(LAT) 
FROM crime 
GROUP BY DISTRICT
```

This is actually pretty useless information, but here we will sum all the latitudes, find the lowest latitude, and the largest latitude. This will create a table that has columns for the sum, min, and max values. 

### CAST

Casting is when we change the variable type to the type we are casting as:

```SQL
SELECT DISTRICT, CAST(SUM(LAT) AS INT) AS Sum 
FROM crime 
GROUP BY DISTRICT
```

Here we are converting the sum of latitudes into integers and then displaying the column as the name Sum.

## SUBSTR

This statements allows us to get a subset of data. 

```SQL
SELECT SUBSTR(DISTRICT,1,1) AS LETTER_D, YEAR, COUNT(0) AS Count 
FROM crime 
GROUP BY SUBSTR(DISTRICT,1,1), YEAR
```

Here the SUBSTR function takes the column as the first argument, then the character where we want to start and how many characters we want to extract. Here we take the first letter from each district and create a columt labeled LETTER_D and then group the data by the letter that we get, as well as the year, and order them by that letter as a default. It is important to note that SQL **does not start the index from 0, it indexes from 1**.

## JOINS

There are variations of joins that can be expressed as ven diagrams:

Command     | Description | ALIAS
-------- | ----- | -----
JOIN | Returns records that have matching values. | INNER
LEFT JOIN | Returns all records from left table and matching from right. | OUTER
RIGHT JOIN | Returns all records from right table and matching from left. | OUTER
RIGHT JOIN | Returns all records from right table and matching from left. | OUTER
FULL JOIN | Returns all records from both tables and show where they connect. | OUTER

### Creating a Database

We are using a package called **sqlalchemy** to create a new table **offence**. Then we insert records to that table that have a single offence code and a name. Then we will use this new table to do an inner join:

```SQL
SELECT A.* 
FROM crime A INNER JOIN offence B ON A.OFFENSE_CODE = B.OFFENSE_CODE
```
This is a tricky join operation because we are selecting using an alias before we create that alias. So what we say here is that we are selecting all the data from a table which we will call A (all the data because of the *). Then we select crime and change the name to A implicitly, and create an inner JOIN with B which we alias as B and use the OFFENCE_CODE column to find the matching values. It is also notable that we can safely ommit the INNER portion of the query and it would still be the same. We can also replace the * in the query to select specific columns of the table. 

```SQL
SELECT COUNT(*) 
FROM crime A INNER JOIN offence B ON A.OFFENSE_CODE = B.OFFENSE_CODE
```
Here we are getting the number of records that have matching offense codes on both tables.

```SQL
SELECT COUNT(*) 
FROM crime A LEFT JOIN offence B ON A.OFFENSE_CODE = B.OFFENSE_CODE
```
Here we are getting all the data from table A along with information from table B, this means that we get a table that has the same size as table A and no new information because table B has no new data. If we were to add a new column from table B with data that is unique to it, we would see that data wherever the data from table B was used, and null in all values from A in that column because it does not exist. 

This was the end of the SQL basics from the DS4A course. 