---
marp: true
theme: default
class: invert
size: 16:9
paginate: true
footer: 國立陽明交通大學 電子與光子學士學位學程
headingDivider: 1
style: |
  section::after {
    content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
  }
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .middle-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .middle-grid img {
    width: 75%;
  }
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }
  .grid img {
    width: 100%;
  }
  .red-text {
    color: red;
  }
  
  .blue-text {
    color: lightskyblue;  
  }

  .brown-text {
    color: brown;  
  }

  .small-text {
    font-size: 0.70rem;
  }
---
# Chapter8: Advanced SQL
- Learn how to create a table and modify columns and constrains
- Learn how to manipulate the contents of the data, using SQL commands to insert, update, and delete rows of data 
- Learn how to use triggers and stored procedures to perform actions when a specific event occurs.
- Learn how SQL facilitates the application of business procedures when it is embedded in a programming language such as Visual Basic NET, C#, or COBOL.  

# Steps to Develop Database
1. Design ER model (Fig 7.1 or Fig 8.1)
2. Create database 
3. Create database **schema** (a logical group of database objects, like tables and indexes)
4. Insert data

# Design ER model
![bg right:70% w:100%](restricted/CFig08_01.jpg)

# Create Database and Insert Data
![bg right:70% w:80%](restricted/CFig08_02.jpg)

# Create Table Syntax
```sql
CREATE TABLE tablename (
column1 data type [constraint] [,
column2 data type [constraint] ] [,
PRIMARY KEY (column1 [, column2]) ] [,
FOREIGN KEY (column1 [, column2]) REFERENCES tablename] [,
CONSTRAINT constraint ] );
```

# Creating VENDOR Table
```sql
CREATE TABLE VENDOR (
V_CODE 		INTEGER,
V_NAME 		VARCHAR(35) NOT NULL,
V_CONTACT 	VARCHAR(15) NOT NULL,
V_AREACODE 	CHAR(3) NOT NULL,
V_PHONE 	CHAR(8) NOT NULL,
V_STATE 	CHAR(2) NOT NULL,
V_ORDER 	CHAR(1) NOT NULL,
PRIMARY KEY (V_CODE)); 
```

# Creating PRODUCT Table
```sql
CREATE TABLE PRODUCT (
P_CODE 	VARCHAR(10) PRIMARY KEY,
P_DESCRIPT 	VARCHAR(35) NOT NULL,
P_INDATE 	DATETIME NOT NULL,
P_QOH 	        INTEGER NOT NULL,
P_MIN 		INTEGER NOT NULL,
P_PRICE 	NUMERIC(8,2) NOT NULL,
P_DISCOUNT 	NUMERIC(4,2) NOT NULL,
V_CODE 		INTEGER,
CONSTRAINT PRODUCT_V_CODE_FK FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE));
```

# The Order of Related Table Creation
- Because the PRODUCT table contains a foreign key that references the VENDOR table, create the VENDOR table first
- “M” side of a relationship always references
the “1” side. Therefore, in a 1:M relationship, you must always create the table for the “1” side first.

# Set SQL Constraints when Table Creating
- <span class="blue-text">PRIMARY KEY </span>constraint : not null and unique
- <span class="blue-text">FOREIGN KEY </span>constraint
  <span class="small-text">
  - You cannot delete a vendor from the VENDOR table if at least one product row references that vendor
  - *CONSTRAINT PRODUCT_V_CODE_FK FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE) ON UPDATE CASCADE*
  - If you make a change in any VENDOR’s V_CODE that change is automatically applied to PRODUCT to maintain referential integrity
  </span>
- <span class="blue-text">NOT NULL</span> constraint
- <span class="blue-text">UNIQUE</span> constraint
- <span class="blue-text">DEFAULT</span> constraint
- <span class="blue-text">CHECK constraint</span>: validate data when an attribute value is entered
  <span class="small-text">
  - CUS_AREACODE CHAR(3) DEFAULT '615' NOT NULL CHECK(CUS_AREACODE IN ('615', '713', '931'))

