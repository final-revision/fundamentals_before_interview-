# SQL & MySQL Theory Interview Questions and Answers

## Complete Concept-Wise Revision Guide for Campus Placements and Written Tests

**Audience:** B.Tech students, freshers, campus placement candidates\
**Focus:** Pure theory, definitions, comparisons, concepts, and common
tricky interview questions\
**Dialect focus:** Core SQL with MySQL-specific notes where needed

> SQL is the language used to work with relational databases. MySQL is a
> relational database management system (RDBMS) that supports SQL. SQL
> features and syntax can differ between database systems such as MySQL,
> PostgreSQL, SQL Server, and Oracle.

------------------------------------------------------------------------

# 1. Database Fundamentals

### 1. What is data?

Data is a collection of raw facts or values, such as names, dates,
numbers, and transaction details.

### 2. What is a database?

A database is an organized collection of related data that can be
stored, retrieved, updated, and managed efficiently.

### 3. What is a DBMS?

A Database Management System (DBMS) is software that allows users and
applications to define, create, store, retrieve, update, and manage
databases.

Examples include MySQL, PostgreSQL, Oracle Database, Microsoft SQL
Server, and SQLite.

### 4. What is an RDBMS?

A Relational Database Management System stores data in relations,
commonly represented as tables of rows and columns, and supports
relationships between tables.

Examples: MySQL, PostgreSQL, SQL Server, Oracle Database.

### 5. What is the difference between DBMS and RDBMS?

  -----------------------------------------------------------------------
  DBMS                                RDBMS
  ----------------------------------- -----------------------------------
  General term for database           DBMS based on the relational model
  management software                 

  Data organization depends on the    Data is organized into
  system                              relations/tables

  May or may not support relational   Typically supports keys,
  constraints                         constraints, and relationships

  Examples include relational and     MySQL and PostgreSQL are examples
  non-relational systems              
  -----------------------------------------------------------------------

**Interview note:** It is too simplistic to say every DBMS has no
relationships or that every RDBMS is always more secure. Explain the
relational model and features instead.

### 6. What is a table?

A table is a database object that organizes related data into rows and
columns.

### 7. What are a row and a column?

-   **Row / record / tuple:** One individual entry in a table.
-   **Column / field / attribute:** One property shared by the records,
    such as `Email` or `Salary`.

### 8. What is a schema?

A schema describes database structure, such as tables, columns, data
types, constraints, views, and relationships. In MySQL, "schema" is also
commonly used as a synonym for database.

### 9. What is metadata?

Metadata is data about data, such as a column's name, type, size,
constraints, or table definition.

### 10. What is a data dictionary?

A data dictionary stores metadata about database objects. Database
systems expose this information through system catalogs or metadata
views.

### 11. What is a relational model?

The relational model represents data as relations (tables) and uses
values and logical operations to query and combine them.

### 12. What is a relationship between tables?

A relationship expresses how rows in one table relate to rows in
another, often through primary and foreign keys.

Common relationship types: - One-to-one - One-to-many - Many-to-many

### 13. What is a many-to-many relationship?

It is a relationship where each row in one entity may relate to multiple
rows in another and vice versa. It is normally implemented using a
junction/bridge table containing foreign keys to both entities.

### 14. What is a NULL value?

`NULL` represents missing, unknown, or inapplicable data. It is not the
same as zero, an empty string, or the text `'NULL'`.

### 15. What is the difference between NULL, zero, and an empty string?

-   `NULL`: value is unknown or absent.
-   `0`: a known numeric value.
-   `''`: a known string with zero characters.

------------------------------------------------------------------------

# 2. SQL Language and Command Categories

### 16. What is SQL?

SQL (Structured Query Language) is a language used to define, query,
manipulate, and control data in relational database systems.

### 17. Is SQL a programming language?

SQL is a declarative language: the user specifies what data or result is
required, and the database engine determines how to execute the request.
SQL also has procedural extensions in some systems, such as
stored-program languages.

### 18. What is the difference between SQL and MySQL?

-   **SQL:** The language.
-   **MySQL:** A database management system that implements SQL and adds
    system-specific features.

### 19. What are the main SQL command categories?

  -----------------------------------------------------------------------
  Category                Purpose                 Common commands
  ----------------------- ----------------------- -----------------------
  DDL --- Data Definition Define or change        `CREATE`, `ALTER`,
  Language                database objects        `DROP`, `TRUNCATE`

  DML --- Data            Change stored data      `INSERT`, `UPDATE`,
  Manipulation Language                           `DELETE`

  DQL --- Data Query      Retrieve data           `SELECT`
  Language                                        

  DCL --- Data Control    Permissions and access  `GRANT`, `REVOKE`
  Language                control                 

  TCL --- Transaction     Manage transactions     `COMMIT`, `ROLLBACK`,
  Control Language                                `SAVEPOINT`
  -----------------------------------------------------------------------

Some textbooks classify `SELECT` under DML rather than giving DQL a
separate category. `TRUNCATE` classification and transaction behavior
can vary by DBMS.

### 20. What is DDL?

DDL commands define or modify database structures. Examples:
`CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`.

### 21. What is DML?

DML commands insert, modify, or delete data in tables. Examples:
`INSERT`, `UPDATE`, `DELETE`.

### 22. What is DQL?

DQL is the commonly used category for querying data, especially
`SELECT`. Some classifications include it within DML.

### 23. What is DCL?

DCL manages permissions, such as granting or revoking a user's ability
to read or modify database objects.

### 24. What is TCL?

TCL commands control transactions, including committing changes, rolling
them back, or setting savepoints.

### 25. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

  -----------------------------------------------------------------------
  `DELETE`                `TRUNCATE`              `DROP`
  ----------------------- ----------------------- -----------------------
  Removes selected rows   Removes all rows from a Removes the table
  or all rows             table efficiently       object itself

  Supports `WHERE`        Does not support        Removes table
                          `WHERE`                 definition and its data

  Commonly DML            Usually classified as   DDL
                          DDL                     

  Transaction behavior    Often causes an         DDL commonly causes
  depends on engine and   implicit commit in      implicit commit in
  context                 MySQL                   MySQL

  Table structure remains Table structure remains Table no longer exists
  -----------------------------------------------------------------------

