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


# SECTION - C (30 Marks)

### 16. Describe about Data Definition Language (DDL)
- **Definition**:  
  Data Definition Language (DDL) is a set of SQL commands used to define, create, modify, and delete database structures such as tables, indexes, views, and schemas.  
  It is responsible for the **structure and schema** of the database rather than the data itself.  

- **Theory**:  
  - DDL commands are **auto-committed**, meaning changes are permanent.  
  - They deal with the **logical structure** of the database.  
  - DDL is used by database administrators and designers.  

- **Main Commands**:  
  1. **CREATE** → Creates new database objects.  
  2. **ALTER** → Modifies existing objects.  
  3. **DROP** → Removes objects permanently.  
  4. **TRUNCATE** → Removes all rows from a table, but keeps structure.  
  5. **RENAME** → Changes the name of a database object.  

- **Syntax & Example**:  
  ```sql
  CREATE TABLE Employee (
     emp_id NUMBER PRIMARY KEY,
     emp_name VARCHAR2(50),
     salary NUMBER(10,2),
     dept_id NUMBER
  );

  ALTER TABLE Employee ADD (email VARCHAR2(100));
  DROP TABLE Employee;
  ```

* **Explanation**:

  * `CREATE` builds the initial structure.
  * `ALTER` allows schema evolution without data loss.
  * `DROP` permanently removes objects.
  * `TRUNCATE` is faster than `DELETE` since it does not log each row.

* **Conclusion**:
  DDL forms the **foundation of database design** and is crucial for defining how data is stored and accessed.

---

### 17. What is a Join? Explain types of it.

* **Definition**:
  A **JOIN** is an SQL operation used to combine rows from two or more tables based on a related column between them.

* **Theory**:

  * Joins are essential for relational databases because data is spread across multiple tables.
  * They help retrieve **meaningful information** by combining related datasets.

* **Types of Joins in SQL**:

  1. **INNER JOIN** → Returns only matching rows from both tables.
  2. **LEFT OUTER JOIN** → Returns all rows from left table and matching rows from right table.
  3. **RIGHT OUTER JOIN** → Returns all rows from right table and matching rows from left table.
  4. **FULL OUTER JOIN** → Returns all rows when there is a match in one of the tables.
  5. **CROSS JOIN** → Cartesian product of two tables (all combinations).
  6. **SELF JOIN** → Join a table with itself.
  7. **NATURAL JOIN** → Joins automatically on columns with the same name.

* **Syntax & Examples**:

  ```sql
  -- INNER JOIN
  SELECT e.emp_name, d.dept_name
  FROM employee e
  INNER JOIN department d
  ON e.dept_id = d.dept_id;

  -- LEFT JOIN
  SELECT e.emp_name, d.dept_name
  FROM employee e
  LEFT JOIN department d
  ON e.dept_id = d.dept_id;
  ```

* **Explanation**:

  * `INNER JOIN` filters unmatched rows.
  * `OUTER JOINs` are useful when you want to preserve all rows from one side.
  * `CROSS JOIN` generates large outputs but rarely used.
  * `SELF JOIN` is useful for hierarchical data (e.g., employees reporting to managers).

* **Conclusion**:
  Joins are fundamental in SQL for combining related data across tables, supporting relational database principles.

---

### 18. Explain concept and advantages of table partitions

* **Definition**:
  Table partitioning is the process of dividing a large table into smaller, more manageable pieces called **partitions**, while still treating them as a single logical table.

* **Theory**:

  * Each partition can store a subset of data.
  * Queries automatically target relevant partitions, improving performance.
  * Useful for very large datasets such as banking, sales, or log data.

* **Types of Partitioning**:

  1. **Range Partitioning** → Data divided by ranges of values.
  2. **List Partitioning** → Based on discrete values (e.g., regions).
  3. **Hash Partitioning** → Based on a hash function for even distribution.
  4. **Composite Partitioning** → Combination of two partition methods.

* **Syntax Example**:

  ```sql
  CREATE TABLE Sales (
     sale_id NUMBER,
     sale_date DATE,
     amount NUMBER
  )
  PARTITION BY RANGE (sale_date)
  (PARTITION p2023 VALUES LESS THAN (TO_DATE('01-JAN-2024','DD-MON-YYYY')),
   PARTITION p2024 VALUES LESS THAN (TO_DATE('01-JAN-2025','DD-MON-YYYY')));
  ```

