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



## Notes
- The SQL commands written above are important for working with different data types and date/time operations.
- Understanding these concepts ensures better data management and query optimization.


### 🚀 This cheat sheet covers fundamental SQL operations for databases, tables, queries, and functions. Happy querying! 🎯