**MySQL caution:** `TRUNCATE TABLE` is DDL and causes an implicit
commit. It generally resets an `AUTO_INCREMENT` counter. Foreign-key
references can prevent truncation. Do not assume that `ROLLBACK` can
undo a truncate or drop.

### 26. What is the difference between `DROP DATABASE` and `DELETE`?

`DROP DATABASE` removes the database object and its contained objects;
`DELETE` removes rows from a table and leaves its structure intact.

### 27. What is `ALTER TABLE` used for?

It changes table structure, such as adding, modifying, renaming, or
dropping columns and constraints. Exact syntax depends on the database
version.

### 28. What is the difference between `CREATE` and `INSERT`?

`CREATE` creates a database object; `INSERT` adds rows to an existing
table.

### 29. What is the difference between `GRANT` and `REVOKE`?

`GRANT` assigns privileges; `REVOKE` removes privileges. Actual
effective access can also depend on roles and other grants.

------------------------------------------------------------------------

# 3. Keys and Constraints

### 30. What is a key in a database?

A key is an attribute or set of attributes used to identify rows,
establish relationships, or enforce uniqueness.

### 31. What is a super key?

A super key is any set of columns that uniquely identifies a row. It may
contain unnecessary attributes.

### 32. What is a candidate key?

A candidate key is a minimal super key: it uniquely identifies a row,
and no proper subset of it does.

### 33. What is a primary key?

A primary key is the candidate key selected to identify each row in a
table. It must be unique and cannot contain `NULL`.

### 34. Can a table have multiple primary keys?

A table has one primary-key constraint, but that key can consist of
multiple columns (a composite primary key). A table cannot define
multiple independent primary-key constraints.

### 35. What is a composite key?

A composite key consists of two or more columns that together identify a
row uniquely.

Example: `(StudentID, CourseID)` in an enrollment table.

### 36. What is an alternate key?

A candidate key that was not selected as the primary key is called an
alternate key.

### 37. What is a foreign key?

A foreign key is a column or group of columns whose values reference a
candidate/primary key in another table, or in some designs the same
table. It enforces referential integrity.

### 38. Can a foreign key contain NULL?

Yes, if the foreign-key column permits `NULL`. A nullable foreign key
can mean the row currently has no related parent. Composite foreign-key
NULL behavior depends on the database and constraint definition.

### 39. Can a foreign key contain duplicate values?

Yes. Many child rows can reference the same parent row. A foreign key
does not automatically require uniqueness.

### 40. What is a unique key / UNIQUE constraint?

A `UNIQUE` constraint prevents duplicate key values. NULL handling
depends on the DBMS; MySQL generally permits multiple `NULL` values in a
unique index.

### 41. Primary key vs UNIQUE key

  -----------------------------------------------------------------------
  Primary key                         UNIQUE constraint
  ----------------------------------- -----------------------------------
  Only one primary-key constraint per Multiple unique constraints can be
  table                               defined

  Cannot contain `NULL`               NULL handling is DBMS-dependent;
                                      MySQL allows multiple NULLs

  Main identifier for rows            Enforces uniqueness for an
                                      alternate identifier or business
                                      rule

  Can be composite                    Can be composite
  -----------------------------------------------------------------------

### 42. What is a natural key?

A natural key uses meaningful business data that already exists, such as
a country code or a carefully governed identifier.

### 43. What is a surrogate key?

A surrogate key is an artificial identifier created for database use,
such as an integer ID or UUID. It has no inherent business meaning.

### 44. What is an auto-increment column in MySQL?

`AUTO_INCREMENT` makes MySQL generate a new numeric value when a row is
inserted without an explicit value for that column. It is commonly used
for surrogate primary keys.

### 45. What is a constraint?

A constraint is a rule enforced by the database to protect data
integrity.

Common constraints: - `NOT NULL` - `UNIQUE` - `PRIMARY KEY` -
`FOREIGN KEY` - `CHECK` - `DEFAULT`

### 46. What does `NOT NULL` do?

It prevents a column from storing `NULL`. It does not, by itself,
prevent empty strings or zero.

### 47. What does `DEFAULT` do?

It supplies a value when an insert omits the column or uses the
`DEFAULT` keyword. An explicitly supplied `NULL` is not automatically
replaced by a default in ordinary cases.

### 48. What does `CHECK` do?

It enforces a Boolean condition on values, such as `Salary >= 0`.
Enforcement and behavior depend on DBMS/version; modern MySQL versions
enforce `CHECK` constraints.

### 49. What is referential integrity?

Referential integrity ensures that foreign-key references point to valid
parent keys, or are `NULL` when allowed.

### 50. What are `ON DELETE CASCADE` and `ON UPDATE CASCADE`?

-   `ON DELETE CASCADE`: deleting a referenced parent row automatically
    deletes related child rows.
-   `ON UPDATE CASCADE`: changing a referenced parent key automatically
    updates related foreign-key values.

Use cascades carefully because one action can affect many rows.

### 51. What is the difference between `RESTRICT`, `NO ACTION`, `CASCADE`, `SET NULL`, and `SET DEFAULT`?

They define what happens to child references when a referenced parent
key is deleted or updated. `CASCADE` propagates the change; `SET NULL`
sets child references to `NULL` if allowed; restrictive options reject
the change. `SET DEFAULT` is not supported by every database engine,
including typical MySQL InnoDB foreign-key behavior.

------------------------------------------------------------------------

# 4. Data Types in MySQL

### 52. What are the main MySQL data-type groups?

-   Numeric: `INT`, `BIGINT`, `DECIMAL`, `FLOAT`, `DOUBLE`
-   String/binary: `CHAR`, `VARCHAR`, `BINARY`, `VARBINARY`, `BLOB`,
    `TEXT`
-   Date/time: `DATE`, `TIME`, `DATETIME`, `TIMESTAMP`, `YEAR`
-   Other: `JSON`, spatial types, and `ENUM`/`SET`

### 53. Difference between `CHAR` and `VARCHAR`

  -----------------------------------------------------------------------
  `CHAR(n)`                           `VARCHAR(n)`
  ----------------------------------- -----------------------------------
  Fixed-length character type         Variable-length character type

  Values are stored using fixed-width Stores a length plus actual string
  semantics, with padding behavior    data

  Can be suitable for consistently    Usually suitable for
  short fixed-size values             variable-length text

  Trailing-space behavior depends on  Trailing-space behavior depends on
  type and collation                  type and collation
  -----------------------------------------------------------------------

