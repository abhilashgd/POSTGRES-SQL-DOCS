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

57. DELETE * FROM person;
58. SELECT * FROM person WHERE id=2;
59. UPDATE person SET email ='parke@teshmail.com' WHERE id =2;
60. SELECT * FROM person WHERE id=2;
61. UPDATE person SET first_name ='Laacie', last_name ='Montana', email ='laacieMontana@testmail.com' WHERE id=2;
62. SELECT * FROM person WHERE id=2;
63.  INSERT INTO person (
64. first_name,
65. last_name,
66. gender,
67. date_of_birth, email)
68. VALUES('Jake', 'Jones', 'MALE', DATE '1990-01-01','jake@gmail.com') 
69. ON CONFLICT(id) DO NOTHING;
70.  INSERT INTO person (
71. first_name,
72. last_name,
73. gender,
74. date_of_birth, email)
75. VALUES('Jake', 'Jones', 'MALE', DATE '1990-01-01','jake@gmail.com') 
76. ON CONFLICT(id) DO UPDATE SET email = EXCLUDED.email;
77. //foreign key is a column that references primary key in another table
78. docker cp person-car.sql 48007cff6b6e:/usr/src
79. \i /usr/src/person-car.sql
80. \d person
81. SELECT * FROM person;
82. SELECT * FROM car;
83. UPDATE person SET car_id=2 WHERE id=1;
84. UPDATE person SET car_id=1 WHERE id=2;
85. SELECT * FROM person;
86. //INNER joins
87.  SELECT * FROM person
88. JOIN car ON person.car_id=car.id;
89. \x //expanded display on
    1.  SELECT * FROM person
    2. JOIN car ON person.car_id=car.id;
    3.  SELECT person.first_name, car.make,car.model,car.price
    4.  FROM person
    5. JOIN car ON person.car_id=car.id;
90. \x // to turn off expanded display
91. //LEFT JOIN
    1. SELECT * FROM person
    2. LEFT JOIN car ON person.car_id=car.id;
92. SELECT * FROM person WHERE car_id is NULL;
93. insert into car (id, make, model, price) values (13, 'Mazda', 'RX-8', '51272.48');
94. SELECT * FROM car;
95. insert into person (first_name, last_name, email, gender, date_of_birth, country_of_birth) values ('Bryna', 'Bruckman', 'bbruckman0@live.com', 'Female', '2021/08/27', 'Jamaica');
96. UPDATE person SET car_id=13 WHERE id=4;
97. SELECT * FROM person WHERE id=4;
98. SELECT * FROM car where id=13;
99. SELECT * FROM person
    1.  LEFT JOIN car ON car.id=person.car_id;
100. \copy (SELECT * FROM person LEFT JOIN car ON car.id=person.car_id) TO '/usr/src/results.csv' DELIMITER ',' CSV HEADER;
results.csv

![Screen Shot 2022-01-09 at 1 09 54 PM](https://user-images.githubusercontent.com/21958756/148674160-79fc9d76-fbf1-41b7-a5ec-0c98162ba8f6.png)




102. #docker cp 48007cff6b6e:/usr/src/results.csv .  //to copy from docker container to local
103. SELECT nextval('person_id_seq'::regclass);
104.  insert into person (first_name, last_name, gender, email, date_of_birth, country_of_birth) values ('John', 'SEcond', 'Male', 'johnSecond@feedburner.com', '1965-02-28', 'England');
105. select * FROM person;
106. SELECT * FROM person_id_seq;
107. ALTER SEQUENCE person_id_seq RESTART WITH 15;
108. SELECT * FROM person_id_seq;
109. //POSTGRES EXTENSIONS
    1.  SELECT * FROM pg_available_extensions;
109. //UUID
110. https://en.wikipedia.org/wiki/Universally_unique_identifier
111. CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
    1.  SELECT * FROM pg_available_extensions;
    2.  \df
    3. SELECT uuid_generate_v4();
     4. \i /usr/src/person-car-2.sql
112. select * from person;
113. select * from car;
114. //person-car-2.sql has UUID implementation
115.  UPADTE person SET car_uid='63208e76-e793-499d-87dd-7250b30405ee' WHERE person_uid = 'b41f06e4-bd1a-47bc-b0f8-81d559759411';
116. UPDATE person SET car_uid='9539bba6-5f63-4dcb-95ab-f1845b5761b2' WHERE person_uid = 'e83ed9b7-7f91-4d95-a6e1-ac681d6c699e';
117. select * from person                                                                     JOIN car ON person.car_uid = car.car_uid;
118. SELECT * FROM person
119. JOIN car USING (car_uid);
    1. SELECT * FROM person
    2. LEFT JOIN car USING (car_uid);
120.  SELECT * FROM person
    1. LEFT JOIN car USING (car_uid)
    2. WHERE car.* IS NULL;







