# Task6
# 📊 Task 6: Sales Trend Analysis Using Aggregations

### 🎯 Objective
Analyze monthly revenue and order volume using SQL aggregation techniques on a retail dataset.

---

## 📁 Dataset Description

**File:** `synthetic_online_retail_data.csv`  
**Total Columns:** 13  
**Source:** Synthetic dataset (manually uploaded)

| Column Name       | Data Type  | Description                         |
|-------------------|------------|-------------------------------------|
| `customer_id`     | `int64`    | Unique ID for each customer         |
| `order_date`      | `object`   | Date when the order was placed      |
| `product_id`      | `int64`    | Unique ID for each product          |
| `category_id`     | `int64`    | Product category ID                 |
| `category_name`   | `object`   | Product category name               |
| `product_name`    | `object`   | Name of the product                 |
| `quantity`        | `int64`    | Quantity ordered                    |
| `price`           | `float64`  | Price per unit                      |
| `payment_method`  | `object`   | Payment method used                 |
| `city`            | `object`   | Customer's city                     |
| `review_score`    | `float64`  | Review score by customer (0–5)      |
| `gender`          | `object`   | Gender of customer                  |
| `age`             | `int64`    | Age of customer                     |

For the purpose of sales analysis, the relevant columns are:
- `order_date`
- `price`
- `quantity`
- `product_id`

---

## 🛠 Tools Used
- SQL (PostgreSQL / MySQL / SQLite)
- Pandas (for data preview)

---

## 🧾 SQL Analysis

### 1. Monthly Revenue and Order Volume

```sql
SELECT 
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(price * quantity) AS monthly_revenue,
    COUNT(DISTINCT CONCAT(order_date, product_id)) AS order_volume
FROM 
    synthetic_online_retail_data
GROUP BY 
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY 
    year, month;
```
### 2. Top 3 Months by Revenue

```sql
SELECT 
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(price * quantity) AS monthly_revenue
FROM 
    synthetic_online_retail_data
GROUP BY 
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY 
    monthly_revenue DESC
LIMIT 3;