The storage size depends on character set and implementation; do not
memorize an oversimplified "CHAR always takes more space" rule.

### 54. Difference between `VARCHAR` and `TEXT`

`VARCHAR` is a variable-length string type with a declared maximum
length; `TEXT` is intended for larger text values. Limits, indexing
rules, and storage details depend on MySQL version and row format.

### 55. Difference between `INT` and `BIGINT`

`BIGINT` supports a larger integer range but uses more storage than
`INT`. Choose based on expected values, not merely because one type is
larger.

### 56. Difference between `DECIMAL` and `FLOAT`/`DOUBLE`

-   `DECIMAL` stores exact fixed-point decimal values within its
    precision and scale; useful for money.
-   `FLOAT` and `DOUBLE` use approximate floating-point representation;
    useful for scientific or measurement data where approximation is
    acceptable.

### 57. Difference between `DATE`, `DATETIME`, and `TIMESTAMP`

-   `DATE`: date only.
-   `DATETIME`: date and time, generally stored without automatic
    time-zone conversion.
-   `TIMESTAMP`: MySQL converts between the session time zone and UTC on
    storage/retrieval; its supported range differs from `DATETIME`.

### 58. What is a collation?

A collation defines rules for comparing and sorting text, including case
and accent sensitivity. MySQL collation defaults depend on version and
configuration.

### 59. What is a character set?

A character set defines the characters that can be represented and how
they are encoded. `utf8mb4` is the recommended MySQL character set for
full Unicode support in modern applications.

### 60. What is `ENUM`?

`ENUM` restricts a column to one value from a predefined list. It can be
convenient for small, stable sets, but changes to allowed values and
portability should be considered.

### 61. What is the MySQL `JSON` type?

It stores valid JSON data and supports JSON functions and operators. It
is useful for semi-structured fields, but frequently queried attributes
may still benefit from ordinary columns or generated/indexed
expressions.

------------------------------------------------------------------------

# 5. SELECT Query Processing and Filtering

### 62. What is the logical order of SQL query processing?

A simplified logical order is:

1.  `FROM` and joins
2.  `WHERE`
3.  `GROUP BY`
4.  `HAVING`
5.  `SELECT`
6.  `DISTINCT`
7.  `ORDER BY`
8.  `LIMIT` / `OFFSET`

This is a logical model, not a guarantee of the physical execution
order. The optimizer may choose a different execution plan.

### 63. What is the difference between `WHERE` and `HAVING`?

`WHERE` filters individual rows before grouping; `HAVING` filters groups
after aggregation. Some systems allow `HAVING` without an explicit
`GROUP BY`.

### 64. What is the difference between `GROUP BY` and `ORDER BY`?

`GROUP BY` combines rows into groups for aggregation; `ORDER BY` sorts
the result rows. Grouping does not guarantee output order.

### 65. What is the difference between `DISTINCT` and `GROUP BY`?

`DISTINCT` removes duplicate result rows. `GROUP BY` forms groups,
usually for aggregate calculations. They can produce similar results in
some queries, but their purposes differ.

### 66. What is `ORDER BY`?

It sorts result rows by one or more expressions. Use `ASC` for ascending
and `DESC` for descending. Without `ORDER BY`, row order is not
guaranteed.

### 67. What are `LIMIT` and `OFFSET` in MySQL?

`LIMIT` caps the number of returned rows; `OFFSET` skips a specified
number before returning rows. Large offsets can be inefficient.
Pagination should use a stable order.

### 68. What is the difference between `LIKE` and `REGEXP`?

`LIKE` supports simple wildcard matching: `%` matches zero or more
characters and `_` matches one character. `REGEXP` uses regular
expressions; syntax and features depend on MySQL version.

### 69. What is the difference between `IN` and `EXISTS`?

`IN` tests whether a value matches a value in a set or subquery.
`EXISTS` tests whether a subquery returns any row. The optimizer may
transform either form; performance depends on data, indexes, and the
query plan.

### 70. What is a subquery?

A subquery is a query nested inside another SQL statement. It can return
a scalar value, a row, a table-like result, or a Boolean existence test
depending on context.

### 71. What is a correlated subquery?

A correlated subquery references columns from the outer query and is
logically evaluated in relation to each outer row, though the optimizer
may transform it.

### 72. What is a scalar subquery?

A scalar subquery returns exactly one column and at most one row. If it
returns more than one row in a scalar context, the database typically
raises an error.

### 73. What is a CTE?

A Common Table Expression (CTE), introduced with `WITH`, names a query
result for use within one statement. It improves readability and can be
recursive. MySQL supports CTEs in modern versions (8.0+).

### 74. What is a recursive CTE?

A recursive CTE refers to its own result and is useful for hierarchical
data, such as organization charts or category trees. Recursive syntax
and limits vary by database.

### 75. What is a view?

A view is a named query presented like a table. A normal view generally
stores the query definition, not a separate copy of the result data.
Some database systems also support materialized views; MySQL does not
provide native materialized views in the same way as PostgreSQL or
Oracle.

### 76. What is a materialized view?

A materialized view stores the result of a query physically and must be
refreshed or maintained. MySQL has no native materialized-view feature
equivalent to systems that support it; developers may use summary tables
and scheduled refresh logic.

### 77. What is an alias?

An alias gives a temporary name to a column or table within a query.
`AS` is optional in many alias contexts, but using it improves
readability.

### 78. What is `CASE`?

`CASE` is a conditional expression that returns a value based on
conditions, similar to if/else logic. It can be used in `SELECT`,
`ORDER BY`, aggregation, and other expressions.

### 79. What are aggregate functions?

Aggregate functions calculate one result from multiple input rows.
Common examples are `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`. Most ignore
`NULL` inputs; `COUNT(*)` counts rows.

### 80. What is the difference between `COUNT(*)` and `COUNT(column)`?

`COUNT(*)` counts rows, including rows with `NULL` values.
`COUNT(column)` counts rows where that column is not `NULL`.

### 81. What is the difference between `COUNT(column)` and `COUNT(DISTINCT column)`?

The former counts non-`NULL` values, including repeats; the latter
counts distinct non-`NULL` values.

------------------------------------------------------------------------

# 6. Joins and Set Operations

### 82. What is a join?

A join combines rows from two or more tables based on a matching
condition or join rule.

