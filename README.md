# POSTGRES-SQL-DOCS

Database SQL Commands

DB: postgres:
postgres running on docker

1. % docker exec -it 48007cff6b6e /bin/bash
2. sql -h localhost -p 5432 -U abhilashgd test //to connect to database test other way is \c test

# TO generate 1000 data using - https://www.mockaroo.com/
4. # REFERENCE: https://www.postgresql.org/docs/9.5/datatype.html
5. to open sql files, use visual code or sublime text or pgadmin
6. //Creating a table named person 
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
    7. test=# SELECT 1=2;
    12. test=# SELECT 1<2;
    18. test=# SELECT 1<1;
    23. test=# SELECT 1<>2;
    28. test=# SELECT 'abhilashgd'<>'ABHILASHGD';
    34. test=# SELECT 'ABHILASHGD'<>'ABHILASHGD';
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
28. //GROUPING BY KEYWORD
    1. SELECT country_of_birth, COUNT(*)  FROM person GROUP BY country_of_birth; // to count number of person in each country;
    2. SELECT country_of_birth, COUNT(*)  FROM person GROUP BY country_of_birth ORDER BY country_of_birth;// displays in order
29. //HAVING KEYWORD
    1. SELECT country_of_birth, COUNT(*)  FROM person GROUP BY country_of_birth HAVING COUNT(*) >10 ORDER BY country_of_birth;
    2. SELECT country_of_birth, COUNT(*)  FROM person GROUP BY country_of_birth HAVING COUNT(*) >37 ORDER BY country_of_birth;
30. // CREATE a NEW TABLE
    1. create from mockaroo and copy to docker
    2. docker cp car.sql 48007cff6b6e:/usr/src
    3. \i /usr/src/car.sql
31. //MAX, MIN, AVG and SUM
    1.  SELECT MAX(price) FROM car;
    2. SELECT MIN(price) FROM car;
    3. SELECT AVG(price) FROM car;
    4. SELECT ROUND(AVG(price)) FROM car;
    5. SELECT make, model, MIN(price) FROM car GROUP BY make, model;
    6. SELECT make, model, MAX(price) FROM car GROUP BY make, model;
    7. SELECT make,  MAX(price) FROM car GROUP BY make;
    8. SELECT SUM(price) FROM car;
    9. SELECT make, SUM(price) FROM car GROUP BY make;
32. //ARITHAMETIC OPERATOR
    1. SELECT 10+2;
    2. SELECT 10 * 2+8;
    3. SELECT 10 /2;
    4. SELECT 10^3;
    5. SELECT 10 % 3;
33. SELECT id, make, model, price, price*.10  FROM car;
34.  SELECT id, make, model, price, ROUND(price*.10,2)  FROM car;
35. SELECT id, make, model, price, ROUND(price*.10,2),ROUND(price -(price *.10),2)  FROM car;
36. //ALiases
    1.  SELECT id, make, model, price AS original_price, ROUND(price*.10,2) AS ten_percent,ROUND(price -(price *.10),2) AS discount_after_10_percent  FROM car;
37. /COALESCE
    1. select COALESCE(1);
    2. select COALESCE(1) AS number;
    3. select COALESCE(null, null, 1) AS number;
    4. SELECT COALESCE (email,'email not provided')  FROM person;
38. SELECT NULLIF(10,10);
39. SELECT NULLIF(10,1);
40. SELECT COALESCE(10/ NULLIF(0,0),0); //handling divide by zero
41. //TIMESTAMPS and DATE
    1. SELECT NOW();
    2. SELECT NOW()::DATE;
    3. SELECT NOW()::TIME;
42. SELECT NOW()-INTERVAL'1 YEAR';
43.  SELECT NOW()-INTERVAL'10 YEARS’;
44. SELECT NOW()-INTERVAL'10 MONTHS';
45. SELECT NOW()-INTERVAL'10 DAYS’;
46. SELECT NOW()+INTERVAL'10 MONTHS’;//etcetera
47. SELECT (NOW() + INTERVAL '10 MONTHS')::DATE;
48. SELECT EXTRACT(YEAR FROM now());
49. SELECT EXTRACT(DOW FROM now());
50. SELECT EXTRACT(CENTURY FROM now());
51. //AGE FUNCTION
    1. SELECT first_name,last_name, gender, country_of_birth,date_of_birth, AGE(NOW(),date_of_birth) AS age FROM person;
  52. //PRIMARY KEY
    1. insert into person (id, first_name, last_name, email, gender, date_of_birth, country_of_birth) values (1,'Bryna', 'Bruckman', 'bbruckman0@live.com', 'Female', '2021/08/27', 'Jamaica');
    2. ERROR:  duplicate key value violates unique constraint "person_pkey"
    3. DETAIL:  Key (id)=(1) already exists.
    4. ALTER TABLE person DROP CONSTRAINT person_pkey; //duplicates can be added if we drop constraint
    5. select * from person WHERE id= 1;
    6. ALTER TABLE person ADD PRIMARY KEY (id);
    7. DELETE FROM person WHERE id=1;
    8. ALTER TABLE person ADD PRIMARY KEY (id);
53. //ADDING UNIQUE CONSTRAINT
54. ALTER TABLE person ADD CONSTRAINT unique_email_address UNIQUE (email);
56. ALTER TABLE person ADD CONSTRAINT gender_constraint CHECK(gender='Female'OR gender='Male');
57. DELETE FROM person WHERE gender ='Agender';

                                        Table "public.person"
      Column      |          Type          | Collation | Nullable |
 Default
------------------+------------------------+-----------+----------+-------------
-----------------------
 id               | bigint                 |           | not null | nextval('per
son_id_seq'::regclass)
 first_name       | character varying(50)  |           | not null |
 last_name        | character varying(50)  |           | not null |
 email            | character varying(150) |           |          |
 gender           | character varying(7)   |           | not null |
 date_of_birth    | date                   |           | not null |
 country_of_birth | character varying(50)  |           |          |
Indexes:
    "person_pkey" PRIMARY KEY, btree (id)
    "unique_email_address" UNIQUE CONSTRAINT, btree (email)
Check constraints:
    "gender_constraint" CHECK (gender::text = 'Female'::text OR gender::text = '
Male'::text)







