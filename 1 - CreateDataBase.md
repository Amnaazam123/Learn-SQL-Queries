Database is used to create multiple tables which help in storing data. First you create Database, then you create your table, then you define your coloumn names and their data types
. After that you can filter your results applying multiple queries.

## Datatypes in MySQL
- string (CHAR, VARCHAR, BINARY, VARBINARY etc)
- numeric (INT, INTEGER, FLOAT, DECIMAL, DOUBLE, BIGINT, MEDIUMINT, BOOLEAN, BOOL etc)
- Date and Time (DATE(format: YYYY-MONTH-DATE), DATETIME(format: YYYY-MM-DD hh::mm::ss), TIME(format: hh::mm::ss), YEAR)

## Create Database
```
CREATE DATABASE student;
```
After running this command you will see student database in schema tab.

![image](https://user-images.githubusercontent.com/71166016/176666129-2b1dda71-354b-4e3a-8bf2-75e531aeb708.png)
## Choose Database
Before creating table, you must choose database in which you want to create table.
###### Method-1
myDatabase > right click > set as Default Schema

![image](https://user-images.githubusercontent.com/71166016/176669123-935e0a97-ff7b-4f22-9e6b-b5114244f233.png)

###### Method-2
Use following query and run it.
```
USE student;
```
## Create Table
```
CREATE TABLE StudentRecord(
	id INT,                   #coloumnName coloumnDtatype
	name VARCHAR(50),
    birth_date DATE,
    phone VARCHAR(12),
    gender VARCHAR(1)
);

```
![image](https://user-images.githubusercontent.com/71166016/176671677-506a589a-e83b-44a1-9e3c-666faf6ab28c.png)

## View table data in Database 
 Method-1: Click on highlighted button

![image](https://user-images.githubusercontent.com/71166016/176672658-4daa4581-9904-4fa5-bba4-0e15c1cb2670.png)

Method-2: Run following query
```
SELECT * FROM student; 
```
## CREATE Rows in table
Once you create a row or table or database, do not re-run that command.<br> 
If you do not provide any value for any cell, it will put *NULL* there.
```
INSERT INTO studentrecord VALUES (1,"Amna Azam", "2002-04-25", "13250377190","F");
INSERT INTO studentrecord VALUES (2,"Arshia Azam", "2005-08-02", "13250377190","F");
INSERT INTO studentrecord VALUES (3,"Zain Azam", "2007-08-24", "13250377190","M");
```
if you want to create multiple rows in one command in sql:
```
INSERT INTO studentrecord VALUES
 (1,"Amna Azam", "2002-04-25", "13250377190","F"),
 (2,"Arshia Azam", "2005-08-02", "13250377190","F"),
 (3,"Zain Azam", "2007-08-24", "13250377190","M");
```
![image](https://user-images.githubusercontent.com/71166016/176676005-b9d9fd52-02c1-4f06-b09d-f4064fe1cc3a.png)

## Constraints
### NOT NULL, CHECK, UNIQUE, DEFALUT
You apply these constraints while creating tables
- if you want that all entries of one coloumn must be filled/provided, then you will use ***NOT NULL*** constraint.
- if you want that one coloumn must have values fulfilling any condition, then you will use ***CHECK(condition)*** constraint.
- if you want to place all values unique in any coloumn, you will use ***UNIQUE*** constraint.
- if you want to put any default value in any coloumn when user leave any cell empty, you will use ***DEFAULT*** CONSTRAINT.
```
CREATE TABLE test(
 id INT UNIQUE NOT NULL,
 name VARCHAR(50) NOT NULL,
 age INT NOT NULL CHECK(age>=20),
 city VARCHAR(12) NOT NULL DEFAULT ("Okara")
);
```
## Display Table Values
### SELECT
if you want to display any two coloumns named as name and gender, you will run following command:
```
SELECT name,gender
FROM studentrecord;
```
![image](https://user-images.githubusercontent.com/71166016/176688231-163818d2-80d7-4771-b4cf-a334c40d71d4.png)


if you want to display all coloumns, you will run following command:
```
SELECT *
FROM studentrecord;
```

## Alias
### AS
```
SELECT name AS "Student Name", gender AS Gender
FROM studentrecord
```
![image](https://user-images.githubusercontent.com/71166016/176688702-5b5e7e6e-9a22-4af5-aba2-2a7f55f16e57.png)

## Condition
### WHERE 
```
SELECT * FROM studentrecord
WHERE gender="F"
```
```
SELECT * FROM studentrecord
WHERE age >= 20
```
```
SELECT * FROM studentrecord
WHERE city != "Agra"          #WHERE city <> "Agra"
```
## Condition Operators
### AND, OR, NOT
###### AND
```
SELECT id, name FROM studentrecord
WHERE gender = "F" AND age >= 10 AND age <= 20 
```
###### OR
```
SELECT id, name FROM studentrecord
WHERE id = 15 OR id > 10 OR gender = "F" 
```
###### NOT
```
SELECT id, name FROM studentrecord
WHERE NOT gender = "F"               # WHERE gender != "F"
```
## IN operator
It is equvialent to OR operator 
```
SELECT * FROM studentrecord
WHERE id IN(3,4,5)              # WHERE id = 3 OR id = 4 OR id = 5
```
```
SELECT * FROM studentrecord
WHERE id NOT IN(3,4,5)         # All values except 3,4,5
```

## BETWEEN operator
For range purposes
```
SELECT * FROM studentrecord
WHERE id BETWEEN 1 AND 3   
```
```
SELECT * FROM studentrecord
WHERE id NOT BETWEEN 1 AND 3   
```
## LIKE operator
```
SELECT * FROM studentrecord
WHERE name LIKE "A%"         # "%" sign represents zero, one or multiple characters.
```
```
SELECT * FROM studentrecord
WHERE name LIKE "__n%"      # where name has n at third position, there are 2 characters before 'n' and after n there may b 0 or multiple characters.
```

## ORDER BY and DISTINCT property
```
SELECT * FROM studentrecord
ORDER BY name DESC           # By default id it ASC	
```
```
SELECT * FROM studentrecord
ORDER BY name, age DESC      #if name has same order then order the results on the base of age coloumn
```
If you want to print all unique data of ONE COLOUMN(unique entries/unique cells of one coloumn), You will use DISTINCT.
```
SELECT DISTINCT gender FROM studentrecord          # F, M	
```
## IS NULL and IS NOT NULL
```
SELECT name FROM studentrecord
WHERE gender IS NULL              #show record where gender is not provided by student.
```
```
SELECT name FROM studentrecord
WHERE gender IS NOT NULL              #show record where gender is provided by student.
```
## LIMIT
To display number of first rows.
```
SELECT * FROM studentrecord
LIMIT 3                               # Display first 3 rows.
```
```
SELECT * FROM studentrecord
LIMIT 2,8           # display 8 rows from third row (after first 2 rows)
```
## Aggregate Functions
### COUNT
```
SELECT COUNT(name) FROM studentrecord          # how many records/rows you have for name.
SELECT COUNT(*) FROM studentrecord             # Display count of rows
```
### MAX
```
SELECT MAX(salary),name FROM studentrecord          # Display maximum salary with his name
```
### MIN
```
SELECT MIN(salary),name FROM studentrecord          # Display min salary with his name
```
### SUM
```
SELECT SUM(salary) FROM studentrecord          # Display sum of salaries
```
### MAX
```
SELECT AVG(salary) FROM studentrecord          # Display average of salary
```
### UPDATE table
```
UPDATE studentrecord
SET name = "Ahmed", age = 20
WHERE name = "Zain Azam";
```


