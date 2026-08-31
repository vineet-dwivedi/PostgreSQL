# 🐘 PostgreSQL — Clauses, Operators & Aggregation Functions

This section covers commonly used SQL clauses, operators, and aggregation functions for filtering, sorting, grouping, and summarizing data.

## 📌 Table of Contents

- [SQL Clauses](#sql-clauses)
- [Basic Clause Examples](#basic-clause-examples)
- [Clauses with Operators](#clauses-with-operators)
- [LIKE Operator](#like-operator)
- [Aggregation Functions](#aggregation-functions)
- [GROUP BY and HAVING](#group-by-and-having)
- [Practice Questions](#practice-questions)
- [Practice Answers](#practice-answers)
- [Quick Cheat Sheet](#quick-cheat-sheet)

---

## 📚 SQL Clauses

| Clause | Purpose |
|---|---|
| `SELECT` | Choose which columns to display |
| `FROM` | Specify the table |
| `WHERE` | Filter rows based on a condition |
| `GROUP BY` | Group rows for aggregation |
| `HAVING` | Filter aggregated groups after GROUP BY |
| `ORDER BY` | Sort results in ascending or descending order |
| `LIMIT` | Limit the number of rows returned |
| `AS` | Rename columns or tables temporarily (aliasing) |
| `DISTINCT` | Return only unique values |

---

## 🧪 Basic Clause Examples

Assume a `products` table:

```
products
├── name
├── price
├── category
├── stock
└── sku_code
```

### 1. SELECT

```sql
SELECT name, price
FROM products;
```

Selects only the `name` and `price` columns.

### 2. FROM

```sql
SELECT *
FROM products;
```

`FROM` specifies the table from which the data is retrieved.

### 3. WHERE

```sql
SELECT *
FROM products
WHERE category = 'Electronics';
```

Filters rows according to a condition.

### 4. GROUP BY

```sql
SELECT category
FROM products
GROUP BY category;
```

Groups rows having the same category.

### 5. HAVING

`HAVING` filters groups after `GROUP BY`.

```sql
SELECT category, COUNT(*) AS product_count
FROM products
GROUP BY category
HAVING COUNT(*) > 1;
```

This returns categories containing more than one product.

**WHERE vs HAVING**

| WHERE | HAVING |
|---|---|
| Filters individual rows | Filters groups |
| Used before grouping | Used after grouping |
| Usually works with row-level conditions | Commonly used with aggregate functions |

### 6. ORDER BY

Ascending:

```sql
SELECT *
FROM products
ORDER BY price ASC;
```

Descending:

```sql
SELECT *
FROM products
ORDER BY price DESC;
```

- `ASC` = smallest to largest / A to Z
- `DESC` = largest to smallest / Z to A

### 7. LIMIT

```sql
SELECT *
FROM products
LIMIT 3;
```

Returns only the first 3 rows from the result.

### 8. AS — Alias

```sql
SELECT
    name AS item_name,
    price AS item_price
FROM products;
```

`AS` temporarily renames a column in the query result. Table aliases are also possible:

```sql
SELECT p.name, p.price
FROM products AS p;
```

### 9. DISTINCT

```sql
SELECT DISTINCT category
FROM products;
```

Returns each category only once.

---

## ⚙️ Clauses with Operators

Operators make filtering more powerful. They allow us to ask questions such as:

- Which products cost more than ₹500?
- Which products belong to Electronics or Fitness?
- Which SKU codes start with W?
- Which products have stock above 50?
- Which products do not cost ₹299?

**Common SQL Operators**

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `price = 299` |
| `<>` | Not equal to | `price <> 299` |
| `!=` | Not equal to | `price != 299` |
| `>` | Greater than | `price > 500` |
| `<` | Less than | `price < 500` |
| `>=` | Greater than or equal to | `stock >= 50` |
| `<=` | Less than or equal to | `stock <= 50` |
| `IN` | Matches any value in a list | `category IN (...)` |
| `LIKE` | Pattern matching | `sku_code LIKE 'W%'` |
| `AND` | Both conditions must be true | `stock > 50 AND price > 299` |
| `OR` | At least one condition must be true | `category = 'Fitness' OR category = 'Electronics'` |

### 📌 IN Operator

`IN` is useful when matching a column against multiple possible values.

Instead of:

```sql
SELECT *
FROM products
WHERE category = 'Electronics'
   OR category = 'Fitness';
```

we can write:

```sql
SELECT *
FROM products
WHERE category IN ('Electronics', 'Fitness');
```

---

## 🔤 LIKE Operator

`LIKE` is used for pattern matching.

| Wildcard | Meaning |
|---|---|
| `%` | Zero or more characters |
| `_` | Exactly one character |

### % — Zero or More Characters

```sql
SELECT *
FROM products
WHERE sku_code LIKE 'W%';
```

Finds SKU codes that start with `W`. Possible matches:
- `W100`
- `W-234`
- `WATCH01`

### _ — Exactly One Character

```sql
SELECT *
FROM products
WHERE sku_code LIKE '_B%';
```

Meaning:
- `_` → exactly one character
- `B` → second character must be B
- `%` → anything after it

Possible matches:
- `AB123`
- `XB900`
- `1B500`

---

## 📊 Aggregation Functions

Aggregation functions summarize data instead of returning every individual row. They answer questions such as:

- How many products are there?
- What is the total stock?
- What is the average price?
- What is the cheapest product?
- What is the most expensive product?

| Function | Purpose | Example |
|---|---|---|
| `COUNT()` | Count rows/values | Total number of products |
| `SUM()` | Add numeric values | Total stock |
| `AVG()` | Calculate average | Average price |
| `MIN()` | Find smallest value | Cheapest price |
| `MAX()` | Find highest value | Most expensive price |

### COUNT()

```sql
SELECT COUNT(*)
FROM products;
```

Counts all rows.

```sql
SELECT COUNT(price)
FROM products;
```

Counts non-`NULL` values in `price`.

### SUM()

```sql
SELECT SUM(stock)
FROM products;
```

Returns total stock.

### AVG()

```sql
SELECT AVG(price)
FROM products;
```

Returns the average price.

### MIN()

```sql
SELECT MIN(price)
FROM products;
```

Returns the smallest price.

### MAX()

```sql
SELECT MAX(price)
FROM products;
```

Returns the highest price.

---

## 🗂️ GROUP BY and HAVING

Aggregation becomes especially useful with `GROUP BY`.

**Count products in each category**

```sql
SELECT
    category,
    COUNT(*) AS product_count
FROM products
GROUP BY category;
```

**Average price per category**

```sql
SELECT
    category,
    AVG(price) AS average_price
FROM products
GROUP BY category;
```

**Categories with more than one product**

```sql
SELECT
    category,
    COUNT(*) AS product_count
FROM products
GROUP BY category
HAVING COUNT(*) > 1;
```

Remember:

```
WHERE     → Filters rows
GROUP BY  → Creates groups
HAVING    → Filters groups
```

---

## 🧪 Practice Questions

<details>
<summary>Q1 — Cheapest Product</summary>

Display the name and price of the cheapest product in the entire table.

</details>

<details>
<summary>Q2 — Average Price</summary>

Find the average price of products belonging to the Home & Kitchen or Fitness category.

</details>

<details>
<summary>Q3 — Available Products</summary>

Show product names and stock quantity where stock is more than 50 and price is not equal to ₹299.

</details>

<details>
<summary>Q4 — Most Expensive Per Category</summary>

Find the most expensive product in each category, showing its name and price.

</details>

<details>
<summary>Q5 — Unique Categories</summary>

Show all unique categories in uppercase, sorted in descending order.

</details>

---

## ✅ Practice Answers

### Q1. Cheapest Product

```sql
SELECT name, price
FROM products
ORDER BY price ASC
LIMIT 1;
```

Alternative that also returns ties:

```sql
SELECT name, price
FROM products
WHERE price = (
    SELECT MIN(price)
    FROM products
);
```

### Q2. Average Price

```sql
SELECT AVG(price) AS average_price
FROM products
WHERE category IN ('Home & Kitchen', 'Fitness');
```

### Q3. Stock > 50 and Price ≠ ₹299

```sql
SELECT name, stock
FROM products
WHERE stock > 50
  AND price <> 299;
```

Since `stock > 50` already means the product has stock, a separate availability condition is unnecessary unless the table contains an `is_available` column.

### Q4. Most Expensive Product in Each Category

```sql
SELECT
    category,
    name,
    price
FROM products p
WHERE price = (
    SELECT MAX(p2.price)
    FROM products p2
    WHERE p2.category = p.category
);
```

This returns every product tied for the highest price within its category.

### Q5. Unique Categories in Uppercase

```sql
SELECT DISTINCT UPPER(category) AS category
FROM products
ORDER BY category DESC;
```

This combines:
- `DISTINCT` → removes duplicates
- `UPPER()` → converts text to uppercase
- `ORDER BY` → sorts the result

---

## 🧠 Query Building Pattern

```
SELECT    → What do I want to display?
FROM      → Where is the data?
WHERE     → Which rows do I need?
GROUP BY  → How should rows be grouped?
HAVING    → Which groups should remain?
ORDER BY  → How should the result be sorted?
LIMIT     → How many rows should I return?
```

Example:

```sql
SELECT category, AVG(price) AS average_price
FROM products
WHERE stock > 0
GROUP BY category
HAVING AVG(price) > 500
ORDER BY average_price DESC
LIMIT 3;
```

---

## ⚡ Quick Cheat Sheet

| Concept | Syntax |
|---|---|
| Select | `SELECT name, price` |
| Table | `FROM products` |
| Filter rows | `WHERE price > 500` |
| Group rows | `GROUP BY category` |
| Filter groups | `HAVING COUNT(*) > 1` |
| Ascending | `ORDER BY price ASC` |
| Descending | `ORDER BY price DESC` |
| Limit | `LIMIT 3` |
| Alias | `price AS item_price` |
| Unique values | `DISTINCT category` |
| Match list | `IN ('A', 'B')` |
| Pattern match | `LIKE 'W%'` |
| Count | `COUNT(*)` |
| Total | `SUM(stock)` |
| Average | `AVG(price)` |
| Minimum | `MIN(price)` |
| Maximum | `MAX(price)` |
| Uppercase | `UPPER(category)` |

---

## 🎯 Key Takeaways

Clauses control how a query retrieves and shapes data, operators make filtering powerful, and aggregate functions turn many rows into useful summaries.

```
SELECT   → What?
FROM     → Where?
WHERE    → Which rows?
GROUP BY → Which groups?
HAVING   → Which groups survive?
ORDER BY → What order?
LIMIT    → How many?

COUNT() → How many?
SUM()   → Total?
AVG()   → Average?
MIN()   → Smallest?
MAX()   → Largest?
```
