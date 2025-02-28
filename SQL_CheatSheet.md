# SQL Cheat Sheet

## Database Operations

### Show all databases:
```sql
SHOW DATABASES;
```

### Create a new database:
```sql
CREATE DATABASE database_name;
```

### Select a database to use:
```sql
USE database_name;
```

### Delete a database:
```sql
DROP DATABASE database_name;
```

### Check the currently selected database:
```sql
SELECT DATABASE();
```

---

## Table Operations

### Create a new table:
```sql
CREATE TABLE table_name (
    column_name1 data_type,
    column_name2 data_type
);
```

### Show all tables in the database:
```sql
SHOW TABLES;
```

### Describe the structure of a table:
```sql
DESC table_name;
-- or
SHOW COLUMNS FROM table_name;
```

### Delete a table:
```sql
DROP TABLE table_name;
```

---

## Inserting Data

### Insert specific columns:
```sql
INSERT INTO table_name (column_name1, column_name2)
VALUES
(value1, value2),
(value1, value2);
```

### Insert into all columns:
```sql
INSERT INTO table_name
VALUES
(value1, value2),
(value1, value2);
```

**Note:** Order of values must match the column order in the table.

---

## Selecting Data

### Select all columns from a table:
```sql
SELECT * FROM table_name;
```

### Select specific columns:
```sql
SELECT column_name1, column_name2 FROM table_name;
```

### Use Aliases to rename columns in output:
```sql
SELECT column_name1 AS Alias1, column_name2 AS Alias2 FROM table_name;
```

---

## Table Constraints

### Define NOT NULL constraints:
```sql
CREATE TABLE table_name (
    column_name1 data_type NOT NULL,
    column_name2 data_type NOT NULL
);
```

