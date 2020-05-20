#MYSQL

+------------------+--------------+
|  ADMIN_ID        |  INT(10)     |    
+------------------+---------------+

`mysql -u root -p`

from external
`mysql -h xxx.xxx.xxx.xxx -u root -p`

each page will have own user on mysql database. This user will have passqord and some privileges on database related to that page

##Databases
`show databases;`
`CREATE DATABASE dbname;`
`USE dbname;`

#Tables
`SHOW TABLES;`
`CREATE TABLE tablename (name VARCHAR(20), owner VARCHAR(20),species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);`
`DESCRIBE tablename`; to show table structure
`INSERT INTO tablename VALUES ('Puffball', 'Diane', 'hamster', 'f', '199-03-30', NULL);`

#Retrieving Information from a Table
`SELECT what_to_select FROM which_table WHERE conditions_to_satisfy;`
`SELECT * FROM tablename WHERE name='Bowser';`
`SELECT * FROM tablename WHERE birth >= '1998-1-1';`
`SELECT * FROM tablename WHERE name='Bowser' AND sex='f';`
`SELECT owner FROM pet`
`SELECT name, species, birth FROM pet WhERE species='dog' OR species='cat'`
`SELECT name, birth FROM pet ORDER BY birth DESC;`

##Types
INT
TINYINT
SMALLINT
MEDIUMINT
BIGINT
FLOAT(M,D)
M - length
D - number of decimal
DOUBLE(M,D)
DECIMAL(M,D)

DATE
DATETIME
TIMESTAMP
TIME
YEAR(M)

CHAR(M)
VARCHAR(M)
BLOB or TEXT
TINYBLOB or TINYTEXT  MEDIUM... LONG...
ENUM - list, for example ENUM('B', 'C', 'D') and only that values or NULL could ever populate field
