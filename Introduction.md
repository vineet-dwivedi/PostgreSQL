# 🐘 PostgreSQL Notes — Introduction

Welcome to my **PostgreSQL notes**, where I’m documenting SQL and PostgreSQL concepts from the fundamentals to advanced topics.

---

## 📌 Table of Contents

* [What is a Database?](#-what-is-a-database)
* [Key Points of a Database](#-key-points-of-a-database)
* [What is RDBMS?](#-what-is-rdbms)
* [What is a Schema?](#-what-is-a-schema)
* [Quick Summary](#-quick-summary)

---

## 🗄️ What is a Database?

A **Database (DB)** is a collection of **organized data** that can be easily:

* 📖 **Accessed**
* ⚙️ **Managed**
* 🔄 **Updated**

Instead of keeping data in scattered files, a database provides a structured way to store and work with large amounts of information.

### 💡 Simple Example

Imagine we have information about students:

| ID | Name  | Course | Age |
| -: | ----- | ------ | --: |
|  1 | Rahul | CSE    |  21 |
|  2 | Priya | IT     |  22 |
|  3 | Aman  | CSE    |  20 |

This structured collection of student information can be stored inside a database.

---

## 🔑 Key Points of a Database

A database generally provides the following capabilities:

### 1. 📊 Data is Organized

Data is organized into **tables**, making it easier to store and manage related information.

```text
Database
│
├── Students
├── Courses
├── Teachers
└── Departments
```

### 2. 🔍 Data Can Be Queried

We can use a query language such as **SQL (Structured Query Language)** to interact with the data.

The basic operations are:

| Operation | Purpose              | SQL Command |
| --------- | -------------------- | ----------- |
| Create    | Create data/objects  | `CREATE`    |
| Read      | Retrieve data        | `SELECT`    |
| Update    | Modify existing data | `UPDATE`    |
| Delete    | Remove data          | `DELETE`    |

These operations are commonly referred to as **CRUD**:

> **C**reate → **R**ead → **U**pdate → **D**elete

### 3. 🛡️ Data Consistency & Reliability

A database system helps maintain:

* **Consistency** — data remains accurate and follows defined rules.
* **Reliability** — data can be stored and retrieved reliably.
* **Availability** — data can be accessed when required.

---

## 🏛️ What is RDBMS?

**RDBMS** stands for:

> **Relational Database Management System**

It is a software system used to **store, organize, manage, and manipulate data in a relational database**.

### Breaking Down the Term

| Term                  | Meaning                                                                   |
| --------------------- | ------------------------------------------------------------------------- |
| **Relational**        | Data is organized into tables that can be related to each other.          |
| **Database**          | A structured collection of data.                                          |
| **Management System** | Software that allows us to create, read, update, delete, and manage data. |

### 🔗 Why "Relational"?

Consider two tables:

```text
┌──────────────────┐
│     Students     │
├────┬───────┬─────┤
│ ID │ Name  │ ... │
├────┼───────┼─────┤
│ 1  │ Rahul │     │
│ 2  │ Priya │     │
└────┴───────┴─────┘
          │
          │ student_id
          ▼
┌────────────────────┐
│      Courses       │
├────┬───────────────┤
│ ID │ Course        │
├────┼───────────────┤
│ 1  │ PostgreSQL    │
│ 2  │ Java           │
└────┴───────────────┘
```

The tables can be **related using keys**, allowing us to represent relationships between different types of data.

### 🐘 PostgreSQL

**PostgreSQL** is an **open-source object-relational database management system (ORDBMS)** that uses and extends SQL.

Throughout these notes, PostgreSQL will be our primary database system.

---

## 📁 What is a Schema?

A **Schema** is a logical container inside a database that helps organize database objects.

Think of a schema like a **folder inside a database** 📂.

It can contain objects such as:

* 📊 Tables
* 👁️ Views
* ⚙️ Functions
* 🔐 Sequences
* 📌 Other database objects

### 🗂️ Simple Mental Model

```text
Database
│
├── 📁 Schema A
│   ├── 📊 Table
│   ├── 📊 Table
│   ├── 👁️ View
│   └── ⚙️ Function
│
├── 📁 Schema B
│   ├── 📊 Table
│   ├── 👁️ View
│   └── ⚙️ Function
│
└── 📁 Schema C
    └── 📊 Table
```

Schemas help keep database objects **organized and separated logically**.

### 💡 PostgreSQL Example

PostgreSQL creates a default schema called `public`.

```sql
CREATE SCHEMA university;
```

We can then create objects inside it:

```sql
CREATE TABLE university.students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

Here:

```text
Database
   │
   └── university (Schema)
          │
          └── students (Table)
```

---

## ⚡ Quick Summary

| Concept           | Meaning                                             |
| ----------------- | --------------------------------------------------- |
| 🗄️ **Database**  | Organized collection of data                        |
| 📊 **Table**      | Stores data in rows and columns                     |
| 🏛️ **RDBMS**     | Software for managing relational databases          |
| 🔗 **Relation**   | Connection between tables                           |
| 📁 **Schema**     | Logical container used to organize database objects |
| 🐘 **PostgreSQL** | Open-source object-relational database system       |
| 🔄 **CRUD**       | Create, Read, Update, Delete                        |

---

### 🧠 Mental Model

```text
                    🗄️ DATABASE
                         │
              ┌──────────┴──────────┐
              │                     │
         📁 SCHEMA              📁 SCHEMA
              │                     │
       ┌──────┼──────┐        ┌─────┼─────┐
       │      │      │        │     │     │
      📊     📊     👁️       📊    ⚙️    👁️
    TABLE  TABLE   VIEW     TABLE FUNCTION VIEW
```

> **Remember:** A database stores the data, schemas organize database objects, tables store structured data, and SQL allows us to interact with that data.
