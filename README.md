# SQL Intermediate Challenge #4: Products Above Category Median

**Difficulty:** Intermediate  
**Estimated time:** 35–50 minutes  
**Concepts:** median calculation, ordering, `COUNT()`, `LIMIT / OFFSET`, correlated subqueries  

This challenge introduces a more advanced statistical concept in SQL: **median**.  
Unlike averages, medians require **positional logic**, which makes this a true intermediate problem.

---

## 🧠 The Challenge

**The product manager asks:**

> “Which products are priced above the median price of their category?”

You’ve already solved “above average.”  
Median is trickier because SQL doesn’t have a universal built-in median function.

---

## 📏 Median Rule (Required)

Within each category:

1. Sort products by:
   - `price ASC`
   - `product_id ASC` (tie-breaker)
2. If the count is:
   - **Odd** → median is the middle value
   - **Even** → median is the average of the two middle values

This definition matches common statistical practice.

---

## 📊 Table Schema

### `products`

| Column Name | Type | Description |
|------------|------|-------------|
| product_id | INTEGER | Unique product ID |
| name | TEXT | Product name |
| category | TEXT | Product category |
| price | DECIMAL | Product price |

---

## 🧪 Sample Data

| product_id | name | category | price |
|-----------:|------|----------|------:|
| 301 | Wireless Mouse | Accessories | 24.99 |
| 302 | USB-C Hub | Accessories | 34.50 |
| 303 | Webcam | Accessories | 59.99 |
| 304 | Mechanical Keyboard | Accessories | 89.00 |
| 305 | Monitor | Displays | 229.99 |
| 306 | 34-inch Monitor | Displays | 399.00 |
| 307 | Desk Lamp | Workspace | 49.99 |
| 308 | Chair Mat | Workspace | 79.99 |
| 309 | Standing Desk | Workspace | 299.00 |

Accessories prices (sorted):  
24.99, 34.50, 59.99, 89.00  
Median = (34.50 + 59.99) / 2 = **47.245**

---

## ✍️ Your Task

Return all products where:

- `price` is **greater than** the median price of their category

Your output must include:

- `category`
- `name`
- `price`
- `category_median_price`

Sort results by:
1. `category` (A–Z)
2. `price` (high → low)

---

## 🧩 Expected Output

| category | name | price | category_median_price |
|---------|------|------:|----------------------:|
| Accessories | Mechanical Keyboard | 89.00 | 47.25 |
| Accessories | Webcam | 59.99 | 47.25 |
| Displays | 34-inch Monitor | 399.00 | 314.50 |
| Workspace | Standing Desk | 299.00 | 79.99 |

---

## ✅ Requirements

Your query must:

- Compute the median **per category**
- Follow the median rule exactly
- Not use `SELECT *`
- Include the median value in the output

---

## 💡 Hint (Optional)

A SQLite-friendly median strategy:

1. Count rows per category
2. Sort prices within each category
3. Use `LIMIT 2 OFFSET (count - 1) / 2`
4. Take the `AVG()` of those rows

---

## 🧪 Write Your SQL Here

```sql
-- Write your query here

