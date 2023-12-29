### Introduction to Relational Databases and SQL: Lecture Notes

#### I. Introduction
- **Topic:** Relational Databases and SQL
- **Focus:** 
  - Understanding relational databases
  - Introduction to SQL (Standard Query Language)
  - Preview of upcoming video content

#### II. Relational Databases
- **Definition:** A system where data is stored in tables (relations).
- **Example Tables:** 'Items' and 'Employees'
  - **Items Table:** Attributes are name, price, number.
  - **Employees Table:** Attributes are birthday, first name, family name.
- **Data Organization:** 
  - Rows (Tuples): Each row in a table represents a data record.
  - Columns (Attributes): Each column represents a specific data type (string, number, date, etc.).
- **Schema Concept:**
  - Definition: A way to define the structure of a table.
  - Example: The schema for 'Items' is Items(name, price, number).

#### III. Characteristics of Relational Tables
- **Columns/Attributes:** Fixed in number and type over time.
- **Rows/Tuples:** Variable in number; content can change over time.
- **Size Variability:** Small number of columns vs. potentially large number of rows.

#### IV. Usage of Rows in Tables
- **Representation:** Each row typically represents an entity (physical or abstract) or a relationship.
- **Examples:**
  - Employee table rows represent individual employees.
  - Item table rows represent individual items.
  - Transaction table rows might represent a sales transaction.

#### V. Impedance Mismatch in Object-Oriented Programming
- **Problem:** Inconsistency in treating objects between databases and object-oriented programming.
  - In databases, identical rows are considered the same.
  - In programming, objects with identical properties are not necessarily the same.

#### VI. Introduction to SQL (Standard Query Language)
- **Relation to Databases:** SQL is the primary language used for interacting with relational databases.
- **Standard Evolution:** Regular updates since 1986, with discrepancies between standards and implementations.
- **Components of SQL:**
  1. **Data Definition Language (DDL):** Creating, altering, deleting databases and tables.
  2. **Data Manipulation Language (DML):** Adding, removing, updating data, and querying.
  3. **Transact SQL:** Managing sequences of SQL statements (transactions).

#### VII. Structure of SQL Content in the Course
- **Week 1-2 (Tutorials):** Focus on Data Definition Language and Data Manipulation Language.
- **Week 3-5 (Transact SQL):** Dealing with SQL statements and transaction-related problems.

#### VIII. Conclusion and Upcoming Content
- **Recap:** Overview of relational databases and introduction to SQL.
- **Next Videos:** Detailed exploration of DDL, DML, querying techniques, and Transact SQL.

### SQL Data Definition Language (DDL): Lecture Notes

#### I. Overview of SQL DDL
- **Focus:** Creation, modification, and deletion of databases and tables.
- **Key Operations:** Creating databases, creating/modifying/deleting tables.

#### II. Creating a Database
- **Syntax:** `CREATE DATABASE [database_name];`
- **Example:** `CREATE DATABASE cs_store;`
- **Concept:** A database is like a folder containing tables, views, triggers.
- **Case Sensitivity:** SQL is not case sensitive.

#### III. Creating Tables
- **Syntax:** 
  ```
  CREATE TABLE [table_name] (
      [column1] [data_type],
      [column2] [data_type],
      ...
  );
  ```
- **Schema Representation:** `table_name(column1, column2, column3, ...)`
- **Whitespace:** Flexible but follow conventional formatting for clarity.

#### IV. Data Types in SQL
- **Integer:** `INT`
- **Floating Point Numbers:** `FLOAT`
- **Strings:**
  - Fixed Length: `CHAR(x)` where x is length.
  - Variable Length: `VARCHAR(x)` where x is maximum length.
- **Dates:**
  - Date: `DATE` format `YYYY-MM-DD`
  - DateTime: `DATETIME` format `YYYY-MM-DD HH:MM:SS`
- **Others:** `XML` for XML files, `BLOB` for binary files.

#### V. Constraints in SQL
1. **Unique Constraint:**
   - Syntax: `ADD CONSTRAINT [constraint_name] UNIQUE([column1, column2, ...]);`
   - Ensures unique values for the specified column(s).
2. **Primary Key:**
   - Syntax: `ADD CONSTRAINT [constraint_name] PRIMARY KEY([column1, column2, ...]);`
   - Unique and used for physical sorting in storage.
   - Only one primary key per table.
3. **Foreign Key:**
   - Syntax: 
     ```
     ADD CONSTRAINT [constraint_name] FOREIGN KEY([child_column])
     REFERENCES [parent_table]([parent_column]);
     ```
   - Links two tables; ensures child column values exist in the parent table.

