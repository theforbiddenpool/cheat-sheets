__PostgreSQL__ → the actual database engine.

__SQL__ → the actual Structured Query Language. It allows us to interact with a relational database.

## CMD Client
#### Enter CMD Client
```
$ psql
```
- `-d <name>` → connect to specific database.
- `-h <name>` → database server host or socket directory.
- `-p <number>` → database server port.
- `-U <name>` → database user name.
- `-w` → don't prompt for password.

The commands start with a `\`.

Some useful commands are:
- `\? [command]` → help command, lists all commands available, or more information about a certain command.
- `\l` → lists databases.
- `\c <name>` → connect to specific database.
- `\d <name>` → list all relations (tables, sequences), or describe table if name is provided.
- `\dt` → list only tables.
- `\i <path>` → run SQL script.
- `\copy <command>` → copy data to a file. To export the data to an CSV, we can use the command `\copy (<query>) TO <file-path>.csv DELIMITER ',' CSV HEADER;`
- `\df` → list available functions.

## Functions
### Date and Timestamps
To get the current timestamp, we can use the `NOW()` function. This will display the date, time, and timezone (*e.g.*, `2018-12-02 22:43:41.774892+00`). We can get only actual date, we can cast it:

``` sql
SELECT NOW()::DATE;
```
We can also cast it to a time, using `::TIME`.

#### Arithmetics with Dates
Both addition and subtraction is possible with dates. We have to make use of the `INTERVAL` keyword.
```sql
SELECT NOW() - INTERVAL '10 MONTHS';
```
We can use `YEARS`, `MONTHS`, `DAYS`, or the singular version of it. It's also possible to calculate with weeks, hours, minutes, etc.

This will always return a timestamp. However, we can use casting to return a date.
```sql
SELECT (NOW() + INTERVAL '10 MONTHS')::DATE;
```

#### Extracting fields
The keyword `EXTRACT` can be used to return the field that we want, *e.g.* the year.
```sql
SELECT EXTRACT(YEAR FROM NOW())
```
We can use `YEAR`, `MONTH`, `DAY`, `DOW` (day of the week), `CENTURY`, etc.

#### `AGE` 
We can get someone's age by providing the current date and their date of birth.
```sql
SELECT first_name, country_of_birth, date_of_birth, AGE(NOW(), date_of_birth) AS age FROM students;
```

## Sequences
Sequences are simply auto-incremented integers. They are managed by `nextval('person_id_seq'::regclass)`. Every time we invoke this function, the sequence is updated. This can create holes in the numbers added.

#### View sequence information
```sql
SELECT * from students_id_seq;
```

#### Restart the value of the sequence
```sql
ALTER SEQUENCE students_id_seq RESTART WITH 10;
```
`10` being the next value that the sequence will have.

## Extensions
PostgreSQL was designed to be incredibly extensible. A couple ones of note are:
- **hstore** → data type for storing sts of (key, value) pairs.
- **pg_visibility** → examine the visibility map (WM) and page-level visibility info.
- **plv8** → allows us to write JavaScript functions.
- **sslinfo** → information about SSL certificates.
- **uuid-ossp** → generate universally unique identifiers (UUIDs). 

#### View list of all available extensions
```sql
SELECT * FROM pg_available_extensions;
```

#### Install an extension
```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

# Sources
[Learn PostgreSQL Tutorial - Full Course for Beginners – FreeCodeCamp Youtube](https://youtu.be/qw--VYLpxG4)
