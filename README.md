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