#### VI. Modifying and Deleting in SQL
1. **Dropping (Deleting):**
   - Database: `DROP DATABASE [database_name];`
   - Table: `DROP TABLE [table_name];`
2. **Altering Tables:**
   - Add Column: `ALTER TABLE [table_name] ADD [column_name] [data_type];`
   - Modify Column: `ALTER TABLE [table_name] MODIFY [column_name] [new_data_type];`
   - Remove Column: `ALTER TABLE [table_name] DROP COLUMN [column_name];`

#### VII. Practical Examples
- **Example of Table Creation:**
  ```
  CREATE TABLE employees (
      birthday DATE,
      first_name VARCHAR(100),
      family_name VARCHAR(100)
  );
  ```
- **Adding Constraints:**
  - Unique: `ADD CONSTRAINT uc_employees UNIQUE(birthday, first_name);`
  - Primary Key: `ADD CONSTRAINT pk_employees PRIMARY KEY(birthday, first_name);`
  - Foreign Key: `ADD CONSTRAINT fk_transactions FOREIGN KEY(emp_id) REFERENCES employees(EID);`

#### VIII. Conclusion
- **Topics Covered:** 
  - Basics of creating and managing databases and tables in SQL.
  - Understanding different data types and constraints.
  - Modifying table structures and handling database/table deletion.

### SQL Data Manipulation Language (DML) - Excluding Queries: Lecture Notes

#### I. Introduction to SQL DML
- **Focus:** Operations for manipulating data in SQL (excluding queries).
- **Components of DML:**
  1. Inserting rows into a table.
  2. Deleting rows from a table.
  3. Updating rows in a table.
  4. Making queries for tables (covered in separate videos).

#### II. Inserting Data into Tables
- **Basic Insert Syntax:**
  ```
  INSERT INTO [table_name] VALUES ([value1], [value2], ...);
  ```
- **Example:** Inserting a student named Oliver with specific details.
- **String Notation:** Strings are denoted with single quotes in SQL.
- **Selective Column Insertion:**
  - Possible to insert data into specific columns.
  - Example: `INSERT INTO students (program, name) VALUES ('D700', 'Danny');`

#### III. SQL Injections
- **Concept:** A common exploit where malicious SQL code is inserted into an application.
- **Prevention:** Sanitization of database inputs to avoid unintended commands.

#### IV. Deleting Data from Tables
- **Basic Delete Syntax:**
  ```
  DELETE FROM [table_name] WHERE [condition];
  ```
- **Example:** `DELETE FROM students WHERE name = 'John';`
- **Caution:** Incorrect usage can lead to deletion of entire table contents.

#### V. Using 'WHERE' Clauses
- **Purpose:** Specifies conditions for SQL DML operations.
- **Operators:** Equality, Inequality, Greater/Less Than, AND, OR, NOT.
- **Special Operators:**
  - `BETWEEN`: For range conditions.
  - `LIKE`: For pattern matching (using '%' for any sequence of characters, '_' for a single character).
  - `IN`: For specifying a list of possible values.

#### VI. Updating Data in Tables
- **Basic Update Syntax:**
  ```
  UPDATE [table_name] SET [column1] = [value1], [column2] = [value2], ... WHERE [condition];
  ```
- **Example:** Change program of student 'Oliver' to 'G402'.
- **Relative Changes:** Possible to make changes relative to existing data (e.g., incrementing a numeric field).

#### VII. Conclusion
- **Covered:** 
  - How to insert, delete, and update data in SQL tables.
  - Importance of SQL injection prevention.
  - Use of WHERE clauses for condition-based operations.
- **Next:** Detailed exploration of SQL queries in upcoming videos.

### SQL Queries - Required Parts: Lecture Notes

#### I. Introduction to SQL Queries
- **Focus:** Understanding the required components in an SQL query.
- **Components of an SQL Query:**
  - **Required:** `SELECT` and `FROM` clauses.
  - **Optional:** `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY` (covered in next video).
- **Note:** Optional parts are not mandatory for a valid SQL query, but may be included based on the query's requirement.

#### II. Basic SQL Query Structure
- **Example:** `SELECT * FROM employees;` retrieves all data from the employees table.
- **Interpretation:** 
  - `SELECT` specifies what to output.
  - `FROM` identifies the input table.

#### III. The `SELECT` Clause
- **Functions:**
  - **Projections:** Choosing specific columns to display.
  - **Distinct:** Removing duplicate rows.
  - **Renaming:** Changing column names for output.
  - **Creating New Columns:** Performing calculations or transformations.

#### IV. Projections in `SELECT`
- **Syntax:** `SELECT [column1], [column2], ... FROM [table];`
- **Example:** `SELECT family_name, birthday FROM employees;` selects only the family name and birthday columns.

