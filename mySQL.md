#MYSQL
+-------------------------------------+
|                STROM                |
+------------------+------------------+
|  ID_STROM        |   INT(10)        |    unsigned NOT NULL AUTO_INCREMENT
+------------------+------------------+
|  TYP_OBJ
|  
|  IDEXT                                  ID z externího zdroje
+------------------+--------------+
|  DATIN           |  DATETIME    |     datum vkladu
+------------------+--------------+
|  DATSC           |  DATETIME    |     datum schválení
+------------------+--------------+
|  DATAK           |  DATETIME    |     datum poslední aktualizace
+------------------+--------------+
|  DATVY           |  DATETIME    |     datum vyřazení
+------------------+--------------+
+------------------+--------------+
|  VLAST               ENUM('RVSCR', 'PAMSTR', 'NPUST', 'PARTN', ...)       znak "vlastnění registrem"
+------------------+--------------+
|  EXURL           |  VARCHAR     |     odchod do EKZ
+------------------+--------------+
|  IDNAZ           |  VARCHAR     |     jméno objektu v RVS ČR
+------------------+--------------+
+------------------+--------------+
|  PRIJEM          |  BIT         |     schválení neschválení
+------------------+--------------+
|  ADMIN_ID        |  INT(10)     |    
+------------------+---------------+
|  KAT_1           |  VARCHAR(255) |     "1, 1, 2, 0, 0, 0, 3"
+------------------+---------------+
|  KAT_2           |  VARCHAR(255) |
+------------------+---------------+
|  KAT_3           |  VARCHAR(255) |
+------------------+---------------+
|  KAT_4           |  VARCHAR(255) |
+------------------+---------------+
|  KAT_5           |  VARCHAR(255) |
+------------------+---------------+
|  OHRO_1          |  VARCHAR(255) | 'A,C'
+------------------+---------------+
|  OHRO_2          |  VARCHAR(255) |
+------------------+---------------+
|  OHRO_3          |  VARCHAR(255) |
+------------------+---------------+
|  OHRO_4          |  VARCHAR(255) |
+------------------+---------------+
|  OHRO_5          |  VARCHAR(255) |
+------------------+---------------+
|  COM_U           |  TEXT         |
+------------------+---------------+
|  COM_A           |  TEXT         |
+------------------+---------------+

+------------------+--------------+
|  LON             |  FLOAT       |
+------------------+--------------+
|  LAT             |  FLOAT       |
+------------------+--------------+
|  KODKU                                    katastrální území
+------------------+--------------+
|  MZCHU                                    kód maloplošného zvláště chráněného území
+------------------+--------------+
|  VZCHU                                    kód velkoplošného zvláště chráněného území
+------------------+--------------+
|  PRPAR                                    kód případného přírodního parku
+------------------+--------------+
|  VYKRP                                    označení kvalifikace významného krajinného prvku
+------------------+--------------+
|  PTAOB                                    kód pračí oblasti
+------------------+--------------+
|  EVVLO                                    kód evropsky významné lokality
+------------------+--------------+



+-----------------------------+
|          ADMIN_USER         |
+-----------+-----------------+
|   ID      |   INT(10)       |      unsigned NOT NULL AUTO_INCREMENT
+-----------+-----------------+
|   NAME    |   CHAR(255)
+-----------+-----------------+
|   PW      |   CHAR(60)           nodejs - bcrypt
+-----------+-----------------+
|   EMAIL   |   CHAR(255)     |
+-----------+-----------------+
|   TEL     |   CHAR(255)     |
+-----------+-----------------+

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
