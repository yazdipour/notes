# SQL

## JOINS

### Nested loops joins

If one join input is small (fewer than 10 rows) and the other join input is fairly large and indexed on its join columns, an index nested loops join is the fastest join operation because they require the least I/O and the fewest comparisons.

https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms191318(v%3dsql.105)

### Merge joins

If the two join inputs are not small but are sorted on their join column (for example, if they were obtained by scanning sorted indexes), a merge join is the fastest join operation. If both join inputs are large and the two inputs are of similar sizes, a merge join with prior sorting and a hash join offer similar performance. However, hash join operations are often much faster if the two input sizes differ significantly from each other. For more information, see Understanding Merge Joins.

https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms190967(v%3dsql.105)

### Hash joins

Hash joins can efficiently process large, unsorted, nonindexed inputs. They are useful for intermediate results in complex queries because:

* Intermediate results are not indexed (unless explicitly saved to disk and then indexed) and often are not suitably sorted for the next operation in the query plan.
* Query optimizers estimate only intermediate result sizes. Because estimates can be very inaccurate for complex queries, algorithms to process intermediate results not only must be efficient, but also must degrade gracefully if an intermediate result turns out to be much larger than anticipated.

The hash join allows reductions in the use of denormalization. Denormalization is typically used to achieve better performance by reducing join operations, in spite of the dangers of redundancy, such as inconsistent updates. Hash joins reduce the need to denormalize. Hash joins allow vertical partitioning (representing groups of columns from a single table in separate files or indexes) to become a viable option for physical database design.

https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms189313(v%3dsql.105)

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