#### V. Distinct in `SELECT`
- **Usage:** Eliminates duplicate rows in the output.
- **Syntax:** `SELECT DISTINCT [column] FROM [table];`
- **Example:** `SELECT DISTINCT first_name FROM employees;` removes duplicates in first names.

#### VI. Renaming in `SELECT`
- **Syntax:** `SELECT [column] AS [new_name] FROM [table];`
- **Example:** `SELECT family_name AS surname FROM employees;` renames the family_name column to surname.

#### VII. Creating New Columns in `SELECT`
- **Methods:** Mathematical operations, constants, or functions.
- **Syntax:** `SELECT [column], [expression] AS [new_column] FROM [table];`
- **Example:** `SELECT name, price * number AS total_cost FROM items;` creates a new column for total cost.

#### VIII. The `FROM` Clause
- **Purpose:** Defines the input tables for the query.
- **Complexity:** Can involve multiple tables, leading to joins.
- **Types of Joins:**
  - **Cross Product:** Combines every row of one table with every row of another.
  - **Natural Join:** Joins tables on common columns.

#### IX. Cross Product Join
- **Syntax:** `SELECT ... FROM [table1], [table2];`
- **Characteristics:** Combines rows from multiple tables, creating a larger table.
- **Example:** Joining employees and items tables.

#### X. Natural Join
- **Syntax:** `SELECT ... FROM [table1] NATURAL JOIN [table2];`
- **Function:** Automatically joins tables on columns with the same name.
- **Cautions:** Can lead to unexpected results if not used carefully.

#### XI. Conclusion
- **Summary:** 
  - The required parts of SQL queries include the `SELECT` and `FROM` clauses.
  - `SELECT` determines the output, while `FROM` sets the input tables.
  - Understanding joins and their implications is crucial for constructing effective queries.

### SQL Queries - Optional Parts: Lecture Notes

#### I. Overview
- **Focus:** Exploring optional components in SQL queries.
- **Components:** `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`.
- **Note:** These components enhance the depth and specificity of queries.

#### II. The `WHERE` Clause
- **Usage:** Filters the results based on specified conditions.
- **Subqueries:** Can be used within `WHERE` for dynamic filtering.
- **Example:** `SELECT * FROM students WHERE name IN (SELECT name FROM lecturers);`

#### III. The `GROUP BY` Clause
- **Purpose:** Groups rows sharing a common attribute for aggregate functions.
- **Example:** `SELECT employee_id, COUNT(transaction_id) FROM transactions GROUP BY employee_id;`
- **Complications:** Only includes grouped columns or aggregates in `SELECT`.

#### IV. The `HAVING` Clause
- **Usage:** Applies conditions to groups created by `GROUP BY`.
- **Relation to `WHERE`:** `HAVING` filters after grouping, whereas `WHERE` filters before.
- **Example:** `SELECT employee_id, COUNT(transaction_id) FROM transactions GROUP BY employee_id HAVING COUNT(transaction_id) > 1;`

#### V. The `ORDER BY` Clause
- **Purpose:** Sorts the query results.
- **Syntax:** `ORDER BY [column] [ASC|DESC];`
- **Example:** `SELECT * FROM employees ORDER BY family_name ASC, first_name DESC;`

#### VI. Using `GROUP BY` Effectively
- **Approaches to Handle Aggregates:**
  - Include non-aggregated columns in `GROUP BY`.
  - Use aggregate functions on non-grouped columns.
- **Example:** `SELECT first_name, employee_id, COUNT(transaction_id) FROM employees GROUP BY first_name, employee_id;`

#### VII. Semi-Joins
- **Concept:** A subset of join operations, implemented using `EXISTS` or `IN` in the `WHERE` clause.
- **Example:** `SELECT * FROM employees WHERE EXISTS (SELECT 1 FROM transactions WHERE employees.employee_id = transactions.employee_id);`

#### VIII. Subqueries in `WHERE`
- **`IN` Subqueries:** For checking if a value matches any value in a list from a subquery.
- **`EXISTS` Subqueries:** Used to check if a subquery returns any rows, indicating a match.
- **Example with `EXISTS`:** `SELECT * FROM students WHERE EXISTS (SELECT 1 FROM lecturers WHERE students.name = lecturers.name);`

#### IX. Conclusion
- **Summary:** 
  - The optional parts of SQL queries enable more complex and specific data retrieval and manipulation.
  - Understanding how to effectively use `WHERE`, `GROUP BY`, `HAVING`, and `ORDER BY` clauses is essential for advanced SQL querying.

### SQL Union: Lecture Notes