# Create Table INVOICE, LINE to Illustrate Constrains 
```sql
CREATE TABLE INVOICE (
INV_NUMBER NUMBER PRIMARY KEY,
CUS_CODE NUMBER NOT NULL REFERENCES CUSTOMER(CUS_CODE),
INV_DATE DATE DEFAULT NOW() NOT NULL,
CONSTRAINT INV_CK1 CHECK (INV_DATE > ('2022-01-01'));

CREATE TABLE LINE (
INV_NUMBER 	INTEGER NOT NULL,
LINE_NUMBER	NUMERIC(2,0) NOT NULL,
P_CODE		VARCHAR(10) NOT NULL,
LINE_UNITS	NUMERIC(9,2) DEFAULT 0.00 NOT NULL,
LINE_PRICE	NUMERIC(9,2) DEFAULT 0.00 NOT NULL,
PRIMARY KEY (INV_NUMBER,LINE_NUMBER),
FOREIGN KEY (INV_NUMBER) REFERENCES INVOICE (INV_NUMBER) ON DELETE CASCADE,
FOREIGN KEY (P_CODE) REFERENCES PRODUCT(P_CODE),
CONSTRAINT LINE_UI1 UNIQUE(INV_NUMBER, P_CODE));
```

# Create a Table with a SELECT Statement
- SQL provides a way to rapidly create a new table based on selected columns and rows of an existing table using a subquery
- All of the data rows returned by the SELECT statement are copied automatically
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT;
```

# SQL Index
- Indexes can be used to improve the efficiency of searches
and to avoid duplicate column values
```sql
CREATE INDEX P_INDATEX ON PRODUCT(P_INDATE);
CREATE UNIQUE INDEX P_CODEX ON PRODUCT(P_CODE);
CREATE INDEX PROD_PRICEX ON PRODUCT(P_PRICE DESC);
DROP INDEX PROD_PRICEX;
```

# Altering Table Structures
- All changes in the table structure are made by using the ALTER TABLE command with three options: ADD, MODIFY, and DROP
- Changing a column’s data type
- Changing a column’s data characteristics
- Adding a column
- Adding primary key, foreign key, and check constraints
- Dropping a column
- Deleting a table from the database

# Changing a Column’s Data Type
```sql
ALTER TABLE PRODUCT
    MODIFY V_CODE CHAR(5);

-- if V_CODE is not a FOREIGN KEY.
-- f V_CODE contains data that cannot be converted, the query will fail.
-- Ensure no data truncation occurs.
```
# Changing a Column’s Data Characteristics
```sql
ALTER TABLE PRODUCT
MODIFY (P_PRICE DECIMAL(9,2));
```
- Some DBMSs impose limitations on when it is possible to change data type or data characteristics.
  - Increase (but not decrease) the size of a column only
  - Attribute changes can be made only when there is no data in the attribute.

# Adding a Column
```sql
ALTER TABLE PRODUCT
    ADD (P_SALECODE CHAR(1));
```
- Do not add NOT NULL as constrain

# Adding Primary Key, Foreign Key, and Check Constraints
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT;

ALTER TABLE PART
    ADD PRIMARY KEY (PART_CODE);

ALTER TABLE PART
    ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE);

ALTER TABLE PART
    ADD CHECK (PART_ PRICE > = 0);

ALTER TABLE PART
    ADD PRIMARY KEY (PART_CODE),
    ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE),    
    ADD CHECK (PART_ PRICE > = 0);
```

# Dropping a Column
```sql
ALTER TABLE VENDOR
    DROP COLUMN V_ORDER;
```

# Dropping a Table
```sql
DROP TABLE PART;
```

# Data Manipulation Commands (INSERT)
```sql
INSERT INTO tablename VALUES (value1, value2, …, valuen)

INSERT INTO VENDOR
    VALUES (21225,'Bryson, Inc.','Smithson','615','223-3234','TN','Y');
INSERT INTO VENDOR
    VALUES (21226,'Superloo, Inc.','Flushing','904','215-8995','FL','N');

SELECT * FROM VENDOR

INSERT INTO PRODUCT
    VALUES ('BRT-345','Titanium drill bit','18-Oct-15', 75, 10, 4.50, 0.06, NULL);

INSERT INTO PRODUCT(P_CODE, P_DESCRIPT) 
    VALUES ('BRT-345','Titaniumdrill bit');    
```

# Inserting Table Rows with a SELECT Subquery
```sql
CREATE TABLE PART (
  PART_CODE CHAR(8),
  PART_DESCRIPT CHAR(35),
  PART_ PRICE DECIMAL(8,2),
  V_CODE INTEGER,
  PRIMARY KEY (PART_CODE));

INSERT INTO PART (PART_CODE, PART_DESCRIPT, PART_PRICE, V_CODE)
  SELECT P_CODE, P_DESCRIPT, P_PRICE, V_CODE
  FROM PRODUCT;
```

