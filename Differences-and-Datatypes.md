# 🐘 PostgreSQL — Differences & Data Types

## 📊 RDBMS Comparison

| Feature | Full RDBMS | RDBMS | Lightweight DB |
|---|---|---|---|
| **Open Source** | Yes | Yes | Yes |
| **Complex Queries** | Excellent | Good | Basic |
| **Performance** | Excellent | Fast on simple operations | Great for small applications |
| **NoSQL Features** | Yes — JSONB | Limited | No |
| **Concurrency** | Strong | Medium | Weak |
| **Use Case** | Enterprise, Big Data | Web Applications | Mobile Apps, Testing |

> 💡 **Note:** PostgreSQL is a full-featured relational/object-relational database system designed to handle complex queries, strong concurrency, and large-scale applications.

---

## 🧬 PostgreSQL Data Types

PostgreSQL provides different data types depending on the kind of data we need to store.

---

### 🔢 1. Numeric Data Types

Numeric data types are used to store **integers, decimal values, and floating-point numbers**.

| Data Type | Description | Example |
|---|---|---|
| `SMALLINT` | 2-byte integer | `age SMALLINT` |
| `INTEGER` / `INT` | 4-byte integer | `quantity INT` |
| `BIGINT` | 8-byte integer | `views BIGINT` |
| `DECIMAL(p,s)` / `NUMERIC(p,s)` | Exact precision numeric value | `price NUMERIC(8,2)` |
| `REAL` | 4-byte floating-point number | `rating REAL` |
| `DOUBLE PRECISION` | 8-byte floating-point number | `accuracy DOUBLE PRECISION` |
| `SERIAL` | Auto-incrementing integer | `id SERIAL PRIMARY KEY` |

#### 🔍 Integer Types

**`SMALLINT`** — Stores a **2-byte signed integer**.

```sql
age SMALLINT
```

Range: `-32,768` to `32,767`. Useful when the value will always remain within a relatively small range.

**`INTEGER` / `INT`** — Stores a 4-byte signed integer.

```sql
quantity INT
```

Approximate range: `-2.1 billion` to `+2.1 billion`. This is the general-purpose integer type.

**`BIGINT`** — Stores an 8-byte signed integer.

```sql
views BIGINT
```

Use it when the number can become very large, such as:
- View counts
- Large IDs
- Financial counters
- Large quantities

#### 💰 Exact Numeric Types

**`NUMERIC` / `DECIMAL`** — Used when exact precision is important.

```sql
price NUMERIC(8,2)
```

Here:
- `8` → Total number of digits
- `2` → Number of digits after the decimal point

For example, `123456.78` has 6 digits before the decimal and 2 after it, for 8 total digits.

> 💡 `NUMERIC` and `DECIMAL` are equivalent types in PostgreSQL. They are commonly preferred for money and financial calculations where floating-point approximation is undesirable.

#### 🌊 Floating-Point Types

**`REAL`** — A 4-byte floating-point number.

```sql
rating REAL
```

Suitable when approximate values are acceptable.

**`DOUBLE PRECISION`** — An 8-byte floating-point number with greater precision than `REAL`.

```sql
accuracy DOUBLE PRECISION
```

Use it when you need a wider range and more precision for approximate floating-point calculations.

#### 🔢 SERIAL

`SERIAL` is used for an auto-incrementing integer column.

```sql
id SERIAL PRIMARY KEY
```

When a new row is inserted, PostgreSQL automatically generates the next integer value. Example:

```
id
---
1
2
3
4
5
```

> ⚠️ **Important:** `SERIAL` is PostgreSQL-specific shorthand for creating an integer column backed by a sequence. For new PostgreSQL designs, identity columns such as `GENERATED ... AS IDENTITY` are generally preferred.

---

### 🔤 2. Character / String Data Types

String data types are used to store textual information.

| Data Type | Description | Example |
|---|---|---|
| `CHAR(n)` | Fixed-length string | `code CHAR(5)` |
| `VARCHAR(n)` | Variable-length string with a maximum length | `email VARCHAR(100)` |
| `TEXT` | Variable-length text with no declared length limit | `bio TEXT` |

**`CHAR(n)`** — Stores a fixed-length string.

```sql
code CHAR(5)
```

If fewer than `n` characters are stored, the value is padded with spaces. For example, `'AB'` stored as `CHAR(5)` is stored as a 5-character value with padding.

