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

### 🚀 This cheat sheet covers fundamental SQL operations for databases, tables, queries, and functions. Happy querying! 🎯
