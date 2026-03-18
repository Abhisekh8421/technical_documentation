

# ACID Properties in Database

## Introduction

ACID is a set of four properties that guarantee reliable database transactions.

ACID stands for:

* Atomicity
* Consistency
* Isolation
* Durability

These properties ensure that data remains correct even if errors, crashes, or multiple users access the system at the same time.

A transaction is a group of operations that are executed as a single unit.

Example of a transaction:

* Deduct money from Account A
* Add money to Account B

Both operations must succeed together.

---

# 1. Atomicity

## Meaning

Atomicity means:

A transaction must complete fully or not run at all.

There is no partial execution.

Either everything happens or nothing happens.



---

# 2. Consistency

## Meaning

Consistency means:

After a transaction completes, the database must follow all rules and constraints.

Data must move from one valid state to another valid state.



---

# 3. Isolation

## Meaning

Isolation means:

Multiple transactions running at the same time should not interfere with each other.

Each transaction should behave as if it is running alone.



---

# 4. Durability

## Meaning

Durability means:

Once a transaction is committed, it will remain saved permanently.

Even if the system crashes.





---

# CAP Theorem in Distributed Systems

## Introduction

CAP Theorem is a principle that explains the limitations of distributed systems.

CAP stands for:

* Consistency
* Availability
* Partition Tolerance


A distributed system means multiple servers working together over a network.

Example:

* Server A in one location
* Server B in another location

If the network between them fails, the system must choose between consistency and availability.

---

# 1. Consistency

## Meaning

Consistency means:

Every read receives the most recent write.

All users see the same data at the same time.

If I update data, everyone must immediately see that updated value.



---

# 2. Availability

## Meaning

Availability means:

Every request receives a response.

The system should always reply, even if some servers fail.

It may return old data, but it must respond.



---

# 3. Partition Tolerance

## Meaning

Partition tolerance means:

The system continues working even if communication between servers breaks.

A partition happens when:

Two servers cannot communicate due to network failure.





---

# CP System

Consistency + Partition Tolerance

If a partition occurs:

The system may reject some requests to keep data correct.

## Example

Banking system.

If network breaks between two branches:

One branch may stop processing transactions.

This ensures:

* No double spending
* No incorrect balances

Availability is sacrificed to maintain correctness.

---

# AP System

Availability + Partition Tolerance

If a partition occurs:

Both sides continue working.

Data may temporarily become inconsistent.

## Example

Social media platform.

If I like a post:

Some users may not see it immediately.

But the app does not stop working.

Later, data becomes consistent.

Availability is prioritized over immediate consistency.

---

# CA System

Consistency + Availability

Possible only when there is no partition.

Example:

Single-server system.

If the server crashes, the whole system stops.

There is no partition concept because it is not distributed.

---


# Joins in SQL

## Introduction

A Join is used to combine rows from two or more tables based on a related column.

Usually, tables are connected using:

* Primary Key
* Foreign Key

Joins help me retrieve related data stored in different tables.

Example:

Table 1: students
Table 2: courses

If I want to know which student enrolled in which course, I use a JOIN.

---

# Example Tables

## Students Table

| id | name  |
| -- | ----- |
| 1  | Abhi  |
| 2  | Ravi  |
| 3  | Ankit |

## Enrollments Table

| student_id | course  |
| ---------- | ------- |
| 1          | Math    |
| 2          | Science |
| 4          | English |

Now let us understand different types of joins.

---

# 1. INNER JOIN

## Meaning

INNER JOIN returns only the matching rows from both tables.

If there is no match, the row is not included.

## Query Example

```sql
SELECT students.name, enrollments.course
FROM students
INNER JOIN enrollments
ON students.id = enrollments.student_id;
```

## Result

| name | course  |
| ---- | ------- |
| Abhi | Math    |
| Ravi | Science |

Student with id 3 is not shown because there is no matching record.

## When to Use

When I only want matched data from both tables.

---

# 2. LEFT JOIN (LEFT OUTER JOIN)

## Meaning

LEFT JOIN returns:

* All rows from the left table
* Matching rows from the right table
* NULL if no match

## Query Example

```sql
SELECT students.name, enrollments.course
FROM students
LEFT JOIN enrollments
ON students.id = enrollments.student_id;
```

## Result

| name  | course  |
| ----- | ------- |
| Abhi  | Math    |
| Ravi  | Science |
| Ankit | NULL    |

Ankit appears even though there is no course.

## When to Use

When I want all records from the main table, even if there is no match.

---

# 3. RIGHT JOIN (RIGHT OUTER JOIN)

## Meaning