* **Advantages**:

  * **Performance** → Queries scan fewer rows (partition pruning).
  * **Manageability** → Easy to backup, load, or drop specific partitions.
  * **Availability** → Partition failures don’t impact the entire table.
  * **Parallelism** → Different partitions can be processed concurrently.
  * **Scalability** → Supports handling of very large databases.

* **Conclusion**:
  Partitioning is a powerful feature in Oracle SQL that improves **query speed, data management, and scalability**, making it essential for big data systems.

---

### 19. Describe about concepts and features of Object-Oriented Programming (OOP)

* **Definition**:
  Object-Oriented Programming (OOP) is a programming paradigm based on the concept of **objects**, which combine data and behavior into a single unit.

* **Core Concepts**:

  1. **Class** → Blueprint for creating objects.
  2. **Object** → Instance of a class.
  3. **Encapsulation** → Wrapping of data and methods into a single unit.
  4. **Inheritance** → Deriving new classes from existing ones.
  5. **Polymorphism** → Ability to use a single interface with different implementations.
  6. **Abstraction** → Hiding internal details and showing only necessary features.

* **Features of OOP**:

  * **Reusability** → Classes and methods can be reused.
  * **Scalability** → Large systems can be built and maintained easily.
  * **Modularity** → Code is divided into classes and objects.
  * **Security** → Encapsulation protects data from unauthorized access.
  * **Flexibility** → Polymorphism provides flexibility in method usage.

* **Example (Java)**:

  ```java
  class Employee {
      int id;
      String name;
      double salary;

      void display() {
          System.out.println(id + " " + name + " " + salary);
      }
  }

  class Manager extends Employee {
      String department;
  }
  ```

* **Explanation**:

  * Here, `Employee` is a class, and `Manager` inherits from it.
  * Encapsulation achieved by combining data (variables) and behavior (methods).
  * Inheritance allows reusing properties in `Manager`.

* **Conclusion**:
  OOP provides a **structured and reusable approach** to software design, making it the backbone of modern programming languages like Java, C++, and Python.

---

### 20. Define triggers? Explain types of triggers

* **Definition**:
  A trigger is a **stored PL/SQL block** that is automatically executed (fired) when a specified event occurs in the database, such as `INSERT`, `UPDATE`, or `DELETE`.

* **Theory**:

  * Triggers are used to enforce **business rules, auditing, and automatic actions**.
  * They cannot be called directly like procedures.
  * Oracle supports **row-level** and **statement-level** triggers.

* **Types of Triggers**:

  1. **Before Trigger** → Executes before an operation (e.g., before insert).
  2. **After Trigger** → Executes after an operation.
  3. **Instead Of Trigger** → Used with views to perform DML operations.
  4. **Row-level Trigger** → Fires once for each row affected.
  5. **Statement-level Trigger** → Fires once per statement, regardless of rows.
  6. **Compound Trigger** → Combines multiple timing points in one trigger.

* **Syntax Example**:

  ```sql
  CREATE OR REPLACE TRIGGER emp_audit
  AFTER INSERT OR UPDATE ON employee
  FOR EACH ROW
  BEGIN
     INSERT INTO emp_log(emp_id, action, action_date)
     VALUES(:NEW.emp_id, 'Modified', SYSDATE);
  END;
  ```

* **Explanation**:

  * `:NEW` and `:OLD` pseudo-records are used to access new and old values.
  * Triggers can log changes, enforce constraints, or maintain derived data.
  * Example above automatically inserts a record in `emp_log` when employee data changes.

* **Conclusion**:
  Triggers are powerful for **automation, security, and data consistency**, but must be used carefully to avoid performance overhead.

---





the question **“Describe about concepts and features of object oriented programming (OOP)”** usually belongs to **Java / C++ / general programming**, not to **Oracle SQL**.

But there’s a reason you might see it in an **Oracle SQL exam**:

### Why it makes sense here

* Oracle introduced **Object-Relational Features** (starting with Oracle 8i).
* It allows database designers to use **OOP concepts** inside SQL/PLSQL.
* You can define **object types (classes)**, create **objects (instances)**, and use **methods (functions/procedures)** in Oracle.

### OOP in Oracle SQL

1. **Object Types (like classes in OOP)**

   ```sql
   CREATE TYPE Employee AS OBJECT (
      emp_id NUMBER,
      emp_name VARCHAR2(50),
      MEMBER PROCEDURE display_emp
   );
   ```

2. **Objects (instances of types)**

   ```sql
   CREATE TABLE emp_table OF Employee;
   ```

3. **Encapsulation** → Data + methods inside object type.

4. **Inheritance** → Oracle supports **subtypes** (specialization).

5. **Polymorphism** → Same method name, different implementations.