### 83. What is an `INNER JOIN`?

It returns rows for which the join condition matches on both sides.

### 84. What is a `LEFT JOIN`?

It returns all rows from the left table and matching rows from the
right. If no right-side match exists, right-side columns are returned as
`NULL`.

### 85. What is a `RIGHT JOIN`?

It returns all rows from the right table and matching rows from the
left. Unmatched left-side columns become `NULL`. Many queries can be
rewritten as a `LEFT JOIN` by swapping table order.

### 86. What is a `CROSS JOIN`?

It returns the Cartesian product: every row on one side paired with
every row on the other. If the tables contain `m` and `n` rows, the
result contains `m × n` rows.

### 87. What is a self join?

A self join joins a table to itself, using aliases to represent
different roles. Common uses include employees and their managers, or
comparing rows within the same table.

### 88. What is a full outer join?

It returns matched rows plus unmatched rows from both sides. MySQL does
not directly support `FULL OUTER JOIN`; it can often be emulated using
`LEFT JOIN` plus a `RIGHT JOIN`/anti-join with `UNION`, taking care not
to duplicate matches.

### 89. What is an equi join?

A join whose matching condition uses equality, such as
`a.DepartmentID = b.DepartmentID`.

### 90. What is a non-equi join?

A join using a non-equality condition such as `<`, `>`, or `BETWEEN`,
for example matching an employee salary to a salary-grade range.

### 91. What is the difference between `ON` and `WHERE` in a join?

`ON` specifies how rows match. `WHERE` filters the resulting rows. For
inner joins, many conditions can be moved between them without changing
results; with outer joins, moving a condition can change which unmatched
rows survive.

### 92. What is a Cartesian product?

It is every possible pairing of rows from two relations. It occurs
intentionally with a cross join and can occur accidentally if a join
condition is missing or incorrect.

### 93. What is the difference between `UNION` and `UNION ALL`?

`UNION` combines result sets and removes duplicate rows. `UNION ALL`
keeps duplicates and is often faster because it avoids duplicate
elimination. Both queries must return the same number of compatible
columns.

### 94. Does SQL have `INTERSECT` and `EXCEPT`?

Support depends on the database/version. These set operators return
common rows (`INTERSECT`) or rows in the first result but not the second
(`EXCEPT`). MySQL versions traditionally lack these operators, so
equivalent joins or `EXISTS`/`NOT EXISTS` patterns are commonly used.

------------------------------------------------------------------------

# 7. Normalization and Database Design

### 95. What is normalization?

Normalization organizes relational data to reduce undesirable redundancy
and prevent insertion, update, and deletion anomalies.

### 96. What is denormalization?

Denormalization intentionally introduces some redundancy or precomputed
data to improve read performance or simplify reporting. It increases
consistency and update complexity.

### 97. What is a database anomaly?

-   **Insertion anomaly:** A fact cannot be inserted without an
    unrelated fact.
-   **Update anomaly:** The same fact must be changed in multiple
    places, risking inconsistency.
-   **Deletion anomaly:** Removing one row unintentionally removes the
    only copy of another fact.

### 98. What is First Normal Form (1NF)?

A relation is in 1NF when each attribute contains a single value from
its domain in each row, rather than repeating groups or multi-valued
lists. "Atomic" depends on the intended domain and design.

### 99. What is Second Normal Form (2NF)?

A relation is in 2NF when it is in 1NF and every non-prime attribute is
fully functionally dependent on every candidate key; there are no
partial dependencies on a proper subset of a candidate key.

### 100. What is Third Normal Form (3NF)?

A relation is in 3NF when it is in 2NF and has no inappropriate
transitive dependency of non-key attributes on candidate keys. Formally,
for every non-trivial functional dependency `X → A`, either `X` is a
super key or `A` is a prime attribute.

### 101. What is BCNF?

Boyce--Codd Normal Form requires every determinant in a non-trivial
functional dependency to be a super key. It is stricter than 3NF.

### 102. What is a functional dependency?

A functional dependency `X → Y` means that whenever two rows agree on
attributes `X`, they must also agree on attributes `Y`.

### 103. What is a partial dependency?

A non-key attribute depends on only part of a composite candidate key.
2NF removes such dependencies.

### 104. What is a transitive dependency?

A dependency where a key determines one attribute, which in turn
determines another non-key attribute, such as `StudentID → DeptID` and
`DeptID → DeptName`.

### 105. What are 4NF and 5NF?

-   **4NF:** Addresses non-trivial multivalued dependencies that are not
    implied by a super key.
-   **5NF:** Addresses join dependencies where a relation can be
    decomposed into smaller relations without loss, under the relevant
    dependency conditions.

For most fresher interviews, know the purpose and basic distinction;
detailed formal theory is more advanced.

### 106. What is lossless decomposition?

A decomposition is lossless if joining the decomposed relations
reconstructs exactly the original relation without spurious rows.

### 107. What is dependency preservation?

A decomposition preserves dependencies when the original constraints can
be enforced on the decomposed relations without needing to join them
back together.

### 108. What is an ER diagram?

An Entity--Relationship diagram models entities, attributes, and
relationships before or during database design.

### 109. What is a weak entity?

In ER modeling, a weak entity cannot be uniquely identified by its own
attributes alone and depends on an identifying relationship with an
owner entity.

------------------------------------------------------------------------

# 8. Transactions and ACID

### 110. What is a transaction?

A transaction is a logical unit of database work that should complete
according to the system's transaction guarantees.

### 111. What are ACID properties?

-   **Atomicity:** All the transaction's work happens, or none of it
    does.
-   **Consistency:** A committed transaction preserves declared database
    rules and application invariants.
-   **Isolation:** Concurrent transactions are controlled so they do not
    interfere in disallowed ways.
-   **Durability:** Once committed, changes survive failures according
    to the database's durability guarantees.

### 112. What is `COMMIT`?

It successfully ends a transaction and makes its changes durable
according to the DBMS guarantees.

### 113. What is `ROLLBACK`?

It undoes uncommitted changes in the current transaction, subject to the
database's transaction semantics.

### 114. What is a `SAVEPOINT`?

A savepoint marks a point inside a transaction so the transaction can
roll back to that point without necessarily discarding all earlier work.

### 115. What is autocommit in MySQL?

With autocommit enabled, each statement that is not already inside an
explicit transaction is generally committed automatically when it
succeeds. Transactional engine and statement behavior still matter.