# Saving Table Changes
- Any changes made to the table contents are not saved on disk until you (1)close database (2)close the program you are using (3) use the COMMIT command
- The COMMIT command permanently saves all changes—such as rows added, attributes modified, and rows deleted made to any table in the database.
- The COMMIT command’s purpose is not just to save changes. The ultimate purpose of the COMMIT and ROLLBACK commands is to ensure database update integrity in transaction management.
- By default, MySQL also automatically commits changes with each command. However, if START TRANSACTION or BEGIN is placed at the beginning of a series of commands, MySQL will delay committing the commands until the COMMIT or ROLLBACK command is issued.

# Updating Table Rows
```sql
UPDATE PRODUCT
SET P_INDATE = '2022-01-18'
WHERE P_CODE = '13-Q2/P2';

UPDATE PRODUCT
SET P_INDATE = '2022-01-18', P_PRICE = 17.99, P_MIN = 10
WHERE P_CODE = '13-Q2/P2';

UPDATE PRODUCT
SET P_SALECODE = '1'
WHERE P_CODE IN ('2232/QWE', '2232/QTY');

UPDATE PRODUCT
SET P_PRICE = P_PRICE * 1.10
WHERE P_PRICE < 50.00
```

# Deleting Table Rows
```sql
DELETE FROM PRODUCT
WHERE P_CODE = 'BRT-345';
```

# Restoring Table Contents
The ROLLBACK command is used to restore the database table contents to the condition that existed after the last COMMIT statements.

# Virtual Tables: Creating a View
- A view is a virtual table based on a SELECT query that is saved as an object in the database
- A base table is the table on which a view is based
```sql
CREATE VIEW PROD_STATS AS
SELECT V_CODE, 
       SUM(P_QOH*P_PRICE) AS TOTCOST, 
       MAX(P_QOH) AS MAXQTY, 
       MIN(P_QOH) AS MINQTY, 
       AVG(P_QOH) AS AVGQTY
FROM PRODUCT
GROUP BY V_CODE;

SELECT * 
FROM PROD_STATS
```

# Auto Increment in MySQL
- In MySQL, you may set one and only one column with the AUTO_INCREMENT property. If you set one, the column must be defined as the primary key of the table

```sql
-- In MySQL
create table arena (
    arena_id          int  primary key auto_increment,
    arena_name        varchar(100),
    location          varchar(100),
    seating_capacity  int);

-- Loading the data without having to manage arena_id column
insert into arena (arena_name, location, seating_capacity)
values ('Madison Square Garden', 'New York', 20000);
insert into arena (arena_name, location, seating_capacity)
values ('Dean Smith Center', 'North Carolina', null);

select * from arena;
```

# Sequences in Oracle
- In Oracle, a sequence is an object for generating unique segment values for a column

```sql
-- In Oracle
CREATE SEQUENCE CUS_CODE_SEQ START WITH 20010 NO CACHE;

INSERT INTO CUSTOMER
VALUES (CUS_CODE_SEQ.NEXTVAL, 'Connery', 'Sean', NULL, '615', '898-2007', 0.00);
```

# Procedural SQL
- Procedural SQL is an extension of SQL that adds procedural programming capabilities, such as variables and logical flow control, to SQL and is designed to run inside the database
- The procedural code is executed as a unit by the DBMS when it is invoked by the end user
- End users can use procedural SQL to create the following:
  - Stored procedures
  - Triggers

# Stored Procedures
- A stored procedure is a named collection of procedural and SQL statements
  - They are stored in the database
  - A major advantage of stored procedures is that they can be used to encapsulate and represent business transactions
- Using stored procedures offers the following advantages:
  - Stored procedures substantially reduce network traffic and increase performance
  - Stored procedures help reduce code duplication by means of code isolation and code sharing 

# Table Population for Store Procedure
```sql
create database population;
use population;
create table state_population
	(state       varchar(100),
   population  int);
insert into state_population values ('New York',	19299981);
insert into state_population values ('Texas',			29730311);
insert into state_population values ('California',39613493);
insert into state_population values ('Florida', 	21944577);
insert into state_population values ('New Jersey', 9267130);
insert into state_population values ('Massachusetts' 6893000);
insert into state_population values ('Rhode Island', 1097379);
```

# Use Store Procedure

```sql
use population;
drop function if exists f_get_state_population;
delimiter //
create function f_get_state_population (
  state_param    varchar(100)
)
returns int
deterministic reads sql data
begin
  declare population_var int;

  select  population
  into    population_var
  from    state_population
  where   state = state_param;

  return(population_var);

end//

delimiter ;

-- Call the f_get_state_population() function
select f_get_state_population('New York');

-- Call the f_get_state_population() function from a WHERE clause
select  *
from    state_population
where   population > f_get_state_population('New York');

```