**Note:** Always use single quotes for text values and escape special characters using `\`.

### Set default values:
```sql
CREATE TABLE table_name (
    column_name1 data_type NOT NULL DEFAULT default_value,
    column_name2 data_type NOT NULL DEFAULT default_value
);
```

### Define a Primary Key:
```sql
CREATE TABLE table_name (
    column_name1 data_type PRIMARY KEY,
    column_name2 data_type NOT NULL DEFAULT default_value,
    column_name3 data_type NOT NULL DEFAULT default_value
);
```

**Alternative syntax:**
```sql
CREATE TABLE table_name (
    column_name1 data_type,
    column_name2 data_type NOT NULL DEFAULT default_value,
    column_name3 data_type NOT NULL DEFAULT default_value,
    PRIMARY KEY (column_name1)
);
```

**Note:** Primary key values must be unique and not NULL.

### Auto-increment Primary Key:
```sql
CREATE TABLE table_name (
    column_name1 data_type AUTO_INCREMENT,
    column_name2 data_type NOT NULL DEFAULT default_value,
    column_name3 data_type NOT NULL DEFAULT default_value,
    PRIMARY KEY (column_name1)
);
```

---

## Filtering Data

### Use `WHERE` conditions:
```sql
SELECT * FROM table_name WHERE column_name condition value;
```

**Example:**
```sql
SELECT cat_id, age FROM cats WHERE cat_id = age;
```

### Update records:
```sql
UPDATE table_name SET column_name = new_value WHERE column_name condition value;
```

**Note:** If `WHERE` is omitted, all rows will be updated!

### Delete records:
```sql
DELETE FROM table_name WHERE column_name condition value;
```

**Note:** If `WHERE` is omitted, all rows will be deleted!

---

## String Functions

### Concatenate strings:
```sql
SELECT CONCAT('text1', 'text2');
```

### Get substring:
```sql
SELECT SUBSTRING('string', start_index, length);
```

**Note:** If `length` is not specified, the substring will extend to the end.

### Replace text:
```sql
SELECT REPLACE(string, from_string, to_string);
```

**Note:** Case-sensitive replacement.

### Reverse a string:
```sql
SELECT REVERSE(string);
```

### Get string length:
```sql
SELECT CHAR_LENGTH(string);
SELECT LENGTH(string); -- Returns length in bytes.
```

### Convert case:
```sql
SELECT UPPER(string);
SELECT LOWER(string);
```

### Insert text at a specific position:
```sql
SELECT INSERT('Hello Bobby', 6, 0, 'There');
-- Output: Hello There Bobby
```

### Trim spaces:
```sql
SELECT TRIM(string);
SELECT TRIM(LEADING string_to_remove FROM string);
SELECT TRIM(TRAILING string_to_remove FROM string);
SELECT TRIM(BOTH string_to_remove FROM string);
```

---

## Sorting and Filtering

### Remove duplicates:
```sql
SELECT DISTINCT column_name1, column_name2 FROM table_name;
```

### Sort results:
```sql
SELECT column_name1, column_name2 FROM table_name ORDER BY column_name;
```

**Descending order:**
```sql
SELECT column_name1, column_name2 FROM table_name ORDER BY column_name DESC;
```

**Note:** Default order is ascending.

### Limit results:
```sql
SELECT column_name1, column_name2 FROM table_name LIMIT number_of_results;
```

---

## Searching with `LIKE`

```sql
SELECT column_name1 FROM table_name WHERE column_name LIKE '%search_term%';
```

**Wildcard usage:**  
- `%search_term` → Any number of characters before the term.  
- `search_term%` → Any number of characters after the term.  
- `_search_term_` → Matches exactly one character before/after the term.  

---

## Aggregate Functions

### Count records:
```sql
SELECT COUNT(column_name) FROM table_name;
```

### Find min/max:
```sql
SELECT MIN(column_name) FROM table_name;
SELECT MAX(column_name) FROM table_name;
```

### Sum values:
```sql
SELECT SUM(column_name) FROM table_name;
```

### Calculate averages:
```sql
SELECT AVG(column_name) FROM table_name;
```

---

## Grouping Data

### Group by a column:
```sql
SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
```

**Example:** Count books per author:
```sql
SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;
```

### Order results in groups:
```sql
SELECT author_fname, author_lname, SUM(pages) AS pages_written
FROM books
GROUP BY author_fname, author_lname
ORDER BY pages_written DESC;
```

---

## Subqueries

### Find the longest book title:
```sql
SELECT title FROM books WHERE pages = (SELECT MAX(pages) FROM books);
```

---

## Running SQL from a File
```sql
source file_name.sql;
```

---


# SQL Data Types and Date/Time Functions

## Data Types

### 1. CHAR
- Fixed-length string.
- If the stored value is shorter than the defined length, padding is added.
- Padding is removed when retrieved.

### 2. Numeric Data Types
- **TINYINT / SMALLINT / MEDIUMINT / INT / BIGINT**: Varying ranges of integers.
- **Unsigned Variants**: Adding `UNSIGNED` increases the range of positive numbers.

### 3. DECIMAL
- Format: `DECIMAL(total_digits, digits_after_decimal)`
- Example: `DECIMAL(5, 2) → 999.99`
- Lower range but higher accuracy.

### 4. Floating Point Types
- **FLOAT**: 4 bytes, precision issues after 7 decimal places.
- **DOUBLE**: 8 bytes, precision issues after 15 decimal places.

### 5. Date & Time Data Types
- **DATE**: Stored in `YYYY-MM-DD` format.
- **TIME**: Stored in `HH:MM:SS` format. Can also represent durations.
- **DATETIME**: Stored in `YYYY-MM-DD HH:MM:SS` format.
- **TIMESTAMP**:
  - Similar to `DATETIME` but takes less storage.
  - Has a smaller range than `DATETIME`.

#### Example Table:
```sql
CREATE TABLE user (
    name VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    profile_updated DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

---

## Date/Time Functions

### Retrieving Current Date & Time
```sql
SELECT CURTIME();       -- Current time
SELECT CURDATE();       -- Current date
SELECT NOW();           -- Current date & time
SELECT CURRENT_TIMESTAMP(); -- Alias for NOW()
```

### Extracting Components
```sql
SELECT DAYOFMONTH(<date/date_time>); -- Day of the month
SELECT DAYOFWEEK(<date/date_time>);  -- Sunday = 1, Monday = 2, ..., Saturday = 7
SELECT DAYOFYEAR(<date/date_time>);  -- Number of days passed in the year
SELECT MONTHNAME(<date/date_time>);  -- Returns month name (e.g., 'January')
SELECT DATE(<date_time>);            -- Extracts date from datetime
SELECT TIME(<date_time>);            -- Extracts time from datetime
SELECT YEAR(<date/date_time>);
SELECT HOUR(<time/date_time>);
SELECT MINUTE(<time/date_time>);
SELECT SECOND(<time/date_time>);
```

### Formatting Dates
```sql
SELECT DATE_FORMAT(date_time, '<format_string>');
```
#### Format Examples:
- `%a` → Abbreviated weekday name (Sun, Mon...)
- `%b` → Abbreviated month name (Jan, Feb...)
- `%c` → Month number (0-12)
- `%r` → 12-hour format time

Example:
```sql
SELECT DATE_FORMAT(NOW(), '%a %b %d, %Y %r'); -- Outputs: Mon Jan 01, 2025 10:30:45 PM
```

---

## Date Math

### Difference Between Dates
```sql
SELECT DATEDIFF(<expr1>, <expr2>);
```

### Adding and Subtracting Intervals
```sql
SELECT DATE_ADD(<date>, INTERVAL <value> <unit>);
SELECT DATE_SUB(<date>, INTERVAL <value> <unit>);
```
#### Examples:
```sql
SELECT DATE_ADD('2018-06-01', INTERVAL 1 DAY);    -- 2018-06-02
SELECT DATE_ADD('2018-06-01 23:56:26', INTERVAL 1 SECOND); -- 2018-06-01 23:56:27
SELECT DATE_SUB('2018-06-01', INTERVAL 1 DAY);    -- 2018-05-31
SELECT DATE_SUB('2018-06-01 23:56:26', INTERVAL 1 HOUR); -- 2018-06-01 22:56:26
```

---

## Time Math
```sql
SELECT ADDTIME(<time1>, <time2>);
SELECT SUBTIME(<time1>, <time2>);
```

---



# SQL Operators and Clauses

This document provides examples of various SQL comparison and logic operators, along with their use cases. The examples are based on SQL queries that perform specific tasks such as filtering data, logical operations, and handling different conditions.

## Comparison and Logic Operators

### 1. NOT EQUALS or (`!=`)

```sql
-- NOT EQUALS or (!=)
SELECT title, author FROM books WHERE author_lname != 'Aditya';
```

### 2. NOT LIKE

```sql
-- NOT LIKE :-
SELECT column_name1, column_name2, column_name3 FROM table_name WHERE column_name NOT LIKE '%<string>%';
```

### 3. GREATER THAN

```sql
-- GREATER THAN :-
SELECT * FROM books WHERE released_year > 2000;
--if needed
SELECT * FROM books WHERE released_year >= 2000;
```

### 4. LESS THAN

```sql
-- LESS THAN :-
SELECT * FROM books WHERE released_year < 2000;
--if needed
SELECT * FROM books WHERE released_year <= 2000;
```

### 5. AND

```sql
-- AND :-
SELECT * FROM books WHERE author_lname = 'Vikram' AND released_year > 2000;

SELECT title, released_year FROM books WHERE released_year >= 2000 AND released_year % 2 = 1;
```

### 6. OR

```sql
-- OR :-
SELECT * FROM books WHERE author_lname = 'Vikram' OR released_year > 2000;
```

### 7. BETWEEN

```sql
-- BETWEEN :-
SELECT title, released_year FROM boos WHERE released_year BETWEEN 2004 AND 2015;
--or
SELECT title, released_year FROM boos WHERE released_year >= 2004 AND released_year <= 2015;
```

### 8. NOT BETWEEN

```sql
-- NOT BETWEEN :-
SELECT title, released_year FROM boos WHERE released_year NOT BETWEEN 2004 AND 2015;
--or
SELECT title, released_year FROM boos WHERE released_year < 2004 AND released_year > 2015;
```

### 9. IN

```sql
-- IN :-
SELECT * FROM books WHERE author_lname IN('ADITYA', 'HARSH', 'PREM', 'BABAN');
--or
SELECT * FROM books WHERE author_lname = 'ADITYA' OR author_lname = 'HARSH' OR author_lname = 'PREM' OR author_lname = 'BABAN';
```

### 10. NOT IN

```sql
-- NOT IN :-
SELECT * FROM books WHERE author_lname NOT IN('ADITYA', 'HARSH', 'PREM', 'BABAN');
```

### 11. CASE STATEMENTS

```sql
-- CASE STATEMENTS :-
-- eg: If books rating is > 4 => Good Book, If books rating is < 4 & >3 => Decent Book, If books rating is < 3 => Poor Book

SELECT title, author_lname,
    CASE
        WHEN ratings BETWEEN 5 AND 4 THEN 'Good Book'
        WHEN ratings BETWEEN 4 AND 3 THEN 'Decent Book'
        ELSE 'Poor book'
    END
    AS 'about book'
FROM books;
```

### 12. IS NULL

```sql
-- IS NULL
SELECT * FROM books WHERE author_lname IS NULL;
```

### 13. IS NOT NULL

```sql
-- IS NOT NULL
SELECT * FROM books WHERE author_lname IS NOT NULL;
```

### 14. CAST

```sql
-- CAST :-
SELECT CAST('09:00:00' AS TIME);
--Note :- Use this when comparing Date or Time
SELECT * FROM people WHERE birthtime BETWEEN CAST('09:00:00' AS TIME) AND CAST('12:00:00' AS TIME);
```

# SQL Constraints and ALTER TABLE Commands

## Constraints in SQL

### 1. UNIQUE Constraint
Ensures that all values in a column are distinct.

```sql
CREATE TABLE companies(
    id INT AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(10) NOT NULL UNIQUE,
    PRIMARY KEY (id)
);
```

### 2. CHECK Constraint
Ensures that a column meets a specific condition.

```sql
CREATE TABLE driver (
    name VARCHAR(50),
    age INT CHECK (age > 18)
);
```

#### Naming a CHECK Constraint
We can provide a custom name for the constraint:

```sql
CREATE TABLE driver (
    name VARCHAR(50),
    age INT,
    CONSTRAINT age_over_18 CHECK (age > 18)
);
```

#### Multi-Column CHECK Constraint
Ensures that a combination of columns meets a condition.

```sql
CREATE TABLE houses (
    purchase_price INT NOT NULL,
    sale_price INT NOT NULL,
    CONSTRAINT must_be_profit CHECK(purchase_price < sale_price)
);
```

## ALTER TABLE Commands

### 1. ADD COLUMN
Adds a new column to an existing table.

```sql
ALTER TABLE <table_name> ADD COLUMN <column_name> <column_definition>;
```

### 2. DROP COLUMN
Removes a column from a table.

```sql
ALTER TABLE <table_name> DROP COLUMN <column_name>;
```

### 3. RENAME TABLE
Changes the name of a table.

```sql
RENAME TABLE <current_name> TO <new_name>;
```

or

```sql
ALTER TABLE <current_name> RENAME TO <new_name>;
```

### 4. RENAME COLUMN
Changes the name of a column.

```sql
ALTER TABLE <table_name> RENAME COLUMN <current_name> TO <new_name>;
```

### 5. MODIFY COLUMN
Changes the data type or properties of a column.

```sql
ALTER TABLE <table_name> MODIFY <column_name> <new_definition>;
```

or

```sql
ALTER TABLE <table_name> CHANGE <column_name> <new_column_name> <new_definition>;
```

## ALTER TABLE Constraints

### 1. ADD CONSTRAINT
Adds a constraint to an existing table.

```sql
ALTER TABLE house ADD CONSTRAINT positive_price CHECK (purchase_price > 0);
```

### 2. DROP CONSTRAINT
Removes a constraint from a table.

```sql
ALTER TABLE house DROP CONSTRAINT positive_price;
```

# 📖 SQL Relationships and Joins

In relational databases, tables are often related to each other to ensure data consistency and integrity. This document explains different types of relationships in SQL and how to implement them using foreign keys.

---

## 🏛️ Understanding Relationships

Imagine you own a bookstore with tables like `Orders`, `Reviews`, `Authors`, `Versions`, and `Customers`. These tables are interconnected through relationships, which help maintain data consistency.

### 🔗 Types of Relationships

1. **One-to-One (1:1)**
2. **One-to-Many (1:M)**
3. **Many-to-Many (M:M)**

**Note:** *Foreign keys* create these relationships by referencing another table's primary key.

---

## 1️⃣ One-to-One Relationship

*Example: A person has only one passport.*

```sql
CREATE TABLE person (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE passport (
    id INT PRIMARY KEY AUTO_INCREMENT,
    passport_number VARCHAR(20) UNIQUE NOT NULL,
    person_id INT UNIQUE,  -- Ensures one person has only one passport
    FOREIGN KEY (person_id) REFERENCES person(id) ON DELETE CASCADE
);
```

### 🔍 Explanation:
- `person_id` is marked `UNIQUE` to ensure that each person can only have one passport.
- `ON DELETE CASCADE` ensures that if a person is deleted, their passport record is also removed.

---

## 2️⃣ One-to-Many Relationship

*Example: One customer can place multiple orders.*

```sql
CREATE TABLE customer (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE NOT NULL,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customer(id) ON DELETE CASCADE
);
```

### 🔍 Explanation:
- Each `order` is associated with one `customer`.
- One `customer` can have many `orders`.

---

## 3️⃣ Many-to-Many Relationship

*Example: Students can enroll in multiple courses, and each course can have multiple students.*

```sql
CREATE TABLE student (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE course (
    id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100) NOT NULL
);

CREATE TABLE student_course (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id), -- Composite primary key
    FOREIGN KEY (student_id) REFERENCES student(id) ON DELETE CASCADE,
    FOREIGN KEY (course_id) REFERENCES course(id) ON DELETE CASCADE
);
```

### 🔍 Explanation:
- `student_course` is a **junction table** that connects `student` and `course`.
- Composite primary key (`student_id`, `course_id`) ensures unique combinations.

**💡 Why use a junction table?**
- A book can be written by multiple authors, and an author can write multiple books.

---

## ⚠️ The Importance of Relationships

Without proper relationships, databases may contain invalid data. For example:
- An `order` might reference a `customer` that doesn't exist.

**SQL ensures data integrity** through foreign keys that prevent these anomalies.

---

## 🔍 Deep Dive: Many-to-Many with Series, Reviewers, and Reviews

Let's consider a scenario where a TV series has multiple reviews from different reviewers.

```sql
CREATE TABLE reviewers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);

CREATE TABLE series (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    released_year YEAR,
    genre VARCHAR(100)
);

CREATE TABLE reviews (
    id INT PRIMARY KEY AUTO_INCREMENT,
    rating DECIMAL(2, 1),
    series_id INT,
    reviewer_id INT,
    FOREIGN KEY (series_id) REFERENCES series(id),
    FOREIGN KEY (reviewer_id) REFERENCES reviewers(id)
);
```

### 🔍 Explanation:
- Each review is connected to both a `series` and a `reviewer`.
- This structure avoids redundant data.

---

## 🚨 Final Notes

1. **Use foreign keys** to maintain referential integrity.
2. **Junction tables** are essential for many-to-many relationships.
3. **`ON DELETE CASCADE`** ensures data consistency when related records are removed.
4. **Avoid incorrect data** by properly designing relationships. For instance, preventing orders from referencing non-existent customers.


# Cross Join Example

## Overview
A **CROSS JOIN** returns the Cartesian product of two tables, meaning every row from the first table is combined with every row from the second table.

## Example

### Consider two tables:

#### `students` Table:
| id | name  |
|----|-------|
| 1  | Alice |
| 2  | Bob   |

#### `courses` Table:
| id | course_name  |
|----|-------------|
| 1  | Math        |
| 2  | Science     |

### CROSS JOIN Query:
```sql
SELECT students.name, courses.course_name
FROM students
CROSS JOIN courses;
```

### Result:
| name  | course_name |
|-------|------------|
| Alice | Math       |
| Alice | Science    |
| Bob   | Math       |
| Bob   | Science    |

Since we have 2 students and 2 courses, the result has **2 × 2 = 4 rows**.

## Notes
- CROSS JOIN is useful when you need all possible combinations between two tables.
- Be cautious when using it on large tables, as the result set grows exponentially.


# Inner Join Example

## Overview
An **INNER JOIN** returns only the rows where there is a match between both tables based on a specified condition.

## Example

### Consider two tables:

#### `students` Table:
| id | name  |
|----|-------|
| 1  | Alice |
| 2  | Bob   |
| 3  | Charlie |

#### `enrollments` Table:
| student_id | course_name  |
|------------|-------------|
| 1          | Math        |
| 2          | Science     |
| 2          | Math        |

### INNER JOIN Query:
```sql
SELECT students.name, enrollments.course_name
FROM students
INNER JOIN enrollments ON students.id = enrollments.student_id;
```

### Result:
| name  | course_name |
|-------|------------|
| Alice | Math       |
| Bob   | Science    |
| Bob   | Math       |

Only the students who have enrollments are included in the result.

## Notes
- INNER JOIN is useful when you only want data that has corresponding matches in both tables.
- If a student has no enrolled courses, they will not appear in the result.



# LEFT JOIN in SQL

## Overview

A **LEFT JOIN** (also called a **LEFT OUTER JOIN**) is used in SQL to combine rows from two or more tables based on a related column. The LEFT JOIN returns all rows from the left table (the first table), and the matched rows from the right table (the second table). If there is no match, NULL values are returned for columns of the right table.

### Syntax
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

- **table1**: The left table.
- **table2**: The right table.
- **column**: The column used for the join condition.

---

## Example

Let's say we have two tables, `students` and `courses`, where each student may have enrolled in a course.

### students Table
| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 3          | Charlie      |

### courses Table
| course_id | student_id | course_name |
|-----------|------------|-------------|
| 101       | 1          | Math        |
| 102       | 2          | Science     |

### SQL Query

```sql
SELECT students.student_name, courses.course_name
FROM students
LEFT JOIN courses
ON students.student_id = courses.student_id;
```

### Result

| student_name | course_name |
|--------------|-------------|
| Alice        | Math        |
| Bob          | Science     |
| Charlie      | NULL        |

---

## Key Points

- The LEFT JOIN will always return all records from the **left table** (students), even if there is no matching record in the **right table** (courses).
- When there is no match, NULL values are used for the right table's columns.

---

## Conclusion

The LEFT JOIN is a powerful SQL operation to retrieve all records from one table, even if there is no match in the related table. It helps ensure that you don't lose valuable data from the left table during queries involving relationships between tables.


# 🔍 SQL RIGHT JOIN

The `RIGHT JOIN` keyword in SQL is used to return all records from the right table and the matched records from the left table. If there is no match, `NULL` values are returned for columns from the left table.

---

## 🛠️ Syntax

```sql
SELECT columns
FROM left_table
RIGHT JOIN right_table
ON left_table.column = right_table.column;
```

---

## 📖 Explanation
- **`left_table`**: The table on the left side of the `JOIN` clause.
- **`right_table`**: The table on the right side of the `JOIN` clause.
- **`ON`**: The condition that specifies how rows from the tables are matched.

---

## 🧠 Visual Representation

Imagine you have two tables: `employees` and `departments`.

### 👥 Employees Table
| employee_id | employee_name | department_id |
|--------------|----------------|---------------|
| 1            | Alice          | 101           |
| 2            | Bob            | 102           |
| 3            | Charlie        | NULL          |

### 🏢 Departments Table
| department_id | department_name |
|----------------|-----------------|
| 101            | HR              |
| 102            | IT              |
| 103            | Finance         |

---

## 🖥️ Query Example

```sql
SELECT e.employee_name, d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id;
```

### 📋 Output
| employee_name | department_name |
|----------------|-----------------|
| Alice         | HR              |
| Bob           | IT              |
| NULL          | Finance         |

---

## 🚨 Key Points
1. **All records from the right table** are included.
2. Records from the left table are included **only if they have a matching record** in the right table.
3. If there's no match, **NULL** is returned for the left table's columns.

---

## ⚠️ When to Use RIGHT JOIN
- When you want **all records from the right table** regardless of matching records in the left table.
- Useful when the right table contains master or reference data.



**Happy Querying! 🛠️**



## Notes
- The SQL commands written above are important for working with different data types and date/time operations.
- Understanding these concepts ensures better data management and query optimization.


### 🚀 This cheat sheet covers fundamental SQL operations for databases, tables, queries, and functions. Happy querying! 🎯