### 116. Does `ROLLBACK` undo every SQL command?

No. DDL and other statements can cause implicit commits or be
non-transactional. In MySQL, `CREATE`, `ALTER`, `DROP`, and `TRUNCATE`
generally cause implicit commits. Non-transactional table engines may
not support rollback of data changes.

### 117. What is a dirty read?

A transaction reads another transaction's uncommitted changes.

### 118. What is a non-repeatable read?

A transaction reads the same row twice and gets different committed
values because another transaction changed it and committed.

### 119. What is a phantom read?

Repeating a range query returns a different set of rows because another
transaction inserted or deleted rows matching the range, or changed rows
so they match.

### 120. What are transaction isolation levels?

Common SQL isolation levels are: - `READ UNCOMMITTED` -
`READ COMMITTED` - `REPEATABLE READ` - `SERIALIZABLE`

The anomalies prevented and implementation details vary by DBMS. MySQL
InnoDB uses `REPEATABLE READ` by default in typical configurations and
uses MVCC and locking mechanisms.

### 121. What is a deadlock?

A deadlock occurs when transactions wait on each other in a cycle so
none can proceed. InnoDB detects many deadlocks and rolls back a victim
transaction; applications should be prepared to retry safely.

### 122. What is a lock?

A lock coordinates concurrent access to database resources. Examples
include shared/read and exclusive/write locks. Exact lock modes and
granularity depend on the database engine.

### 123. What is MVCC?

Multi-Version Concurrency Control maintains versions of rows so reads
and writes can often proceed concurrently without blocking every reader
and writer. MySQL InnoDB uses MVCC.

### 124. What is the difference between optimistic and pessimistic concurrency?

-   **Pessimistic:** Locks resources early to prevent conflicting work.
-   **Optimistic:** Allows work to proceed and detects conflicts when
    validating or committing changes.

------------------------------------------------------------------------

# 9. Indexes and Query Performance

### 125. What is an index?

An index is a data structure that helps the database find rows without
scanning the entire table. It improves some reads but consumes storage
and adds write/maintenance overhead.

### 126. What are the advantages of indexes?

-   Faster lookups, filtering, and joins when an appropriate index can
    be used.
-   Can help `ORDER BY`, grouping, and uniqueness enforcement.
-   Can reduce the amount of data examined.

### 127. What are the disadvantages of indexes?

-   Consume disk and memory.
-   Slow down inserts, updates, and deletes because indexes must be
    maintained.
-   Too many or poorly chosen indexes can harm performance.
-   The optimizer may choose not to use an index if a scan is cheaper.

### 128. What is a clustered index?

A clustered index determines how table rows are organized by the index
key in storage. InnoDB organizes table data by the primary key in its
clustered index; if no primary key exists, InnoDB selects an appropriate
unique non-null key or creates an internal row ID.

### 129. What is a secondary index in InnoDB?

A secondary index is a separate index structure. Its leaf records
include the indexed columns and the primary-key columns used to locate
the full row.

### 130. Can a table have multiple clustered indexes?

InnoDB has one clustered organization per table, so it cannot have
multiple independent clustered indexes. It can have many secondary
indexes.

### 131. What is a composite index?

An index over multiple columns, such as `(DeptID, Salary)`. Column order
matters.

### 132. What is the leftmost-prefix rule?

For a composite B-tree index `(A, B, C)`, queries that constrain a
leftmost prefix---such as `A`, `(A,B)`, or `(A,B,C)`---can generally use
the index efficiently. A condition on `B` alone usually cannot use it as
effectively for lookup, though optimizer features and index types can
change details.

### 133. What is a unique index?

An index that prevents duplicate indexed key values, subject to the
DBMS's `NULL` rules.

### 134. What is a covering index?

An index that contains all columns needed by a query, allowing the
engine to answer it from the index without fetching the full table row
in applicable cases.

### 135. What is a full-text index?

An index designed for searching words and text content, with supported
search modes and tokenization rules. MySQL supports full-text indexes
for supported storage engines and column types.

### 136. What is a prefix index?

An index on only the first N characters/bytes of a string column. It can
save space but may be less selective and cannot always satisfy
full-column operations.

### 137. What is `EXPLAIN`?

`EXPLAIN` shows the optimizer's planned approach to executing a query,
including access paths and join order. MySQL also supports
`EXPLAIN ANALYZE` in modern versions to execute a query and report
actual execution measurements.

### 138. Why might MySQL not use an index?

Possible reasons include: - The predicate matches a large fraction of
rows. - A function or expression is applied to an indexed column in a
way that prevents ordinary index lookup. - Data types or collations
cause implicit conversions. - The index is not selective or does not
match the leftmost prefix. - Table statistics or cost estimates favor a
table scan.

### 139. What is a sargable predicate?

A predicate that can be used effectively by an index access method. For
example, `HireDate >= '2025-01-01'` is often more index-friendly than
`YEAR(HireDate) = 2025`.

### 140. How can SQL query performance be improved?

-   Inspect the query plan using `EXPLAIN`.
-   Index columns used in selective filters and joins when justified.
-   Select only required columns instead of `SELECT *`.
-   Avoid unnecessary functions on indexed columns.
-   Use suitable join conditions and data types.
-   Limit returned rows when appropriate.
-   Measure with realistic data; do not assume an index always helps.

------------------------------------------------------------------------

# 10. Storage Engines and MySQL Architecture

### 141. What is a storage engine?

A storage engine determines how MySQL stores, indexes, locks, and
retrieves table data.

### 142. What is InnoDB?

InnoDB is MySQL's default general-purpose transactional storage engine
in modern releases. It supports transactions, row-level locking, foreign
keys, crash recovery, and MVCC.

### 143. What is MyISAM?

MyISAM is an older MySQL storage engine. It does not provide
InnoDB-style transactions or foreign-key enforcement and traditionally
uses table-level locking. It may still appear in legacy systems.

### 144. InnoDB vs MyISAM

  -----------------------------------------------------------------------
  InnoDB                              MyISAM
  ----------------------------------- -----------------------------------
  Supports transactions and ACID      No transaction support comparable
  behavior                            to InnoDB

  Supports foreign keys               Does not enforce foreign keys

  Row-level locking is available      Traditionally table-level locking

  Crash recovery support              Weaker crash-recovery guarantees

  Default for modern MySQL tables     Legacy/limited use cases
  -----------------------------------------------------------------------

