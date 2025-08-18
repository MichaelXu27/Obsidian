### Not Null Constraints
* Sometimes we want to reinforce that a column must have a value, this can be done with the `NOT NULL` constraint
```postgresql
CREATE TABLE users (
    name TEXT NOT NULL,
    age INTEGER
);
```
* in this case name has the contraint `NOT NULL` which means the every row in the tabel must have a value for the name column
* The `NOT NULL` constraint can also be combined with a default value
```postgresql
CREATE TABLE users ( 
	name TEXT NOT NULL DEFAULT 'Anon',
	age INTEGER DEFAULT 0 NOT NULL
);
```
* As seen above, the order in which we place the `NOT NULL` and default constraints do not matter
### Unique Constraint

* This constraint is used when we want to ensure that a column or group of columns have unique values `UNIQUE`
```postgresql
CREATE TABLE users (
    email TEXT UNIQUE NOT NULL,
    name TEXT
);
```
### Primary Key
* This is a special column within a table*
	* must be unique for each row
	* cannot contain a `NULL` value
* Only one primary key per table
```postgresql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
);
```
* Its good practice to have a primary key in every table
* What is the difference between a primary key and combining the NOT NULL and UNIQUE constraints?
	* Primary key is a combination of NOT NULL and UNIQUE but with additional properties
		* only one primary key per table
		* can be made up of multiple columns known as a composite key
		* databases also create an index on the primary key to speed up queries
### Foreign Key
* A foreign key is a column or group of columns in a table that references a column in another table
* Essentially it establishes a relationship between two tables
```postgresql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT
);

CREATE TABLE videos (
    id INTEGER PRIMARY KEY,
    title TEXT,
    owner_id INTEGER REFERENCES users(id)
);

```
* We can see that there is a keyword `REFERENCES` , this creates the foreign key constraint
* The `owner_id` column in the `videos` table references the  `id` column in the `users` table.
	* This means that the value in `owner_id` column must exist in the id column of the `users` table
* A foreign key does not have to be unique, but it must match an existing value in the referenced column. The referenced column must be a primary key or have a unique constraint.
### Composite Primary Key
* A primary key can be made up of multiple columns, which is known as a **compound primary key** or a **composite primary key**
* The combination of columns in a composite primary key must be unique for each row
* The combination of values in the columns must be unique even if the individual columns are not
``` postgresql
CREATE TABLE employees (
    department_id INTEGER,
    employee_id INTEGER,
    name TEXT,
    PRIMARY KEY (department_id, employee_id)
);

```
* `PRIMARY KEY` constraint after the column list is another approach to adding primary keys but it is required for a composite or compound key

### Check constraint
* A rule that defines valid values for a column, allows you to specify a condition that each row in the table must satisfy

```postgresql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    age INTEGER CHECK (age >= 18)
);
```
Heres another example of how the check constraint can be used
```postgresql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    status TEXT CHECK (status IN ('active', 'inactive'))
);
```
* This means that the status column can only have the values of `'active'` or `'inactive'`