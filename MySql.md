# MySql

- [MySql](#mysql)
  - [Initial Commands](#initial-commands)
  - [Database Commands](#database-commands)
  - [Table Initial Commands](#table-initial-commands)
  - [Creating tables:](#creating-tables)
  - [Inserting in Tables:](#inserting-in-tables)
  - [Filtering Commands](#filtering-commands)
    - [ORDER BY](#order-by)
    - [LIKE](#LIKE)
  - [Insert UNIQUE DATA in tables (PRIMARY KEY & UNIQUE)](#insert-unique-data-in-tables-primary-key--unique)
  - [Updating & Deleting](#updating--deleting)
  - [String Functions](#string-functions)
    - [CONCAT](#concat)
    - [SUBSTRING](#substring)
    - [REPLACE](#replace)
    - [REVERSE](#reverse)
    - [CHAR_LENGTH](#char-length)
    - [UPPER & LOWER](#upper---lower)
    - [DISTINCT](#distinct)
  - [Aggregate Functions](#aggregate-functions)
    - [Count](#count)
    - [Group By](#group-by)
    - [Min & Max](#min--max)
    - [Using Min & Max along with Group By](#using-min--max-along-with-group-by)
    - [SUM](#sum)
    - [AVG](#avg)
  - [WORKING WITH DATES AND TIME](#working-with-dates-and-time)
    - [Create Table of DATES](#create-table-of-dates)
    - [Format_Date](#format-date)
    - [DATE_DIFF & DATE_ADD](#date_diff--date_add)
    - [TIME-INTERVAL, DATE_DIFF & DATE_ADD](#time-interval--date_diff--date_add)
    - [Create TIME-STAMP Table](#create-time-stamp-table)
  - [CASE STATEMENTS & IF STATEMENTS](#case-statements--if-statements)
  - [DATA RELATIONSHIPS](#data-relationships)
    - [Creating relational table](#creating-relational-table)
    - [Inner Joint](#inner-joint)
    - [Left Join](#left-join)
    - [RIGHT Join](#right-join)
    - [Join MANY TO MANY (3 tables)](#join-many-to-many--3-tables)
  - [TRIGGERS](#triggers)
    - [Managing TRIGGERS](#managing-triggers)
  - [MySQL-NODE](#MySQL-NODE)

## Initial Commands

| Command          | Description                   |
| ---------------- | ----------------------------- |
| `SHOW WARNINGS;` | Show all the warnings present |

## Database Commands

| Command                            | Description                              |
| ---------------------------------- | ---------------------------------------- |
| `SHOW DATABASES;`                  | Show all the databases present in Server |
| `CREATE DATABASE <database_name>;` | Create a new DataBase                    |
| `USE <database_name>;`             | Use that DataBase                        |
| `SELECT DATABASE();`               | Show DataBase currently in use           |
| `DROP DATABASE <database_name>;`   | Delete a DataBase                        |

## Table Initial Commands

| Command                           | Description                              |
| --------------------------------- | ---------------------------------------- |
| `SHOW TABLES;`                    | Show all the tables present in Databases |
| `SHOW COLUMNS FROM <table_name>;` | Show all the columns & Properties        |
| `DESC <table_name>;`              | Show all the columns & Properties        |
| `DROP TABLE <table_name>;`        | Delte a Table                            |

## Creating tables:

```
CREATE TABLE <table_name> (
    name_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL DEFAULT 'Dummy',
    age INT,
    gender VARCHAR(6),
    PRIMARY KEY (name_id)
    etc...
);
```

## Inserting in Tables:

```
INSERT INTO <table_name> (c1, c2 , ....)
VALUES (V11, V12, ....),
       (V21, V22, ....),
       (V31, V32, ....);
```

## Filtering Commands

| Command                                              | Description                                            |
| ---------------------------------------------------- | ------------------------------------------------------ |
| `SELECT IFNULL(<column_name>, 0) FROM <table_name>;` | Show 0 if column have value NULL                       |
| `SELECT <column_name> FROM <table_name>;`            | Show the specified column                              |
| `SELECT <column_name> AS <abc> FROM <table_name>;`   | Using Alias abc                                        |
| `WHERE <any condition> ;`                            | Where is used to Filter data                           |
| `HAVING <any condition> ;`                           | Used Just like as WHERE , used after GROUP BY          |
| `LIKE <any condition> ;`                             | LIKE is used after WHERE to ultra Filter data          |
| `ORDER BY <column_name> ;`                           | ORDER BY is used to sort data in ascending order       |
| `ORDER BY <column_name> DESC ;`                      | ORDER BY DESC is used to sort data in descending order |
| `LIMIT <strt_num>, <prsnt_num> ;`                    | Present only limited data ,[Start data , end data]     |

### ORDER BY

<!-- Combine CONCAT & SUBSTRING & REPLACE -->

order by column_name

```
SELECT column_name FROM <table_name> ORDER BY column_name;
```

Order in descending order

```
SELECT column_name FROM <table_name> ORDER BY column_name DESC;
```

Order in ascending order (its the default oreder even if you dont mention it will do ascending order)

```
SELECT column_name FROM <table_name> ORDER BY column_name ASC;
```

Order by column_name-2

```
SELECT column_name-1,column_name-2,column_name-3
FROM <tableName> ORDER BY 2;
```

Order by column_name-1 , if same column_name-1 data then order by column_name-2

```
SELECT column_name-1,column_name-2,column_name-3
FROM <tableName> ORDER BY column_name-1,column_name-2;
```

### LIKE

<br>
( USING "%" WILDCARD )<br>
->using a string length

Filter in column_name-1 with words who has da between them :-

```
SELECT column_name-1,column_name-2 FROM <tableName> WHERE column_name-1 LIKE '%da%';
```

Filter in column_name-1 with words who starts with da :-

```
SELECT column_name-1,column_name-2 FROM <tableName> WHERE column_name-1 LIKE 'da%';
```

Filter in column_name-1 with words who ends with da :

```
SELECT column_name-1,column_name-2 FROM <tableName> WHERE column_name-1 LIKE '%da';
```

Filter in column_name-1 with words who are exactly equal to "the":-

```
SELECT column_name-1,column_name-2 FROM <tableName> WHERE column_name-1 LIKE 'the';
```

( USING "\_" WILDCARD )<br>
-> one underscore means one char length,specifc exact char length

Filter in column_name-1 with exact char length as there are underscore :-

```
SELECT column_name-1,column_name-2 FROM <tableName> WHERE condition/string LIKE '____';
```

### EXTRAS

Used when we want to search % or \_ wildcards in the strings , we do it by using backslash

```
SELECT title FROM books WHERE title LIKE '%\%%'

SELECT title FROM books WHERE title LIKE '%\_%'
```

## Insert UNIQUE DATA in tables (PRIMARY KEY & UNIQUE)

<br>

PRIMARY KEY : It is a column or combination of column that uniquely identifies a row in a table.
Given below example of combination (user_id, photo_id) which cannot be duplicated .

```
CREATE TABLE <table_name> (
    user_id INTEGER NOT NULL,
    photo_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(user_id) REFERENCES users(id) ON DELETE CASCADE ON UPDATE CASCADE,
    FOREIGN KEY(photo_id) REFERENCES photos(id) ON DELETE CASCADE ON UPDATE CASCADE,
    PRIMARY KEY(user_id, photo_id)
);
```

UNIQUE : This keyword is used to uniquely set a data .

```
CREATE TABLE users (
    id INTEGER AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);
```

---

## Updating & Deleting

```
///---- Updating Data ----////
UPDATE <table_name>
SET <column_name> ='Anything'
WHERE <condition>;

////---- Delete Data ----////
DELETE FROM <table_name>
WHERE <condition>
```

---

## String Functions

| Command       | Description                           |
| ------------- | ------------------------------------- |
| `CONCAT`      | Used to join two or more              |
| `SUBSTRING`   | Used as SPLICE in JS                  |
| `REPLACE`     | Replaces certain characters in String |
| `REVERSE`     | Reverse a String                      |
| `CHAR_LENGTH` | Show the specified column             |
| `UPPER`       | Show the specified column             |
| `LOWER`       | Show the specified column             |
| `DISTINCT`    | Show the specified column             |

### CONCAT

Used to join two or more

```
SELECT
CONCAT (<column-1> , ' ' , <column-2 , .....>)
FROM <table_name>
WHERE <condition>
```

### SUBSTRING

Used as SPLICE in JS

```
SELECT SUBSTRING(
    <column_name>, strt_num, end_num;
) FROM <table_name>
```

### REPLACE

Replaces certain characters in String

```
SELECT
    REPLACE(<column_name> , 'e', 3)
    FROM <table_name>
```

### REVERSE

Reverse a String

```
SELECT
    REVERSE(<column_name>)
    FROM <table_name>
```

### CHAR_LENGTH

Gives num of characters in a String

```
SELECT
    CHAR_LENGTH(<column_name>)
    FROM <table_name>
```

### UPPER & LOWER

Converts to UpperCase Or LowerCase

```
SELECT
    UPPER(<column_name>)
    FROM <table_name>

SELECT
    LOWER(<column_name>)
    FROM <table_name>
```

### DISTINCT

Remove Duplicates

```
SELECT
    DISTINCT(<column_name>)
    FROM <table_name>
```

Combine CONCAT & SUBSTRING & REPLACE

```
SELECT
    CONCAT(
        SUBSTRING(column_name, strt_num, end_num),
        '...'
    ) AS '<Any alias_name>'
FROM books;
```

## Aggregate Functions

| Command     | Description                                |
| ----------- | ------------------------------------------ |
| `COUNT`     | Gives no. of items present in table        |
| `GROUP BY`  | Summarizes identical data into single rows |
| `MIN & MAX` | Find minimum or maximum among a list       |
| `SUM`       | Used to sum a whole column                 |
| `AVG`       | Used to AVG a whole column                 |

### Count

Gives the no. of rows present in table

```
SELECT COUNT(*)FROM <table_name>
```

Gives the no. of \<required_item> present in table

```
SELECT
COUNT(
    <column_name>
)FROM <table_name>
```

### Group By

Summarizes identical data into single rows, here count implies on the grouped rows. It will first group them with column_name-1 then if identical it will group by column_name-2

```
SELECT
<column_name-1>, <column_name-2>, COUNT(*)
FROM books
GROUP BY <column_name-1>, <column_name-2>;
```

### Min & Max

Find minimum or maximum among a list

```
SELECT MIN(<column_name>)
FROM <table_name>
```

### Using Min & Max along with Group By

Table containing first book release of every author

```
SELECT author_fname,
       author_lname,
       Min(released_year)
FROM   books
GROUP  BY author_lname,
          author_fname;
```

### SUM

Used to sum a whole column

```
SELECT SUM(<column_name>)
FROM <table_name>;
```

### AVG

Used to AVG a whole column

```
SELECT AVG(<column_name>)
FROM <table_name>;
```

---

## WORKING WITH DATES AND TIME

### Date and Time Functions();

- for viewing current date

```
Select CURDATE();
```

- for viewing current time

```
Select CURTIME();
```

- for viewing current date-time

```
Select NOW();
```

### Create Table of DATES

- Date and time datatypes

DATE - for dates ( yy:mm:dd )<br>
TIME - for time ( hh:mm:ss)<br>
DATETIME - for date_time ( yy:mm:dd - hh:mm:ss)<br>

```
CREATE TABLE people (name VARCHAR(100),
birthdate DATE,
birthtime TIME,
birthdt DATETIME);
```

### Format_Date

- Used for various date and time realted functions like,dayOfTheWeek,DayName,WeekdayName..etc

```
SELECT DATE_FORMAT(<column_date-time>, '%m/%d/%Y at %h:%i')
FROM <table_name>;
```

### DATE_DIFF & DATE_ADD

```
SELECT
DATEDIFF(NOW(), birthdate)
FROM people;
```

```
SELECT
DATE_ADD(birthdt, INTERVAL 10 year)
FROM people;
```

### TIME-INTERVAL , DATE_DIFF & DATE_ADD

```
SELECT NOW()+INTERVAL 1 MONTH  FROM people;
SELECT NOW()-INTERVAL 1 MONTH  FROM people;
```

### Create TIME-STAMP Table

Time-stamp wont work properly with too old years like that of before 1970. It same as date_time but this one uses less space(like 4 bytes instead of 8 bytes)

```
CREATE TABLE comments (
    content VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW() ON UPDATE NOW()
);
```

---

## CASE STATEMENTS & IF STATEMENTS

CASE works as IF ELSE

```
SELECT title, stock_quantity,
    CASE
        WHEN stock_quantity <= 50 THEN '*'
        WHEN stock_quantity <= 100 THEN '**'
        ELSE '***'
    END AS 'Stock'
FROM books;
```

Using IF

```
SELECT title, stock_quantity,
    IF stock < 10 , 'Out of stock', 'Available' AS status
```

---

## DATA RELATIONSHIPS

### Creating relational table

```
CREATE TABLE <table_name>(
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY(customer_id) REFERENCES customers(id)
);
```

### Inner Joint

```
SELECT * FROM <table_1>
    JOIN <table_2>
    ON <condition>
```

### Left Join

```
SELECT * FROM <table_1>
    LEFT JOIN <table_2>
    ON <condition>
```

### RIGHT Join

```
SELECT * FROM <table_1>
    RIGHT JOIN <table_2>
    ON <condition>
```

### Join MANY TO MANY (3 tables)

```
SELECT
    title,
    rating,
    CONCAT(first_name,' ', last_name) AS reviewer
FROM reviewers
INNER JOIN reviews
    ON reviewers.id = reviews.reviewer_id
INNER JOIN series
    ON series.id = reviews.series_id
ORDER BY title;
```

---

## TRIGGERS

These are rules which can be set for a table, that take place after or just before an event . Which can also give an error message set by us.

Given below , an example of a trigger that gives error message when age entered is less than 18.

NEW -  refers to the data to be inserted

DELIMITER $$ - let us use multiple ";" to "$$"

```
DELIMITER $$
CREATE TRIGGER must_be_adult
	BEFORE INSERT ON users FOR EACH ROW
    BEGIN
		IF NEW.age < 18
        THEN
			SIGNAL SQLSTATE '45000'
				SET MESSAGE_TEXT = 'Must be an adult';
		END IF;
	END;
$$
DELIMITER ;
```

Given below , Trigger code that stops self-following on social media.

```
DELIMITER $$
CREATE TRIGGER prevent_self_follows
	INSERT BEFORE ON follows FOR EACH ROW
		BEGIN
			IF NEW.follower.id = NEW.followee_id
            THEN
				SIGNAL SQLSTATE '45000'
                SET MESSAGE_TEXT = 'You cannot follow yourself!';
			END IF;
        END;
$$
DELIMITER
```

Given below , Trigger code that entrys data when someone unfollows someone. This also uses another syntax to insert data in a table.

```
DELIMITER $$
CREATE TRIGGER capture_unfollow
	AFTER DELETE ON follows FOR EACH ROW
		BEGIN
			INSERT INTO unfollows
            SET follower_id = OLD.follower_id,
				followee_id = OLD.followee_id;
        END;
$$;
DELIMITER
```

### Managing TRIGGERS

| Command                       | Description                |
| ----------------------------- | -------------------------- |
| `SHOW TRIGGERS`               | Show and list all triggers |
| `DROP TRIGGER <trigger_name>` | Delete a trigger           |

# MySQL-NODE

WE can use faker library of node to install fake data

more info @ https://github.com/mysqljs/mysql

```
npm i faker
```

Step 1 : Install the MySQL Node Package

```
npm i mysql
```

Step 2 : Connect to Database\*

```

var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',     // your root username
  database : 'join_us'   // the name of your db
});
```

Step 3 : Run Queries

```
var q = 'SELECT CURTIME() as time, CURDATE() as date, NOW() as now';
connection.query(q, function (error, results, fields) {
  if (error) throw error;
  console.log(results[0].time);
  console.log(results[0].date);
  console.log(results[0].now);
});
```

Step 4 : Inserting Data Using Node

- Approach #1 (HARD_CODED)

```
var q = 'INSERT INTO users (email) VALUES ("rusty_the_dog@gmail.com")';

connection.query(q, function (error, results, fields) {
  if (error) throw error;
  console.log(results);
});
```

- Approach #2 (DYNAMIC VERSION)

```
var person = {
    email: faker.internet.email(),
    created_at: faker.date.past()
};

var end_result = connection.query('INSERT INTO users SET ?', person, function(err, result) {
  if (err) throw err;
  console.log(result);
});

console.log(end_result.sql) # this to view sql in the node
```

Step 5 : BULK INSERT

```
var data = [];
for(var i = 0; i < 500; i++){
    data.push([
        faker.internet.email(),
        faker.date.past()
    ]);
}


var q = 'INSERT INTO users (email, created_at) VALUES ?';

connection.query(q, [data], function(err, result) {
  console.log(err);
  console.log(result);
});

connection.end();
```

- FINAL QUERY

```
var mysql = require('mysql');
var faker = require('faker');


var connection = mysql.createConnection({
 host     : 'localhost',
 user     : 'root',
 database : 'join_us'
});


var data = [];
for(var i = 0; i < 500; i++){
   data.push([
       faker.internet.email(),
       faker.date.past()
   ]);
}


var q = 'INSERT INTO users (email, created_at) VALUES ?';

connection.query(q, [data], function(err, result) {
 console.log(err);
 console.log(result);
});

connection.end();
```

## EXPRESS SERVER STARTER

Remember to start the server up using - node FileName.js

The res.send() entity should be a string
```
var express = require('express');

var app = express();

app.get("/", function(req, res){
 res.send("HELLO FROM OUR WEB APP!");
});

app.listen(8080, function () {
 console.log('App listening on port 8080!');
});
```