### 145. What is the MySQL query optimizer?

The optimizer chooses an execution plan, such as join order, access
method, and index usage, based on query semantics, statistics, and cost
estimates.

### 146. What is a query execution plan?

It describes how the database expects to access tables, use indexes,
join rows, and process operations to produce a result.

### 147. What is a buffer pool?

In InnoDB, the buffer pool is a memory area used to cache table and
index pages, reducing disk I/O for frequently accessed data.

### 148. What is the redo log?

The InnoDB redo log records changes needed to recover committed or
in-progress work after a crash. It is central to durability and
recovery.

### 149. What is the undo log?

The undo log stores information used to roll back changes and support
consistent reads of older row versions under MVCC.

### 150. What is the binary log?

The MySQL binary log records database changes/events for purposes such
as replication and point-in-time recovery, depending on configuration
and logging format. It is distinct from the InnoDB redo log.

### 151. Redo log vs undo log vs binary log

  -----------------------------------------------------------------------
  Log                                 Main purpose
  ----------------------------------- -----------------------------------
  Redo log                            Crash recovery by reapplying logged
                                      changes as needed

  Undo log                            Rollback and older row versions for
                                      consistent reads

  Binary log                          Replication and point-in-time
                                      recovery of logged database changes
  -----------------------------------------------------------------------

### 152. What is replication?

Replication copies changes from a source server to one or more replica
servers. It can support read scaling, availability, and recovery
architectures, but replication lag and failover design matter.

### 153. What is partitioning?

Partitioning divides a table into smaller physical partitions according
to a rule such as range, list, hash, or key. It is not the same as
sharding, and it does not automatically make every query faster.

### 154. What is sharding?

Sharding distributes rows across separate database servers or
independent database instances. It can increase horizontal capacity but
adds complexity to queries, transactions, rebalancing, and operations.

### 155. Partitioning vs sharding

Partitioning usually divides a table within one database system;
sharding distributes data across separate database instances or servers.
Terminology varies, but sharding normally implies horizontal
distribution across nodes.

------------------------------------------------------------------------

# 11. Stored Programs: Procedures, Functions, Triggers, and Events

### 156. What is a stored procedure?

A stored procedure is a named set of SQL and procedural statements
stored in the database and invoked using `CALL` in MySQL.

### 157. What is a stored function?

A stored function returns a value and can be used in expression contexts
where permitted. It has restrictions that differ from stored procedures.

### 158. Stored procedure vs stored function

  -----------------------------------------------------------------------
  Stored procedure                    Stored function
  ----------------------------------- -----------------------------------
  Invoked using `CALL` in MySQL       Used as an expression where allowed

  Can return result sets and use      Returns a value with `RETURN`
  OUT/INOUT parameters                

  Suitable for multi-step operations  Suitable for reusable value
                                      calculations

  Restrictions differ by context      Restrictions apply to side effects
                                      and statements
  -----------------------------------------------------------------------

### 159. What is a trigger?

A trigger is database code automatically executed in response to a
specified table event, such as `INSERT`, `UPDATE`, or `DELETE`.

### 160. What are `BEFORE` and `AFTER` triggers?

A `BEFORE` trigger executes before the triggering row operation; an
`AFTER` trigger executes after it. Exact capabilities depend on the
event and database. MySQL supports row-level triggers, not
statement-level triggers.

### 161. What is an event in MySQL?

A scheduled event is a database task that runs at a specified time or
interval when the MySQL Event Scheduler is enabled.

### 162. What is a cursor?

A cursor processes a query result row by row in stored-program code.
Cursors can be useful for tasks requiring sequential processing but are
often slower and less concise than set-based SQL.

### 163. What is dynamic SQL?

Dynamic SQL is SQL assembled and executed at runtime. It is useful when
object names or query structure must vary, but values should be bound
with prepared statements to reduce SQL injection risk.

------------------------------------------------------------------------

# 12. Views, Temporary Tables, and Table Types

### 164. What is a temporary table?

A temporary table stores intermediate data for a limited session or
transaction scope, depending on the database. MySQL temporary tables are
visible to the creating session and are automatically dropped when the
session ends.

### 165. Temporary table vs view

  -----------------------------------------------------------------------
  Temporary table                     View
  ----------------------------------- -----------------------------------
  Stores rows in a temporary table    Defines a query
  object                              

  Can be populated and modified       Reads from underlying objects when
  subject to rules                    queried

  Lifetime is limited                 Definition persists until dropped

  Useful for intermediate results     Useful for abstraction and reusable
                                      queries
  -----------------------------------------------------------------------

### 166. What is a derived table?

A derived table is a subquery in the `FROM` clause, treated as a table
for that query.

### 167. What is a table-valued function?

A function that returns a table-like result. Availability and syntax
depend on the DBMS; MySQL does not provide table-valued functions in the
same style as SQL Server.

------------------------------------------------------------------------

# 13. Security and SQL Injection

### 168. What is SQL injection?

SQL injection is a vulnerability where untrusted input changes the
intended SQL command structure, potentially allowing unauthorized reads
or changes.

### 169. How do you prevent SQL injection?

-   Use parameterized queries/prepared statements.
-   Do not build SQL by concatenating untrusted values.
-   Validate inputs and allow-list identifiers where dynamic
    table/column names are required.
-   Apply least-privilege database permissions.
-   Avoid exposing database errors or credentials to users.

### 170. What is a prepared statement?

A prepared statement separates SQL structure from parameter values. The
database/driver binds values safely rather than interpreting them as SQL
syntax.

### 171. What is the principle of least privilege?

Give each database user only the permissions required for their role. An
application account that only reads certain tables should not have
unnecessary `DROP`, `ALTER`, or broad administrative privileges.

### 172. What is a database role?

A role is a named collection of privileges that can be granted to users,
making permission management easier.

### 173. Why should passwords not be stored as plain text in a database?

A breach would expose passwords directly. Applications should store
salted, slow password hashes using a password-hashing algorithm such as
Argon2id or bcrypt, not reversible encryption or plain text.

------------------------------------------------------------------------

# 14. MySQL Transactions, Users, and Practical Administration

### 174. What is a database user in MySQL?

A MySQL account is identified by a user name and host component, such as
`'appuser'@'localhost'`. Permissions are associated with the account and
its roles.