> 💡 Use `CHAR(n)` only when fixed-width storage semantics are actually useful.

**`VARCHAR(n)`** — Stores a variable-length string with a maximum character limit.

```sql
email VARCHAR(100)
```

This allows a value of up to 100 characters, e.g. `name VARCHAR(50)`.

**`TEXT`** — Stores variable-length text without specifying a maximum length.

```sql
bio TEXT
```

Useful for:
- Descriptions
- Bios
- Comments
- Articles
- Large text content

> 💡 In PostgreSQL, `TEXT` and `VARCHAR` have essentially the same performance characteristics. `VARCHAR(n)` is mainly useful when you want PostgreSQL to enforce a maximum length.

---

### ✅ 3. Boolean Data Type

The `BOOLEAN` type stores a logical value. It can represent:
- `TRUE`
- `FALSE`
- `NULL`

```sql
is_active BOOLEAN
```

**Example:**

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT,
    is_active BOOLEAN
);
```

---

### 📅 4. Date & Time Data Types

PostgreSQL provides several types for storing dates, times, timestamps, and time durations.

| Data Type | Description | Example |
|---|---|---|
| `DATE` | Stores only a date | `dob DATE` |
| `TIME` | Stores only a time | `login_time TIME` |
| `TIMESTAMP` | Stores date + time | `created_at TIMESTAMP` |
| `TIMESTAMPTZ` | Timestamp with time-zone-aware semantics | `event_at TIMESTAMPTZ` |
| `INTERVAL` | Stores a time duration | `duration INTERVAL` |

**`DATE`** — Stores only the date.

```sql
dob DATE
```

Example: `2025-07-05`

**`TIME`** — Stores only the time of day.

```sql
login_time TIME
```

Example: `14:30:00`

**`TIMESTAMP`** — Stores date + time.

```sql
created_at TIMESTAMP
```

Example: `2025-07-05 14:30:00`

**`TIMESTAMPTZ`** — PostgreSQL's shorthand name for `TIMESTAMP WITH TIME ZONE`.

```sql
event_at TIMESTAMPTZ
```

It is useful when working with events that occur across different time zones.

> 💡 PostgreSQL stores `timestamptz` values internally in UTC and converts them to the current session's time zone when displaying them.

**`INTERVAL`** — Stores a duration or difference between dates/times.

```sql
duration INTERVAL
```

Examples: `2 hours`, `3 days`, `6 months`, `1 year 2 months`

```sql
SELECT INTERVAL '2 hours 30 minutes';
```

---

## 🧠 Quick Data Type Cheat Sheet

| Category | Data Types |
|---|---|
| 🔢 Integer | `SMALLINT`, `INT`, `BIGINT` |
| 💰 Exact Numeric | `NUMERIC`, `DECIMAL` |
| 🌊 Floating Point | `REAL`, `DOUBLE PRECISION` |
| 🔢 Auto Increment | `SERIAL` |
| 🔤 String | `CHAR`, `VARCHAR`, `TEXT` |
| ✅ Boolean | `BOOLEAN` |
| 📅 Date | `DATE` |
| 🕐 Time | `TIME` |
| 📅🕐 Date + Time | `TIMESTAMP` |
| 🌍 Time-zone-aware Timestamp | `TIMESTAMPTZ` |
| ⏱️ Duration | `INTERVAL` |

---

## 🧪 Example Table Using Different Data Types

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    bio TEXT,
    age SMALLINT,
    followers BIGINT,
    rating REAL,
    account_balance NUMERIC(10,2),
    is_active BOOLEAN,
    dob DATE,
    login_time TIME,
    created_at TIMESTAMP,
    last_seen TIMESTAMPTZ,
    membership_duration INTERVAL
);
```

This single table demonstrates how PostgreSQL allows us to choose a data type according to the kind of data being stored.

---

## 🎯 Key Takeaways

- Choose the data type based on the data you actually need to store.
- Use `INT` for normal whole numbers.
- Use `BIGINT` for very large integers.
- Use `NUMERIC` / `DECIMAL` when exact decimal precision matters.
- Use `REAL` / `DOUBLE PRECISION` for approximate floating-point calculations.
- Use `TEXT` for general text.
- Use `VARCHAR(n)` when you specifically want a maximum character limit.
- Use `BOOLEAN` for true/false values.
- Use `DATE` for dates only.
- Use `TIMESTAMP` or `TIMESTAMPTZ` when date and time are required.
- Use `INTERVAL` for durations.
