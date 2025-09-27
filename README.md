# ORACLE_NOTES_2


# SECTION-A (20 Marks)

### 1. Define Normalization
- Normalization is the process of organizing data in a database.  
- It reduces redundancy and improves data integrity.  
- Data is divided into smaller, related tables.  
- Ensures dependencies are logical.  
- Helps in efficient database design.  

---

### 2. Write any two commands of data definition language
- **CREATE** → Used to create database objects like tables, views, indexes.  
- **ALTER** → Used to modify existing database objects.  
- **DROP** → Deletes existing objects from the database.  
- DDL commands are auto-committed.  
- They define the structure of the database.  

---

### 3. Write a note on functions
- A function is a named PL/SQL block that returns a single value.  
- It is used to perform calculations or operations.  
- Can accept input parameters.  
- Always returns a value using the `RETURN` statement.  
- Example: `CREATE FUNCTION ... RETURN datatype`.  

---

### 4. Define subqueries
- A subquery is a query inside another SQL query.  
- It is written within parentheses.  
- Used to return intermediate results.  
- Can be nested inside `SELECT`, `INSERT`, `UPDATE`, or `DELETE`.  
- Example: `SELECT * FROM emp WHERE deptno IN (SELECT deptno FROM dept);`.  

---

### 5. Write any two concepts of locks
- **Shared Lock** → Allows multiple users to read but not modify data.  
- **Exclusive Lock** → Prevents other users from reading or writing data.  
- Locks ensure data consistency during transactions.  
- They prevent simultaneous conflicting operations.  
- Oracle automatically manages locks.  

---

### 6. How to insert records into a partitioned table?
- Partitioned tables are divided into smaller segments.  
- Records are inserted using normal `INSERT` statements.  
- Oracle decides the partition based on partition key.  
- Example: `INSERT INTO sales VALUES (...);`.  
- Data is stored in the correct partition automatically.  

---

### 7. Define view
- A view is a virtual table based on a query.  
- It does not store data itself.  
- Provides a customized way of looking at data.  
- Useful for security and simplicity.  
- Example: `CREATE VIEW emp_view AS SELECT ename, sal FROM emp;`.  

---

### 8. Define control structure
- Control structures are used to control the flow of PL/SQL programs.  
- They allow conditional and iterative execution.  
- Types: Conditional (`IF`), Iterative (`LOOP`, `WHILE`, `FOR`).  
- Help in decision-making in programs.  
- Provide flexibility in coding.  

---

### 9. What do you mean by stored procedures?
- A stored procedure is a named PL/SQL block stored in the database.  
- It can perform one or more actions.  
- May accept input and output parameters.  
- Improves reusability and performance.  
- Example: `CREATE PROCEDURE proc_name IS ... END;`.  

---

### 10. Write syntax for creating trigger
```sql
CREATE [OR REPLACE] TRIGGER trigger_name
BEFORE | AFTER | INSTEAD OF
{INSERT | UPDATE | DELETE} ON table_name
[FOR EACH ROW]
DECLARE
   -- variable declarations
BEGIN
   -- trigger logic
END;
```

---



# SECTION - B (25 Marks)

### 11(a) Describe about relational database system
- **Definition**:  
  A Relational Database System (RDBMS) is a database system where data is stored in tables (relations) consisting of rows and columns.  

- **Theory**:  
  - Developed based on E.F. Codd’s relational model.  
  - Data is represented as tuples (rows) and attributes (columns).  
  - Ensures **data integrity** using keys and constraints.  
  - Provides support for SQL as a standard query language.  
  - Examples: Oracle, MySQL, PostgreSQL.  

- **Key Features**:  
  - Data stored in **tables (relations)**.  
  - **Primary Keys** uniquely identify records.  
  - **Foreign Keys** establish relationships between tables.  
  - Support for **normalization** to remove redundancy.  
  - Ensure **ACID properties** in transactions.  

---

### 11(b) Write a note on data manipulation language
- **Definition**:  
  DML (Data Manipulation Language) is used to manipulate and process data stored in database tables.  

- **Types of DML Commands**:  
  - **INSERT** → Adds new rows.  
  - **UPDATE** → Modifies existing data.  
  - **DELETE** → Removes data.  
  - **MERGE** → Inserts or updates based on condition.  

- **Syntax Example**:  
  ```sql
  INSERT INTO employee (id, name, salary) VALUES (101, 'Arun', 50000);
  UPDATE employee SET salary = 60000 WHERE id = 101;
  DELETE FROM employee WHERE id = 101;
  ```

* **Explanation**:

  * DML does not change structure, only data.
  * Supports **transaction control** (`COMMIT`, `ROLLBACK`).
  * Ensures flexibility in managing database contents.

---

### 12(a) Differentiate UNION and UNION ALL set operations

* **Definition**:
  Both `UNION` and `UNION ALL` are used to combine results from multiple queries.

* **Theory**:

  * **UNION** → Combines results and removes duplicates.
  * **UNION ALL** → Combines results but keeps duplicates.
  * Both require same number of columns and compatible data types.

* **Syntax Example**:

  ```sql
  SELECT name FROM emp WHERE deptno=10
  UNION
  SELECT name FROM emp WHERE deptno=20;

  SELECT name FROM emp WHERE deptno=10
  UNION ALL
  SELECT name FROM emp WHERE deptno=20;
  ```

* **Difference Table**:

  | Feature     | UNION                   | UNION ALL             |
  | ----------- | ----------------------- | --------------------- |
  | Duplicates  | Removed automatically   | Retained              |
  | Performance | Slower (extra work)     | Faster                |
  | Usage       | When unique result req. | When all results req. |