RIGHT JOIN returns:

* All rows from the right table
* Matching rows from the left table
* NULL if no match

## Query Example

```sql
SELECT students.name, enrollments.course
FROM students
RIGHT JOIN enrollments
ON students.id = enrollments.student_id;
```

## Result

| name | course  |
| ---- | ------- |
| Abhi | Math    |
| Ravi | Science |
| NULL | English |

Student id 4 does not exist in students table, so name is NULL.

## When to Use

When I want all records from the right table.


---

# 4. FULL JOIN (Using UNION Method)

## Meaning

Since some databases do not support FULL JOIN directly, I can simulate it using:

* LEFT JOIN
* UNION
* RIGHT JOIN

This returns:

* All rows from both tables
* NULL where there is no match

---

## Query Example

```sql
SELECT students.name, enrollments.course
FROM students
LEFT JOIN enrollments
ON students.id = enrollments.student_id

UNION

SELECT students.name, enrollments.course
FROM students
RIGHT JOIN enrollments
ON students.id = enrollments.student_id;
```

---

## Result

| name  | course  |
| ----- | ------- |
| Abhi  | Math    |
| Ravi  | Science |
| Ankit | NULL    |
| NULL  | English |

Includes everything from both tables.


## When to Use

When my database does not support FULL JOIN, and I want all data from both tables.


---

# 5. CROSS JOIN

## Meaning

CROSS JOIN returns the Cartesian product.

Every row from table 1 combines with every row from table 2.

## Query Example

```sql
SELECT students.name, enrollments.course
FROM students
CROSS JOIN enrollments;
```

If students has 3 rows and enrollments has 3 rows:

Result = 3 × 3 = 9 rows.

## When to Use

Rarely used. Mostly for combinations.

---

# 6. SELF JOIN

## Meaning

A table joined with itself.

Used when I want to compare rows within the same table.




---

# Aggregations and Filters in SQL

## Introduction

Aggregation functions are used to perform calculations on multiple rows and return a single result.

Filters are used to limit the rows that are returned in a query.





---

# 1. Aggregation Functions

Aggregation functions operate on multiple rows and return a single value.

## Common Aggregation Functions

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()

---

# COUNT()

## Meaning

COUNT() returns the number of rows.

## Example

```sql
SELECT COUNT(*) FROM students;
```

Returns total number of students.

---

# SUM()

## Meaning

SUM() returns the total of a numeric column.

## Example

```sql
SELECT SUM(salary) FROM employees;
```

Returns total salary of all employees.

---

# AVG()

## Meaning

AVG() returns the average value.

## Example

```sql
SELECT AVG(salary) FROM employees;
```

Returns average salary.

---

# MIN() and MAX()

## Meaning

MIN() returns smallest value.
MAX() returns largest value.

## Example

```sql
SELECT MIN(salary), MAX(salary)
FROM employees;
```

Returns lowest and highest salary.

---

# 2. GROUP BY

## Meaning

GROUP BY is used with aggregation functions to group rows based on a column.

Instead of calculating on entire table, I calculate per group.





---

# 3. Filters in Queries

Filters are used to restrict rows.

There are two main types:

* WHERE
* HAVING

---

# WHERE Clause

## Meaning

WHERE filters rows before aggregation.

It works on individual rows.



---

# HAVING Clause

## Meaning

HAVING filters after aggregation.

It works on grouped results.


---

# Normalization in Database

## Introduction

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity.

It helps in:

* Removing duplicate data
* Avoiding data anomalies
* Maintaining consistency

Normalization divides large tables into smaller related tables.

---

# Why Normalization Is Needed

Without normalization:

* Data duplication increases
* Updating data becomes difficult
* Deleting data may remove important information
* Insertion may cause errors

These problems are called:

* Insertion anomaly
* Update anomaly
* Deletion anomaly

---

# Example Without Normalization

Suppose I have a single table:

| student_id | student_name | course  | instructor |
| ---------- | ------------ | ------- | ---------- |
| 1          | Abhi         | Math    | Sharma     |
| 2          | Ravi         | Math    | Sharma     |
| 3          | Ankit        | Science | Mehta      |

Problems:

* Instructor "Sharma" is repeated
* If instructor changes, I must update multiple rows
* If I delete last student of Math, course info is lost

---

# Normal Forms

Normalization is divided into stages called Normal Forms.

The main ones are:

* 1NF (First Normal Form)
* 2NF (Second Normal Form)
* 3NF (Third Normal Form)
* BCNF (Boyce-Codd Normal Form)

---

# 1. First Normal Form (1NF)

## Rule

