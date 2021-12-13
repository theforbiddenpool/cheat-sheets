__Structured Query Language (SQL)__ → domain-specific programming language designed for managing data held in a relational database management system.

### Basic syntax
The semicolon (`;`) is the standard way to separate statements. The SQL keywords, such as `SELECT`, are usually written in uppercase, whilst the data or parameters in lowercase.

## Basic Statements
#### `CREATE TABLE`
Creates a new SQL table.
```sql
CREATE TABLE students
  (first_name VARCHAR(255),
  last_name VARCHAR(255),
  age INTEGER);
```

#### `DROP TABLE`
Deletes a table. All data within it will be erased.
```sql
DROP TABLE students;
```

#### `INSERT`
Add new rows of data to a table.
```sql
INSERT INTO students(first_name, last_name, age)
  VALUES
    ('Helena', 'Vesley', 15), 
    ('Marvel', 'Vallette', 16), 
    ('Claribel', 'Lynd', 15);
```

#### `SELECT`
Fetches data in a database, returning it in a table format.
```sql
SELECT first_name, last_name FROM students;
```
If we want to select every column we can use `*` instead of te columns' name.

## Clauses
__Clause__ → logical chunk of an SQL statement. We can specify conditions for the values we want to be returned.

#### `WHERE`
States a condition while fetching data from a database.
```sql
SELECT * FROM students
  WHERE age=15;
```

We can also combine multiple clauses with `AND`, `OR`, and `LIKE` (or `ILIKE` for case-insensitivity).
```sql
SELECT * FROM students
  WHERE age>14 AND first_name LIKE 'H%';
```
- `%` → any character.
- `_` → single character.

If we have a list that we want to compare to a single column, we can use the keyword `IN`.
```sql
SELECT * FROM students
  WHERE contry_of_birth IN ('China', 'Brazil', 'Poland');
```

To select something that is between a range of numbers, we can use `BETWEEN`.
```sql
SELECT * FROM students
  WHERE date_of_birth BETWEEN DATE '2000-01-01' AND '2015-01-01';
```

#### `COUNT`, `AVG`, and `SUM`
`COUNT` finds the count of a column/columns in a table, `AVG` the average, and `SUM` computes the sum of all values.
```sql
SELECT COUNT(first_name) FROM students;
```
There are also functions for `MIN`, and `MAX`. 

`ROUND` rounds the number displayed.
```sql
SELECT ROUND(AVG(age)) FROM students;
```

#### `LIMIT`
Cuts off responses to just a specified amount.
```sql
SELECT * FROM students LIMIT 3;
```

## Others
#### `ORDER BY`
Sorts the results in ascending or descending order.
```sql
SELECT * FROM students ORDER BY first_name ASC;
```

#### `GROUP BY`
Groups categories that have the same values into rows.
```sql
SELECT COUNT(first_name), age FROM students GROUP BY age;
```

We can use the `HAVING` keyword to further restrict the query results shown.
```sql
SELECT COUNT(*), age FROM students GROUP BY age HAVING COUNT(*) > 5;
```
This will only display the rows that have a count superior to 5.

#### `DISTINCT`
Returns only different values.
```sql
SELECT DISTINCT country_of_birth FROM students;
```

#### `COALESCE`
Will return a default value, if the first is not present.
```sql
SELECT COALESCE(null, 1);
```
This will return `1`.

```sql
SELECT COALESCE(email, 'email not provided') FROM person;
```

#### `NULLIF`
Returns the first argument, if the second argument is not equal to the first one.
```sql
SELECT NULLIF(10, 9);
```
This will return `10`.

Together with `COALESCE`, it can be used to handle division by 0. Instead of throwing an error, it will display `0`.
```sql
SELECT COALESCE(10 / NULLIF(0, 0), 0);
```

## Constraints
### `CHECK`
It allows us to limit the data that can be inserted according to a boolean operation. We can have any condition that we want.

#### Create a constraint
```sql
ALTER TABLE students ADD CONSTRAINT gender_constraint CHECK(gender = 'female' OR gender = 'male');
```
If there's an attempted to add another value but the ones provided, the query will throw an error.

## Dealing with Conflicts
The `ON CONFLICT` keyword allows us to specify behavior that should happen if a conflict and errors (*e.g.* adding a new row with an id already in use) happens. This will only work if there's an `UNIQUE` constraint on the column we're specifying.

```sql
INSERT INTO students(id, first_name, last_name, email)
  VALUES(2017, 'Rus', 'Ruddoch', 'rruddoch7@hhs.gov')
  ON CONFLICT (id) DO NOTHING;
```
No rows will be inserted, but no error will be thrown either.

It is also possible to do an upsert. This useful for the situations where, for example, an user sends two requests to create an account, one after the other, and we want to update the information to the latest request.
```sql
INSERT INTO students(first_name, last_name, email)
  VALUES('Rus', 'Ruddoch', 'rruddoch7@hhs.uk')
  ON CONFLICT (email) DO UPDATE SET email = EXCLUDED.email;
```
The `EXCLUDED` keyword is the email that was supposed to be inserted (the 2nd request). Any field can be updated, including `first_name`, `last_name`, etc.

# Sources
[What is SQL? What is a Database? Relational Database Management Systems (RDBMS) Explained in Plain English. – FreeCodeCamp](https://www.freecodecamp.org/news/sql-and-databases-explained-in-plain-english/)\
[Learn PostgreSQL Tutorial - Full Course for Beginners – FreeCodeCamp Youtube](https://youtu.be/qw--VYLpxG4)