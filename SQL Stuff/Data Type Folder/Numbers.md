There are several ways to represent numbers in PostgreSQL
### Integers
* `SMALLINT`
	* stores a 2 byte signed integer
* `INTEGER`
	* stores a 4 byte signed integer
* `BIGINT`
	* stores a 8 byte signed integer
### Floating-point numbers
* `FLOAT`
	* stores a 4 byte floating point number
* `DOUBLE PRECISION`
	* stores a 8 byte floating point number
* `DECIMAL` == `NUMERIC`
	* stores a fixed point number where the precision is specified
	* `NUMERIC(10,1)` specified that the column can store up to 10 digits total and 1 to the right of the decimal point.
* 