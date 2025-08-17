### Setting up a table
* Postgres is the worlds most advanced open-source database
* Relational databases store data in tables which consists of **rows** and **columns**
```postgresql
CREATE TABLE users (
    name TEXT,
    age INTEGER,
    join_date DATE
);
```
In the example above, we created a table called `users` with three columns.

1. The `name` column is of type `TEXT`
2. The `age` column is of type `INTEGER`
3. The `join_date` column is of type `DATE`

This is the **schema** of the table. It's analogous to a class definition in object-oriented programming.

The `CREATE TABLE` statement is used to create a new table within a database.

* SQL is not case sensitive meaning that SQL keywords can be written in any case
* However the convention is that the SQL keywords are written in uppercase and the table and column names are written in lowercase. This will make the SQL easier to read.
### Default Values
* Table columns can have default values.
* When inserting rows into a table it is possible to omit values for some columns
* Database will automatically insert null for those columns
	* Or you can specify a specific value
```postgresql
CREATE TABLE users (
    name TEXT DEFAULT 'Anonymous',
    email TEXT,
    age INTEGER DEFAULT 18
);
```
### Altering a table
* The `Alter Table` statement allows you to add, modify, or drop columns in an existing table
* See the syntax below
```postgresql
CREATE TABLE users (
    name TEXT
);

-- Add a new column called `age` of type `INTEGER` to the table
ALTER TABLE users ADD COLUMN age INTEGER;

-- Modify the `name` column to be called `full_name` instead
ALTER TABLE users RENAME COLUMN name TO full_name;

-- Remove / drop the `name` column from the table
ALTER TABLE users DROP COLUMN name;
```
### Dropping a table from a database
* To drop an entire table from a database you can use the below SQL
```postgresql
CREATE TABLE users (
    name TEXT,
    age INTEGER
);

DROP TABLE users;
```
