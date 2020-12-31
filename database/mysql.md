## SQL

## Overview
- ecosystem
  - MySql
  - PSql
- entities
  - table: table
  - row: records
  - column: fields
- features
  - strong schema
   - fields has to be normalized
  - data distributed across multiple tables
  - connected through relations
- scaling
  - horitontal: difficult / impossible
  - vertical: possible
- pros
  - predictable
- cons
  - frequent read of complex relation is slow

## installation
- run mysql docker container
  - docker run --name mysql -e MYSQL_ROOT_PASSWORD=921021 -d -p 3306:3306 -v mysql_data:/var/lib/mysql/data mysql:5.7

- run psql docker container
  - docker run --name postgres -e POSTGRES_PASSWORD=921021 -d -p 5432:5432 -v postgres_data:/var/lib/postgresql/data postgres

## SQL syntax
- SELECT, FROM, and WHERE
- join (aka inner join)
- left join (aka left outer join)
- right join (aka right outer join)
- full join (aka full outer join)
- cross join

## questions
- What are indexes and how do they work?
- Model me a “many to many” relationship.
- What is the difference between = NULL and IS NULL?
- What’s a prepared statement and why do we use them?





Login to your MYSQL console.
USE <name_of_your_database>;
SOURCE <path_of_your_.sql_file>


//login to mysql
mysql -u root -p

//set user password
ALTER USER 'root'@'localhost' IDENTIFIED BY '921021';

//list existing databases
show databases;

//create new database
create database huoshui;

//add user to database
CREATE USER 'admin'@'localhost';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';

//show all users
SELECT User FROM mysql.user;



## joins
- `inner join` (aka `join`)
	- get only the overlapped rows
- `left join` (aka `left outer join`)
	- keep the left table rows even if there is no match
- `right join` (aka `right outer join`)
	-	keep the right table rows even if there is no match
- `full join`
	- mysql can only emulate this through `UNION ALL` a left join & right join

## group
- reduce rows through `GROUP BY`

## aggregate
- reduce values through `aggregate function`

## subqueries
- can be used as multiple things
	- value
	```sql
	SELECT COUNT(name) FROM products
	```
	- rows
	```sql
	FROM (SELECT * FROM products) AS p1
	JOIN (SELECT * FROM prodcts) AS p2 on p1.id=p2.id
	```
	- column
	```sql
	where p1.id IN (SELECT id FROM products);
	```
- rules
	- in SELECT: must be a scalar value
	- in FROM: 
		- can by anything, but must be compatible with outer environement
		- must use alias
	- in JOIN: must be compatible with ON
	- in WHERE: must be compatible with comparison operator
