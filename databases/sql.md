__Structured Query Language (SQL)__ → domain-specific programming language designed for managing data held in a relational database management system.

### Basic syntax
The semicolon (`;`) is the standard way to separate statements. The SQL keywords, such as `SELECT`, are usually written in uppercase, whilst the data or parameters in lowercase.

## Basic Statements
#### `CREATE TABLE`
Creates a new SQL table.
```sql
CREATE TABLE Students
  (first_name VARCHAR(255),
  last_name VARCHAR(255),
  age INTEGER);
```

#### `DROP TABLE`
Deletes a table. All data within it will be erased.
```sql
DROP TABLE Students;
```

#### `INSERT`
Add new rows of data to a table.
```sql
INSERT INTO Students(first_name, last_name, age)
  VALUES
    ('Helena', 'Vesley', 15), 
    ('Marvel', 'Vallette', 16), 
    ('Claribel', 'Lynd', 15);
```

#### `SELECT`
Fetches data in a database, returning it in a table format.
```sql
SELECT first_name, last_name FROM Students;
```
If we want to select every column we can use `*` instead of te columns' name.

## Clauses
__Clause__ → logical chunk of an SQL statement. We can specify conditions for the values we want to be returned.

#### `WHERE`
States a condition while fetching data from a database.
```sql
SELECT * FROM Students
  WHERE age=15;
```

We can also combine multiple clauses with `AND`, `OR`, and `LIKE`.
```sql
SELECT * FROM Students
  WHERE age>14 AND first_name LIKE 'H%';
```

#### `COUNT`, `AVG`, and `SUM`
`COUNT` finds the count of a column/columns in a table, `AVG` the average, and `SUM` computes the sum of all values.
```sql
SELECT COUNT(first_name) FROM Students;
```

#### `LIMIT`
Cuts off responses to just a specified amount.
```sql
SELECT * FROM Students LIMIT 3;
```

## Others
#### `ORDER BY`
Sorts the results in ascending or descending order.
```sql
SELECT * FROM Students ORDER BY first_name ASC;
```

#### `GROUP BY`
Groups categories that have the same values into rows.
```sql
SELECT COUNT(first_name), age FROM Students GROUP BY age;
```

# Sources
[What is SQL? What is a Database? Relational Database Management Systems (RDBMS) Explained in Plain English. – FreeCodeCamp](https://www.freecodecamp.org/news/sql-and-databases-explained-in-plain-english/)