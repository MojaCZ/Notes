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
`DROP TABLE IF EXISTS 'user'`

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


## Example tables 1:1

```sql
DROP TABLE IF EXISTS 'user';

CREATE TABLE IF NOT EXISTS `db`.`user` (
  `id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(255) NOT NULL,
  `email` VARCHAR(255) NOT NULL,
  `password` VARCHAR(255) NOT NULL,
  `created` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `updated` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `email_UNIQUE` (`email` ASC),
  UNIQUE INDEX `id_UNIQUE` (`id` ASC))
ENGINE = InnoDB
AUTO_INCREMENT = 2
DEFAULT CHARACTER SET = utf8;
```

```sql
DROP TABLE IF EXISTS `db`.`user_detail` ;

CREATE TABLE IF NOT EXISTS `db`.`user_detail` (
  `id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `address` VARCHAR(255) NULL DEFAULT NULL,
  `postal_code` VARCHAR(20) NULL DEFAULT NULL,
  `city` VARCHAR(100) NULL DEFAULT NULL,
  `phone_number` VARCHAR(45) NULL DEFAULT NULL,
  `created` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `updated` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  UNIQUE INDEX `id_UNIQUE` (`id` ASC),
  CONSTRAINT `fk_user_detail_user`
    FOREIGN KEY (`id`)
    REFERENCES `db`.`user` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 3
DEFAULT CHARACTER SET = utf8;
```

If I try to run theuser_detail and insert an user id that does not exists, it throws an error
```sql
INSERT INTO `db`.`user` (`id`, `name`, `email`, `password`)
VALUES('100', 'John Doe', 'john.doe@example.com', 'aaa');


INSERT INTO `db`.`user_detail` (`id`, `address`, `postal_code`, `city`, `phone_number`)
VALUES('100', '91 Wembley Park', 'AB1 2CD', 'London', '123456789');
```

Querry these tables
```sql
SELECT 
	u.id, 
	u.name, 
	u.email, 
	u.password,
	ud.address,
	ud.postal_code,
	ud.city,
	ud.phone_number
FROM `db`.`user` u 
JOIN `db`.`user_detail` ud ON u.id = ud.id;
```