### 175. What is `SHOW DATABASES`?

It lists databases visible to the current account according to its
privileges.

### 176. What is `SHOW TABLES`?

It lists tables and, depending on context, other table-like objects
visible in the selected database.

### 177. What is `DESCRIBE` / `DESC`?

It displays column information for a table, including data types,
nullability, key information, defaults, and extra attributes.

### 178. What is `USE database_name`?

It selects the default database for subsequent statements in the current
session.

### 179. What is `INFORMATION_SCHEMA`?

It is a set of metadata tables/views that provide information about
databases, tables, columns, constraints, and other objects. Access and
exact contents depend on the MySQL version and privileges.

### 180. What is a backup?

A backup is a recoverable copy of data and relevant database objects.
Backups should be tested through restoration, not merely assumed valid
because the backup command succeeded.

### 181. What is point-in-time recovery?

It restores a backup and replays logged changes up to a chosen time or
position, commonly using the MySQL binary log when properly configured.

------------------------------------------------------------------------

# 15. SQL NULL Logic and Common Traps

### 182. Why does `column = NULL` not work?

SQL uses three-valued logic: `TRUE`, `FALSE`, and `UNKNOWN`. Comparisons
involving `NULL` generally produce `UNKNOWN`, so use `IS NULL` or
`IS NOT NULL`.

### 183. What is three-valued logic?

Conditions can evaluate to `TRUE`, `FALSE`, or `UNKNOWN` because of
`NULL`. In `WHERE`, only rows whose condition evaluates to `TRUE` are
retained.

### 184. What is the difference between `COALESCE()` and `IFNULL()`?

Both can replace a `NULL` with another value. `COALESCE()` is standard
SQL and accepts multiple arguments, returning the first non-`NULL`
value. `IFNULL()` is MySQL-specific and takes two arguments.

### 185. What is `NULLIF()`?

`NULLIF(a, b)` returns `NULL` if `a = b`; otherwise it returns `a`. It
can help avoid division by zero, for example
`numerator / NULLIF(denominator, 0)`.

### 186. Why can `NOT IN` behave unexpectedly with NULL?

If the set contains `NULL`, the membership comparison can become
`UNKNOWN` rather than `TRUE`, causing rows to be filtered out.
`NOT EXISTS` is often a safer anti-join pattern.

### 187. Does `COUNT(column)` count NULLs?

No. It counts only non-`NULL` values. `COUNT(*)` counts rows.

### 188. Does `AVG(column)` include NULL as zero?

No. `AVG()` ignores `NULL` values; it does not treat them as zero. If
zero is the intended meaning, express that explicitly with a suitable
expression and understand the effect on the average.

------------------------------------------------------------------------

# 16. Advanced Concepts Frequently Asked

### 189. What is a window function?

A window function calculates a value across a set of related rows while
preserving individual rows in the result. Examples include
`ROW_NUMBER()`, `RANK()`, `LAG()`, and `SUM() OVER (...)`.

### 190. Aggregate function vs window function

  ------------------------------------------------------------------------------
  Aggregate                           Window function
  ----------------------------------- ------------------------------------------
  Often returns one row per group     Usually preserves each input row
  when used with `GROUP BY`           

  Example:                            Example:
  `AVG(Salary) GROUP BY DeptID`       `AVG(Salary) OVER (PARTITION BY DeptID)`
  ------------------------------------------------------------------------------

### 191. What does `PARTITION BY` do?

It divides rows into independent groups for a window function. It does
not itself collapse rows like `GROUP BY`.

### 192. What does the `OVER()` clause do?

It defines the window over which a window function operates, including
optional partitioning, ordering, and frame boundaries.

### 193. Difference between `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`

-   `ROW_NUMBER()`: assigns a unique sequence number to every row.
-   `RANK()`: ties share a rank and later ranks have gaps.
-   `DENSE_RANK()`: ties share a rank but later ranks have no gaps.

### 194. What do `LAG()` and `LEAD()` do?

They access a value from a previous row (`LAG`) or a following row
(`LEAD`) in the ordered window, useful for change detection and
comparisons across time.

### 195. What is a window frame?

It defines which rows around the current row contribute to a window
calculation, such as all prior rows through the current row. Explicit
frames are important for running totals and related calculations.

### 196. What is a recursive query useful for?

It traverses hierarchical or graph-like relationships, such as employee
reporting chains, category trees, or parent-child structures.

### 197. What is a generated column in MySQL?

A generated column derives its value from an expression. It can be
`VIRTUAL` or `STORED`; indexing options and restrictions depend on the
expression and MySQL version.

### 198. What is an upsert?

An upsert inserts a row if it does not exist and updates or otherwise
handles it if a uniqueness conflict occurs. MySQL commonly uses
`INSERT ... ON DUPLICATE KEY UPDATE`; syntax differs across database
systems.

### 199. What is optimistic locking with a version column?

A row stores a version number that is checked during update. The update
succeeds only if the version still matches the value previously read,
helping detect concurrent changes.

### 200. What is idempotency in database operations?

An operation is idempotent if repeating it has the same effect as
performing it once. Idempotent application design is valuable for
retries, payment processing, and distributed systems; not every SQL
statement is idempotent.

------------------------------------------------------------------------