---

### 12(b) Explain correlated subquery

* **Definition**:
  A correlated subquery is a subquery that references a column from the outer query.

* **Theory**:

  * Executed **once for each row** in the outer query.
  * Dependent on values of outer query row.
  * Used for row-by-row comparison.

* **Syntax Example**:

  ```sql
  SELECT e1.name, e1.salary
  FROM employee e1
  WHERE salary > (SELECT AVG(salary)
                  FROM employee e2
                  WHERE e1.deptno = e2.deptno);
  ```

* **Explanation**:

  * In this example, each employee’s salary is compared with average salary of their department.
  * Subquery depends on outer query’s `deptno`.
  * More powerful but less efficient than simple subqueries.

---

### 13(a) Explain in detail about types of locks

* **Definition**:
  Locks are mechanisms to control concurrent access to data.

* **Theory**:

  * Ensure **data consistency** and **isolation** in transactions.
  * Prevent conflicts like **lost updates** and **dirty reads**.

* **Types of Locks in Oracle**:

  1. **Shared Lock** → Multiple users can read, but no updates allowed.
  2. **Exclusive Lock** → Only one user can read/write at a time.
  3. **Row-level Lock** → Lock only one row; supports high concurrency.
  4. **Table-level Lock** → Locks whole table; less concurrency.
  5. **Deadlock** → Situation where two sessions wait for each other’s lock.

* **Example**:

  ```sql
  SELECT * FROM employee FOR UPDATE;
  ```

  → Places a row-level exclusive lock.

---

### 13(b) Write a note on advantages of table partitions

* **Definition**:
  Partitioning divides a large table into smaller, manageable pieces called partitions.

* **Advantages**:

  * **Improved Performance** → Queries access only required partitions.
  * **Easier Maintenance** → Can backup, load, or drop partitions individually.
  * **Data Distribution** → Helps in managing very large datasets.
  * **Parallelism** → Different partitions processed in parallel.
  * **Availability** → Partition failure doesn’t affect entire table.

* **Example**:

  ```sql
  CREATE TABLE sales
  (id INT, sale_date DATE, amount NUMBER)
  PARTITION BY RANGE (sale_date)
  (PARTITION p1 VALUES LESS THAN (TO_DATE('01-01-2023','DD-MM-YYYY')),
   PARTITION p2 VALUES LESS THAN (TO_DATE('01-01-2024','DD-MM-YYYY')));
  ```

---

### 14(a) Describe about partitioning in Index

* **Definition**:
  Index partitioning divides a large index into smaller sub-indexes.

* **Theory**:

  * Works with partitioned tables.
  * Each partition corresponds to a table partition.
  * Improves performance of searches and maintenance.

* **Types**:

  * **Local Partitioned Index** → Each partition index matches table partition.
  * **Global Partitioned Index** → Partitioning independent of table.

* **Example**:

  ```sql
  CREATE INDEX idx_sales_date ON sales(sale_date)
  LOCAL;
  ```

* **Benefits**:

  * Faster query performance.
  * Better manageability of large datasets.
  * Supports parallelism in searches.

---

### 14(b) Write a note on PL/SQL data types

* **Definition**:
  PL/SQL supports various data types for variables and constants.

* **Categories**:

  1. **Scalar Types** → `NUMBER`, `VARCHAR2`, `DATE`, `BOOLEAN`.
  2. **Composite Types** → `RECORD`, `TABLE`, `VARRAY`.
  3. **Reference Types** → `REF CURSOR`, pointers to objects.
  4. **LOB Types** → `CLOB`, `BLOB` for large objects.

* **Example**:

  ```sql
  DECLARE
     emp_name VARCHAR2(30);
     emp_salary NUMBER(10,2);
  BEGIN
     emp_name := 'Arun';
     emp_salary := 50000;
  END;
  ```

* **Explanation**:

  * Each data type serves a different purpose.
  * Ensures correct storage and operations on data.

---

### 15(a) What do you mean by purity of functions?

* **Definition**:
  Purity of functions refers to whether a PL/SQL function can be safely called from SQL statements without side effects.

* **Theory**:

  * Pure functions should not modify database state.
  * Should not use **INSERT, UPDATE, DELETE** inside.
  * Deterministic → Same input, same output.

* **Example**:

  ```sql
  CREATE FUNCTION get_bonus (salary NUMBER)
  RETURN NUMBER DETERMINISTIC IS
  BEGIN
     RETURN salary * 0.1;
  END;
  ```

* **Explanation**:

  * `DETERMINISTIC` keyword specifies purity.
  * Helps Oracle in query optimization.

---

### 15(b) Describe about enabling and disabling triggers

* **Definition**:
  Triggers can be enabled or disabled as required to control automatic execution.

* **Theory**:

  * **Enabled Trigger** → Fires automatically on specified event.
  * **Disabled Trigger** → Exists in DB but does not fire.
  * Useful in data loading or maintenance to avoid unwanted actions.

* **Syntax**:

  ```sql
  ALTER TRIGGER trigger_name ENABLE;
  ALTER TRIGGER trigger_name DISABLE;

  ALTER TABLE table_name ENABLE ALL TRIGGERS;
  ALTER TABLE table_name DISABLE ALL TRIGGERS;
  ```

* **Explanation**:

  * Helps maintain flexibility in database operations.
  * Reduces overhead when bulk inserting or updating data.

---