#### I. Introduction to SQL Union
- **Purpose:** Combines the results of two or more `SELECT` statements.
- **Key Point:** Both queries must produce the same number of columns, with similar data types.
- **Syntax:** `SELECT [columns] FROM [table1] UNION SELECT [columns] FROM [table2];`

#### II. Basic Union Usage
- **Example 1:** Combining First and Last Names
  - Query: `SELECT first_name AS name FROM employees UNION SELECT family_name FROM employees;`
  - Result: A single column list of all first names followed by all family names.

#### III. Requirements for Union
- **Similar Data Types:** Columns being united should have compatible data types.
- **Same Number of Columns:** Each `SELECT` statement must have the same number of columns.

#### IV. Advanced Union Examples
- **Example 2:** Combining Multiple Columns
  - Query: `SELECT first_name, employee_id FROM employees UNION SELECT family_name, employee_id FROM employees;`
  - Result: A two-column list with first names and employee IDs followed by family names and employee IDs.

- **Example 3:** Adding Order By
  - Query: `SELECT first_name, employee_id FROM employees UNION SELECT family_name, employee_id FROM employees ORDER BY name;`
  - Result: Similar to Example 2, but sorted by the name column.

#### V. Union Compatibility Issues
- **Incompatible Columns Example:**
  - Incorrect Query: `SELECT first_name FROM employees UNION SELECT family_name, employee_id FROM employees;`
  - Issue: The number of columns in the `SELECT` statements are not the same.

- **Data Type Compatibility:**
  - Varies across different SQL systems.
  - MySQL Example: Treats integers and strings as similar, allowing unions like `SELECT employee_id, first_name FROM employees UNION SELECT family_name, employee_id FROM employees;`
  - SQL Server Example: More strict with data type compatibility, may not allow the above union.

#### VI. Conclusion
- **Summary:** 
  - `UNION` is used to concatenate the results of multiple `SELECT` statements.
  - Essential to ensure the same number of columns and compatible data types.
  - Behavior can vary between different SQL implementations.

### SQL Queries - Miscellaneous and Relational Algebra: Lecture Notes

#### I. Introduction
- **Topic:** Combining SQL query components and understanding relational algebra.
- **Goal:** To demonstrate the flexibility in composing various SQL components and introduce relational algebra concepts.

#### II. SQL Query Execution Order
- **Sequence:** 
  1. `FROM` (Joins)
  2. `WHERE` (Row filtering)
  3. `GROUP BY` (Grouping)
  4. `HAVING` (Group filtering)
  5. `ORDER BY` (Sorting)
  6. `SELECT` (Output)
- **Note:** `SELECT` is processed last, despite being written first.

#### III. SQL Views
- **Definition:** A virtual table created by a query.
- **Usage:** 
  - `CREATE VIEW` to save complex queries.
  - `SELECT` from views like standard tables.
- **Limitations:** Cannot update, delete, or insert into views directly.
- **Modifying Views:** Use `CREATE OR REPLACE VIEW`.
- **Removing Views:** Use `DROP VIEW`.

#### IV. Relational Algebra
- **Concept:** Mathematical system for manipulating and processing relations (tables).
- **Functions:** Similar to SQL queries, with set-based semantics (no duplicates, unordered).

#### V. Relational Algebra Functions
1. **Projection (π):** 
   - Selects specific columns.
   - Example: `π_family name, birthday(Employees)`.
2. **Renaming (ρ):** 
   - Renames columns.
   - Example: `ρ_birthday→bday(Employees)`.
3. **Selection (σ):** 
   - Filters rows based on conditions.
   - Example: `σ_name='Ann'(Employees)`.
4. **Cartesian Product (×):** 
   - Combines each row of one table with every row of another.
   - Example: `Modules × Lectures`.
5. **Natural Join (⋈):** 
   - Joins tables on common columns.
   - Example: `Employees ⋈ Transactions`.

#### VI. Semi-Joins and Group By in Relational Algebra
- **Semi-Joins:** Filters one table based on its relation to another.
- **Group By:** Not explicitly defined in relational algebra; varies in implementation.

#### VII. Composing SQL Components
- **Flexibility:** SQL allows nesting and combining various query components.
- **Example:**
  ```sql
  SELECT first_name, COUNT(*)
  FROM (
      SELECT first_name FROM Employees
      UNION
      SELECT family_name FROM Employees
  ) AS CombinedNames
  GROUP BY first_name;
  ```

#### VIII. Conclusion
- **Key Points:**
  - SQL queries offer extensive flexibility in combining different components.
  - Understanding relational algebra enhances the ability to conceptualize and optimize SQL queries.
  - Views provide a useful tool for managing and reusing complex queries.
