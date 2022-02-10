# W5D1 - SQLf

## intro to SQL
- why database 
- DBMS 
- relational databases 
- SQL (structured sequal language)


## DBMS
- database management system 

## relational databases 
- the most popular type of databases of the last few decades 
- the data is broken down into tables with associations between them (relationships)
- each table is like a spreadsheet with columns and rows 
- we can query data with SQL

## SQL 
- developed by IMB in the early 70s
- initially called SEQUAL (structured english query language)
- declarative language (vs imperative)

### DDL - deata definition language 
- create and modify the structure of a database 

```
DROP TABLE IF EXISTS games;
CREATE TABLE games(
  id SERIAL PRIMARY KEY
  ...
)
```

Operations to declare (similar to CRUD)
- INSERT (c)
  - INSERT INTO ... (makes a new row on that table)
- UPDATE (u)
- DELETE (d)
- SELECT (r)

### terminal 

psql -U postgres -p 5433 spot
- -U postgres (postgres is a type of RDBS)
- -p 5433 (port)
- spot (name of file)

- /x toggle function to turn on extended display, turn row to columns to show all the information 

### select statement 
``` 
SELECT column list, function(), function(), ...
FROM table1
INNER JOIN table2
...
ON table.col1 = table2.col2
...
WHERE criteria for row selection 
[...]
```


### JOIN

why do we join two tables together?

when we need more data from more than just one table

to goin a main table with a side table to display two pieces of information from a table made on the fly

different types of joins
- inner join
- left || right outer join
  - left or right is the main table


### HAVING