# 17. Differences to Memorize

  -----------------------------------------------------------------------
  Concept A               Concept B               Key difference
  ----------------------- ----------------------- -----------------------
  SQL                     MySQL                   Language vs database
                                                  system

  DBMS                    RDBMS                   General database
                                                  software vs relational
                                                  database system

  Primary key             Foreign key             Identifies a row vs
                                                  references a key in
                                                  another table

  Primary key             UNIQUE                  Main row identifier, no
                                                  NULL vs uniqueness
                                                  constraint with
                                                  DBMS-specific NULL
                                                  rules

  `DELETE`                `TRUNCATE`              Row deletion, optional
                                                  filter vs remove all
                                                  rows

  `TRUNCATE`              `DROP`                  Keeps table structure
                                                  vs removes the table

  `WHERE`                 `HAVING`                Filters rows vs filters
                                                  groups

  `GROUP BY`              `ORDER BY`              Groups rows vs sorts
                                                  rows

  `UNION`                 `UNION ALL`             Removes duplicates vs
                                                  keeps duplicates

  `INNER JOIN`            `LEFT JOIN`             Only matches vs all
                                                  left rows plus matches

  `IN`                    `EXISTS`                Membership test vs
                                                  row-existence test

  `NOT IN`                `NOT EXISTS`            Can be affected by NULL
                                                  in the set vs
                                                  correlated existence
                                                  logic

  Procedure               Function                Invoked as a procedure
                                                  vs returns a value for
                                                  expression use

  Trigger                 Event                   Runs in response to
                                                  table event vs
                                                  scheduled task

  View                    Temporary table         Stored query definition
                                                  vs temporary stored
                                                  rows

  `CHAR`                  `VARCHAR`               Fixed-width semantics
                                                  vs variable-length

  `DECIMAL`               `FLOAT`                 Exact decimal
                                                  arithmetic within
                                                  defined precision vs
                                                  approximate binary
                                                  floating point

  Redo log                Undo log                Recovery of changes vs
                                                  rollback/older versions

  Redo log                Binary log              InnoDB crash recovery
                                                  vs replication/PITR log

  Partitioning            Sharding                Data divided into
                                                  partitions vs
                                                  distributed across
                                                  database nodes

  Normalization           Denormalization         Reduce
                                                  redundancy/anomalies vs
                                                  intentionally add
                                                  redundancy for a
                                                  purpose

  Clustered index         Secondary index         Organizes table data in
                                                  InnoDB vs separate
                                                  lookup structure

  `ROW_NUMBER()`          `DENSE_RANK()`          Unique row sequence vs
                                                  shared rank for ties
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 18. Rapid-Fire Interview Questions

### 201. Can a primary key be NULL?

No.

### 202. Can a table have more than one foreign key?

Yes. A table can have multiple foreign-key constraints.

### 203. Can a foreign key reference a column that is not unique?

A referenced key generally must be eligible for reference, typically a
primary or unique key. MySQL/InnoDB has had non-standard behavior around
referenced indexes; design foreign keys against primary or unique keys
for portable, reliable schemas.

### 204. Does `ORDER BY` guarantee order without an explicit direction?

Yes, the sort expression is applied, but direction defaults to ascending
where omitted. Without `ORDER BY`, no result order is guaranteed.

### 205. Is `BETWEEN` inclusive?

Yes, its endpoints are included. For timestamp ranges, a half-open range
(`>= start AND < next_period`) is often safer.

### 206. Does `COUNT(*)` count duplicate rows?

Yes, it counts every result row. It does not deduplicate unless the
query uses `DISTINCT` or grouping changes the result.

### 207. Can `GROUP BY` be used without aggregate functions?

Yes. It forms groups, though if only distinct values are needed,
`SELECT DISTINCT` may communicate intent more clearly.

### 208. Can we use an aggregate function in `WHERE`?

Not directly in ordinary query structure; use `HAVING` for aggregate
group conditions or a subquery/window-function approach.

### 209. What is referential integrity?

It ensures relationships expressed by foreign keys remain valid.

### 210. What is a transaction rollback?

It reverses uncommitted transactional changes, within the capabilities
of the storage engine and statements used.

### 211. What is an index scan?

An access method that reads index entries to locate or return data. It
may be efficient or expensive depending on how many entries must be
scanned.

### 212. What is a full table scan?

The database reads the table's rows rather than using a selective index
lookup. It can be appropriate when most rows are needed.

### 213. What is a deadlock victim?

A transaction chosen by the database to roll back so that a deadlock
cycle can be broken.

### 214. What is a primary-key index in InnoDB?

The clustered index that organizes the table data by the primary key.

### 215. What is the purpose of `EXPLAIN ANALYZE`?

It executes a query and reports actual runtime information alongside
plan details in supported MySQL versions. Use caution with expensive
queries because it really runs them.

### 216. What is a database migration?

A controlled, versioned change to database schema or data, often tracked
as scripts and applied consistently across environments.

### 217. What is connection pooling?

Reusing a managed pool of database connections instead of opening a new
connection for every request, reducing overhead and helping control
concurrency.

### 218. What is a transaction boundary?

The start and end of the set of operations that must succeed or fail
together.

### 219. What is eventual consistency?

A consistency model in which replicas may temporarily disagree but
converge if updates stop and replication proceeds. It is relevant to
distributed databases and replicated systems.

### 220. What is a database deadlock retry strategy?

Catch the appropriate transient error, roll back or let the failed
transaction end, and retry the whole logical transaction with bounded
retries and possibly backoff. Ensure the operation is safe to retry.

------------------------------------------------------------------------

# 19. How to Prepare These Topics for an Interview

## Priority 1 --- Must know

-   SQL vs MySQL; DBMS vs RDBMS
-   DDL, DML, DQL, DCL, TCL
-   Primary, foreign, candidate, composite, and unique keys
-   Constraints and `NULL`
-   `DELETE` vs `TRUNCATE` vs `DROP`
-   `WHERE` vs `HAVING`
-   Joins and `UNION` vs `UNION ALL`
-   Aggregate functions and subqueries
-   Normalization: 1NF, 2NF, 3NF, BCNF
-   ACID, transactions, `COMMIT`, `ROLLBACK`
-   Indexes and `EXPLAIN`
-   `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`

## Priority 2 --- Strong advantage

-   Correlated subqueries, `EXISTS`, `NOT EXISTS`
-   CTEs and recursive CTEs
-   Window frames, `LAG()`, `LEAD()`
-   InnoDB vs MyISAM
-   Redo, undo, and binary logs
-   Isolation levels, locks, deadlocks, MVCC
-   Views, procedures, functions, triggers, events
-   Query optimization and composite-index ordering

## Priority 3 --- Advanced / role-dependent

-   4NF and 5NF
-   Partitioning and sharding
-   Replication and point-in-time recovery
-   Generated columns, upserts, optimistic locking
-   Connection pooling, migrations, eventual consistency

## Final advice

For every topic, prepare four things: 1. **Definition** --- explain it
in one or two sentences. 2. **Purpose** --- why it exists and when it is
used. 3. **Example** --- give a small real-world example or query. 4.
**Difference/trap** --- know the closest related concept and the common
misconception.

This file focuses on theory. Practise query-writing separately,
especially joins, aggregate queries, subqueries, and window functions.
SQL behavior can differ across DBMS products and versions, so mention
the database when an answer depends on MySQL-specific syntax or
behavior.
