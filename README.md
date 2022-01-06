# POSTGRES-SQL-DOCS

Database SQL Commands

DB: postgres:
postgres running on docker

1. % docker exec -it 48007cff6b6e /bin/bash
2. # sql -h localhost -p 5432 -U abhilashgd test //to connect to database test other way is \c test
3. https://www.postgresql.org/docs/9.5/datatype.html
4. //Creating a table named person 
    1. test=# CREATE TABLE person(
    2. test(# id INT,
    3. test(# first_name VARCHAR(50),
    4. test(# last_name VARCHAR(50),
    5. test(# gender VARCHAR(7),
    6. test(# date_of_birth DATE);
CREATE TABLE
5. \d //lists all tables
6. \d person //list details of person table
7. DROP TABLE person; //to delete person table
8. //creating table with constraints
test=# CREATE TABLE person (
id BIGSERIAL  NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
email VARCHAR(150));
CREATE TABLE
9. //inserting data into table
test=# INSERT INTO person (
test(# first_name,
test(# last_name,
test(# gender,
test(# date_of_birth)
test-# VALUES('Anne', 'Smith', 'FEMALE', DATE '1988-01-09');
INSERT 0 1
10.//inserting another row
 INSERT INTO person (
first_name,
last_name,
gender,
date_of_birth, email)
VALUES('Jake', 'Jones', 'MALE', DATE '1990-01-01','jake@gmail.com');
INSERT 0 1
11. test=# select * from person;
12. test=# select from person;
13. test=# select first_name from person;
14. test=# select first_name, last_name from person;
15. generate 1000 data using - https://www.mockaroo.com/
16. \?
17.  Downloads git:(master) ✗ docker cp person.sql 48007cff6b6e:/usr/src //to copy file from local to docker container path /usr/src
18. \i /usr/src/person.sql //to run sql file
19. //ORDER BY COMMANDS
    1. SELECT * FROM person ORDER BY country_of_birth; // to sort by country type
    2. SELECT * FROM person ORDER BY id DESC; // sort by id descending order
    3.  SELECT * FROM person ORDER BY first_name  ASC;
    4. SELECT * FROM person ORDER BY id, email; // sorting with two column constraints
    5. SELECT * FROM person ORDER BY date_of_birth desc;
20. SELECT country_of_birth FROM person;
21. SELECT country_of_birth FROM person ORDER BY country_of_birth;
22. SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth; // Distinct to remove duplicates from the query
23. //WHERE COMMANDS
    1. SELECT * FROM person WHERE gender ='Female';
    2. SELECT * FROM person WHERE gender ='Male' AND country_of_birth='Poland';
    3. SELECT * FROM person WHERE gender ='Male' AND country_of_birth='Poland' OR country_of_birth='United States';
    4. SELECT * FROM person WHERE gender ='Male' AND country_of_birth='Poland' OR country_of_birth='China' AND last_name ='Oven';
24. //COMPARISON OPERATORS
    1. test=# SELECT 1=1;
    2.  ?column?
    3. ----------
    4.  t
    5. (1 row)
    6. 
    7. test=# SELECT 1=2;
    8.  ?column?
    9. ----------
    10.  f
    11. (1 row)
    12. test=# SELECT 1<2;
    13.  ?column?
    14. ----------
    15.  t
    16. (1 row)
    17. 
    18. test=# SELECT 1<1;
    19.  ?column?
    20. ----------
    21.  f
    22. (1 row)
    23. test=# SELECT 1<>2;
    24.  ?column?
    25. ----------
    26.  t
    27. (1 row)
    28. test=# SELECT 'abhilashgd'<>'ABHILASHGD';
    29.  ?column?
    30. ----------
    31.  t
    32. (1 row)
    33. 
    34. test=# SELECT 'ABHILASHGD'<>'ABHILASHGD';
    35.  ?column?
    36. ----------
    37.  f
    38. (1 row)
25. //LIMIT OFFSET and FETCH
    1. SELECT * FROM person LIMIT 5;
    2. SELECT * FROM person OFFSET 5 LIMIT 5;
    3. SELECT * FROM person OFFSET 5 FETCH FIRST 5 ROW ONLY;
    4. SELECT * FROM person WHERE country_of_birth ='China' OR country_of_birth='France' OR country_of_birth='Brazil';
    5.  SELECT * FROM person WHERE country_of_birth IN ('China', 'Brazil', 'Mexico', 'Portugal', 'Nigeria');
    6. SELECT * FROM person WHERE country_of_birth IN ('China', 'Brazil', 'Mexico', 'Portugal', 'Nigeria') ORDER BY country_of_birth;
26. //BETWEEN KEYWORD
    1. SELECT * FROM person
    2. WHERE date_of_birth
    3. BETWEEN DATE '2021-01-01' AND '2021-05-01'
27. //LIKE COMMAND
    1. SELECT * FROM person WHERE email LIKE '%@symantec.com';
    2. SELECT * FROM person WHERE email LIKE '%@symantec.%';
    3. SELECT * FROM person WHERE email LIKE '%@baidu.%';
    4. SELECT * FROM person WHERE email LIKE '_______@%';
    5.  SELECT * FROM person WHERE email LIKE '___a__@%';
    6. SELECT * FROM person WHERE country_of_birth LIKE 'P%'; //to fetch countries starting with P
    7. SELECT * FROM person WHERE country_of_birth ILIKE ‘p%’; // to fetch countries starting with p ignore case


