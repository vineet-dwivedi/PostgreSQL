# 🛠️ PostgreSQL — Basic CRUD Operations

CRUD is the foundation of working with data in a database.

> **CRUD = Create → Read → Update → Delete**

These four operations allow us to create new data, retrieve existing data, modify it, and remove it.

---

## 📌 Table of Contents

- [1. Create a Database](#1--create-a-database)
- [2. Connect to a Database](#2--connect-to-a-database)
- [3. Create a Table](#3--create-a-table)
- [4. Insert Data](#4--insert-data)
- [5. Read Data](#5--read-data)
- [6. Update Data](#6--update-data)
- [7. Delete Data](#7--delete-data)
- [8. Complete CRUD Example](#8--complete-crud-example)
- [9. Quick Cheat Sheet](#9--quick-cheat-sheet)

---

## 1. 🏗️ Create a Database

We can create a new database using `CREATE DATABASE`.

```sql
CREATE DATABASE my_db;
```

This creates a database named `my_db`.

### PostgreSQL CLI

If you're using `psql`, you create it the exact same way — connect to psql and run:

```sql
CREATE DATABASE my_db;
```

---

## 2. 🔌 Connect to a Database

After creating the database, we need to connect to it before creating tables or working with its data.

In `psql`:

```
\c my_db
```

Here:

- `\c` → connect
- `my_db` → database name

> 💡 `\c` is a psql meta-command, not standard SQL.

---

## 3. 📊 Create a Table

A table stores data in rows and columns.

Let's create a `students` table.

```sql
CREATE TABLE students (
    student_id INT,
    name CHAR(5),
    age INT,
    grade CHAR(1)
);
```

### Table Structure

```
students
│
├── student_id → INT
├── name       → CHAR(5)
├── age        → INT
└── grade      → CHAR(1)
```

### Example Data

| student_id | name  | age | grade |
|------------|-------|-----|-------|
| 1          | Rahul | 22  | A     |
| 2          | Aryan | 24  | B     |

---

## 4. ➕ Insert Data

The `INSERT` statement is used to add new rows to a table.

### Basic Syntax

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

### Example

```sql
INSERT INTO students (student_id, name, age, grade)
VALUES (1, 'Rahul', 22, 'A');
```

We can insert multiple rows in a single query:

```sql
INSERT INTO students (student_id, name, age, grade)
VALUES
    (1, 'Rahul', 22, 'A'),
    (2, 'Aryan', 24, 'B');
```

### Result

```
 student_id | name  | age | grade
------------+-------+-----+-------
          1 | Rahul | 22  | A
          2 | Aryan | 24  | B
```

> ⚠️ String values should be enclosed in single quotes, like `'this'`.

---

## 5. 📖 Read Data

The `SELECT` statement is used to retrieve/read data from a table.

### Select All Columns

```sql
SELECT *
FROM students;
```

`*` means: select all columns.

### Select Specific Columns

Instead of selecting everything, we can select only the columns we need.

```sql
SELECT name, age
FROM students;
```

Result:

```
 name  | age
-------+-----
 Rahul | 22
 Aryan | 24
```

### 🔎 Using WHERE

The `WHERE` clause is used to filter rows based on a condition.

**Example**

```sql
SELECT *
FROM students
WHERE age = 24;
```

Only students whose age is 24 will be returned.

**Another example**

```sql
SELECT name
FROM students
WHERE grade = 'A';
```

### 🧠 SELECT Structure

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

Example:

```sql
SELECT name, age
FROM students
WHERE age > 20;
```

Think of it as:

- `SELECT` → What do I want?
- `FROM` → From where?
- `WHERE` → Which rows?

---

## 6. ✏️ Update Data

The `UPDATE` statement is used to modify existing data.

### Basic Syntax

```sql
UPDATE table_name
SET column = new_value
WHERE condition;
```

### Example

Suppose Rahul's age needs to be changed from 22 to 23.

```sql
UPDATE students
SET age = 23
WHERE name = 'Rahul';
```

Now:

- **Before** → Rahul = 22
- **After** → Rahul = 23

### ⚠️ Important: Use WHERE

Always be careful with `UPDATE`.

```sql
UPDATE students
SET age = 23;
```

This updates **every row** in the table.

Therefore, when you want to update specific rows, always use `WHERE`:

```sql
UPDATE students
SET age = 23
WHERE name = 'Rahul';
```

> 🚨 No `WHERE` = potentially updating every row.

---

## 7. 🗑️ Delete Data

The `DELETE` statement removes rows from a table.

### Basic Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

### Example

```sql
DELETE FROM students
WHERE student_id = 2;
```

This removes the student whose `student_id` is 2.

### ⚠️ DELETE Without WHERE

```sql
DELETE FROM students;
```

This deletes all rows from the table. The table itself still exists, but its data is gone.

Before:

```
students
├── Rahul
├── Aryan
└── Aman
```

```sql
DELETE FROM students;
```

After:

```
students
└── (empty)
```

> 🚨 Be extremely careful when executing DELETE without a WHERE clause.

---

## 8. 🧪 Complete CRUD Example

Let's perform the complete CRUD workflow from start to finish.

### 🟢 CREATE

Create the table:

```sql
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    age INT,
    grade CHAR(1)
);
```

> 📝 Note: `name` is `VARCHAR(50)` here instead of `CHAR(5)` like in section 3 — `CHAR(5)` pads/truncates to a fixed 5 characters, which is too restrictive for real names. `VARCHAR(50)` allows variable length up to 50 characters instead.

### ➕ CREATE DATA

Insert students:

```sql
INSERT INTO students (student_id, name, age, grade)
VALUES
    (1, 'Rahul', 22, 'A'),
    (2, 'Aryan', 24, 'B'),
    (3, 'Aman', 21, 'A');
```

### 🔵 READ

Read all students:

```sql
SELECT *
FROM students;
```

Read only students older than 21:

```sql
SELECT *
FROM students
WHERE age > 21;
```

### 🟡 UPDATE

Update Rahul's age:

```sql
UPDATE students
SET age = 23
WHERE student_id = 1;
```

### 🔴 DELETE

Delete student with ID 3:

```sql
DELETE FROM students
WHERE student_id = 3;
```

### 🔄 Final Table

After performing the operations above:

| student_id | name  | age | grade |
|------------|-------|-----|-------|
| 1          | Rahul | 23  | A     |
| 2          | Aryan | 24  | B     |

---

## 9. ⚡ Quick Cheat Sheet

| CRUD | SQL Command | Purpose |
|------|-------------|---------|
| 🟢 Create | `INSERT` | Add new rows |
| 🔵 Read | `SELECT` | Retrieve rows |
| 🟡 Update | `UPDATE` | Modify existing rows |
| 🔴 Delete | `DELETE` | Remove rows |

### Most Important Syntax

<details>
<summary>➕ INSERT</summary>

```sql
INSERT INTO students (name, age, grade)
VALUES ('Rahul', 22, 'A');
```

</details>

<details>
<summary>📖 SELECT</summary>

```sql
SELECT *
FROM students
WHERE age > 20;
```

</details>

<details>
<summary>✏️ UPDATE</summary>

```sql
UPDATE students
SET age = 23
WHERE student_id = 1;
```

</details>

<details>
<summary>🗑️ DELETE</summary>

```sql
DELETE FROM students
WHERE student_id = 1;
```

</details>

---

### 🧠 CRUD Mental Model

```
                    DATABASE
                       │
                    STUDENTS
                       │
          ┌────────────┼────────────┐
          │            │            │
       CREATE         READ        UPDATE
          │            │            │
       INSERT        SELECT       UPDATE
          │            │            │
          └────────────┼────────────┘
                       │
                     DELETE
```

> 💡 Remember: **INSERT** adds data → **SELECT** reads data → **UPDATE** changes data → **DELETE** removes data.
