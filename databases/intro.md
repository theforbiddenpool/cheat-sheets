__Database__ → collection of data. It allows us to organize data, *e.g.* numbers, dates, in a way that's useful for us.

__Database Management System (DBMS)__ → collection of programs which allows us to access databases and work with data, and add control access to users. There are two types of DBMS: **relational databases** and .

## Relational Databases
They consist of two or more tables, with columns and rows. The relation between tables and fields is called **schema**. Each schema must be clearly defined before any information can be added.

We can connect the information, by connecting different pieces of the table. This is done by using **foreign keys**.

__Primary key__ → the field that uniquely identifies each row in a tabje.

Some examples are PostgresSQL, Oracle, Mysql. They all follow a similar format.

All relational databases use **SQL** to communicate with the backend server.

## Non Relational Database (NoSQL)
They allow us to build an application without having to define the schema first. Some examples are MongoDB, Redis, CouchDB. They all have different ways of storing information, offering a greater flexibility.

Instead of using SQL, each one has its own query language.

NoSQL databases can be classified as four different types:
- __Key-Value__ → similar to how we handle objects in JavaScript, *e.g.* Redis.
- __Document__ → stores information as documents - each (for example) user has its own document, *e.g.* MongoDB, CouchDB.
- __Wide Column__ → *e.g.* Cassandra
- __Graph__ → *e.g.* Neo4j

## SQL vs NoSQL
SQL | NoSQL
--- | ---
Data uses Schemas | Schema-less
Relations | No (or very few) Relations
Data is distributed across multiple tables | Data is typically merged/nested in a few collections
Horizontal scaling is difficult/impossible; Vertical scaling is impossible | Both horizontal and vertical scalling is possible
Limitations for lots of (thousands) read & write queries per second | Great performance for multiple (simple) read & write requests

#### Better to use SQL when we have:
- structured data.
- complex queries, and need to handle relations between the data.
- a lot of complex writes, changing data in multiple tables.

#### Better to use NoSQL when we have:
- no opinion on how the data should look like, or don't know in what form the data will come.
- data with no relations.
- a lot of reads, and/or simple writes.

### Horizontal vs. Vertical Scaling
__Horizontal Scaling__ → if we want more performance, we can just add another server to the cluster. We can essentially scale infinitely.

__Vertical Scaling__ → if we need to improve performance, the only way is by adding more power to the server, *e.g.* more RAM, or better CPU.

MongoDB can scale both horizontally and vertically, whilst RDMSQL are limited to partitions for horizontal scaling, which aren't very good, and vertical scaling.

# Normalized vs Denormalized Databases
There are two main design patterns we can use when designing a database:
- __Normalized__ → optimizes for **minimizing redundancy**. We have two tables: Courses, and Teacher; they are connected via a foreign key. We have to query both tables if we want to get the teachers teaching a specific course. 
- __Denormalized__ → optimizes for **read time**. We only have one table (Courses), which contains the names of the teachers.

# Data Integrity
It's vital to users that the data they interact with is secure, correct, and sensible. Data integrity takes several forms and can be divided into four categories:
- __Entity Integrity__ → no duplicates rows exist in a table. 
- __Domain Integrity__ → enforcing correct values by restricting the type of values one can insert.
- __Referential Integrity__ → records used by other records cannot be deleted.
- __User-Defined Integrity__ → business-related logic and rules to the database.

# ACID
__ACID (Antomicity, Consistency, Isolation, Durability)__ → standard set of properties that guarantee database transactions are processed reliably. It's especially concerned with how a database recovers from any failure that might occur while processing a transation.

The ACID properties are designed as principles of transaction-oriented database recovery. They ensure data doesn't become corrupt as a resulf of a failure of some sort. Any ACID-compliant databases will ensure only successful transactions complete; if they fail, no data will be changed.

### Definition
- __Atomicity__ → if one part of the transaction fails, the whole transation fails.
- __Consistency__ → all data will be valid according to all defined rules.
- __Isolation__ → no transaction will be affected by any other transaction.
- __Durability__ → once a transaction is committed, it will remain in the system, even if there's a system crash immediately after.

### Types of Failure
- __Transaction Failure__ → bad input or some other violation of consistency, or timeout or deadlock in the DBMS.
- __System Failure__ → bug in the DBMS code, operating system fault, or hardware failure.
- __Media Failure__ → not being able to read from or write a storage device. Usually quite rare when compared with the previous types of failures.

## ACID Compliance
All of the major relational DBMSs adhere to the ACID principles. NoSQL databases are a bit different. They are often design to ensure high availabiity across a cluster, sacrificing consistency and/or durability. However, some vendors offer NoSQL DBMS.

# Keywords
__Relational Database Management Systems (RDBMS)__ → framework for databases such as MySQL.

__Structured Query Language (SQL)__ → domain-specific language designed for managing data in a RDBMS.

__Tables__ → database object that carry data. *e.g.* Students

__Fields__ → values of a table. *e.g.* First Name, on Students table

__Record / Row__ → an individual entry in the table.

# Sources
[What is SQL? What is a Database? Relational Database Management Systems (RDBMS) Explained in Plain English. – FreeCodeCamp](https://www.freecodecamp.org/news/sql-and-databases-explained-in-plain-english/)\
[What does ACID mean in Database Systems? – Database.Guide](https://database.guide/what-is-acid-in-databases/)\
[SQL vs NoSQL or MySQL vs MongoDB – Youtube](https://www.youtube.com/watch?v=ZS_kXvOeQ5Y)\
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