* Each column must have atomic values
* No repeating groups
* Each field contains only one value

## Example (Not in 1NF)

| id | name | courses       |
| -- | ---- | ------------- |
| 1  | Abhi | Math, Science |

Here courses contains multiple values.

## Convert to 1NF

| id | name | course  |
| -- | ---- | ------- |
| 1  | Abhi | Math    |
| 1  | Abhi | Science |

Now each cell contains a single value.

---

# 2. Second Normal Form (2NF)

## Rule

* Must be in 1NF
* No partial dependency

Partial dependency happens when:

A non-key column depends on only part of a composite primary key.



---

# 3. Third Normal Form (3NF)

## Rule

* Must be in 2NF
* No transitive dependency

Transitive dependency means:

A non-key column depends on another non-key column.



---

# BCNF (Boyce-Codd Normal Form)

## Rule

For every functional dependency:

The determinant must be a candidate key.

BCNF is stronger than 3NF.

It handles special cases where 3NF is not enough.

---

# Advantages of Normalization

* Reduces redundancy
* Improves data consistency
* Saves storage space
* Prevents anomalies

---

# Disadvantages of Normalization

* More tables
* More joins
* Slightly slower read performance

Sometimes databases use denormalization for performance.





---

# Indexes

## Introduction

An index is a database structure that improves the speed of data retrieval.

Without an index, the database performs a full table scan.

With an index, the database can directly locate data.

Indexes are usually implemented using B+ Trees.

---

## Why Index Is Needed

If a table has 1 million rows and I search for one record:

Without index:
The database checks every row.

With index:
The database quickly finds the record using the indexed column.

---

## Types of Indexes

### 1. Clustered Index

* Determines physical order of data.
* Only one clustered index per table.
* Data is stored sorted by that column.

Example:
Primary key often creates clustered index.

---

### 2. Non-Clustered Index

* Stored separately from table data.
* Contains key and pointer to actual row.
* Multiple allowed per table.

Search happens in two steps:

1. Search index
2. Fetch row

---

### 3. Composite (Multi-Column) Index

* Index on multiple columns.
* Follows left-to-right rule.

Example:

```sql
CREATE INDEX idx_name_city
ON students(name, city);
```

Works efficiently for:

* WHERE name = 'Abhi'
* WHERE name = 'Abhi' AND city = 'Delhi'

---

## Advantages

* Faster SELECT queries
* Improves search performance

## Disadvantages

* Slows INSERT, UPDATE, DELETE
* Uses extra storage

---

# Transactions

## Introduction

A transaction is a group of operations executed as a single unit.

Example:

* Deduct money from Account A
* Add money to Account B

Both must succeed together.

---

## Basic Commands

```sql
BEGIN;
COMMIT;
ROLLBACK;
```

BEGIN starts transaction.
COMMIT saves changes.
ROLLBACK cancels changes.

---

## Why Transactions Are Important

They ensure:

* Data correctness
* Reliability
* Safety during failures

Transactions follow ACID properties.

---

# Locking Mechanism

## Introduction

Locking prevents multiple transactions from modifying the same data at the same time.

It ensures data consistency.

---

## Types of Locks

### 1. Shared Lock (Read Lock)

* Multiple transactions can read.
* No transaction can write.

---

### 2. Exclusive Lock (Write Lock)

* Only one transaction can modify.
* Others must wait.

---

## Lock Levels

* Row-level lock
* Page-level lock
* Table-level lock

Row-level lock provides better concurrency.

---



# Database Isolation Levels

## Introduction

Isolation level controls how transactions interact with each other.

Higher isolation means stricter rules but less concurrency.

---

## Four Isolation Levels

### 1. Read Uncommitted

* Can read uncommitted data.
* Allows dirty reads.

---

### 2. Read Committed

* Can only read committed data.
* Prevents dirty reads.

(Default in many systems)

---

### 3. Repeatable Read

* Ensures rows read cannot change during transaction.
* Prevents non-repeatable reads.

---

### 4. Serializable

* Highest isolation level.
* Transactions behave as if executed one by one.
* Prevents phantom reads.

---

## Common Problems

* Dirty Read
* Non-Repeatable Read
* Phantom Read

Isolation levels control these problems.

---

# Triggers

## Introduction

A trigger is a database object that automatically executes when a specific event occurs.

Events:

* INSERT
* UPDATE
* DELETE

Triggers run automatically.

---

## Types of Triggers

### Based on Timing

* BEFORE
* AFTER
* INSTEAD OF

---

### Based on Level

* FOR EACH ROW
* FOR EACH STATEMENT
---




























