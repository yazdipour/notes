# SQL

## Search

```sql
$q="SELECT * FROM $table_name WHERE $from LIKE '%$what%'";
$q="SELECT *, MATCH ($from) AGAINST ('$what') AS score FROM $table_name WHERE MATCH ($from) AGAINST ('$what') ORDER BY score ASC";
```

## ACID

Atomicity, Consistency, Isolation, Durability

## CRUD

Create read update delete

### Normalization

* First normal form: no repeating values, no repeating groups
* Second normal form: third normal form: no non-key values based on just part of a composite key
* Third normal form: no non-key values based on other non-key values

### Basics

```sql
Create DB: CREATE DATABASE  dbName authorization creatorUser
SELECT: Select * from table1 where 1
Insert: Insert into table1 VALUES(x,y,z,a)
DROP: DROP DATABASE dbName;
Delete Record: Delete from table1 where score is null
Update Record: Update table1 set phone=110  where name='ali'
Order: Select * from table1 ordered by name DESC - / ASC +
Union: Select name from t1 UNION select pname from t2
Except: Select pname from t1 EXCEPT select sname from t2
IN: Select * from t1 where city IN('The','LA')
MIN / MAX/ SUM / AVG: Select min(score) form t1
GroupBy: Select a,b from t1 GROUP BY a   (a must be in select)
Count id: Select count(id) from t1 //ids are unique
Count all: Select count(*) from t1 // * is unique
Domain: Create domain season char(8) 
        Default "Spring"
        Check (value in 'Spring','Summer',…);

Create Tb:  Create table tableName{
                id int(10) not null Primary Key,
                Primary key(id),
                unique(phone Nr),
                foreign key(clg) reference clg(clg#)
                On delete cascade
                on update cascade
                Check( unit>0 and unit<5);
            }
            Create TABLE tName (id int not null primary key auto_increment, tName INT unique)

AlterTb:    Alter table table1 modify 'C#' int
            Alter table table1 add 'text' char(100)
            Alter table table1 drop 'xxx'
            Alter table table1 add INDEX(id);
            Alter table table1 add FOREIGNKEY(sec_id)REFERENCES section(sec_id)ON DELETE CASCADE
            ALTER TABLE `section` ADD PRIMARY KEY (`course_id`);

Procedure:  Delimiter //
            Create Procedure foo(IN id int, OUT total int)
            Begin
            Select * from t1 where ID=id
            End //
            Delimiter ;
            @total=1;
            CALL foo(id,@total);
            PROCEDURE +	DELIMITER: //
            Dynamic Table	CREATE PROCEDURE getCount (IN whereFrom VARCHAR(255), OUT result INT)
            BEGIN
            SET @query = CONCAT('SELECT COUNT(Id) INTO @v FROM ',whereFrom);
            PREPARE stmt FROM @query;
            EXECUTE stmt;
            SET result=@v;
            END//
```

### MySql

```sql
mysql DATABASENAME -h localhost -u USERNAME -p PASSWORD  

mysqldump DATABASENAME -h localhost -u USERNAME -p PASSWORD  

SHOW DATABASES;

SELECT DATABASE();

USE dbName;

DESCRIBE tableName;
```