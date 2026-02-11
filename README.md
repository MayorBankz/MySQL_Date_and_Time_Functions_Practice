# MySQL_Date_-_Time_Functions_Practice
## An easy to understand documentation on date & time functions using MySQL
## Date - 11/02/2026

---

## Overview 

This repository focuses exclusively on MySQL Date & Time Functions, providiing hands on practice queries with clear explanation. 

---
📌 Table of Contents
1. Date Aggregation Functions
2. Date Filtering
3. Date Formatting
4. Date Difference Calculations

---

### DATE AGGREGATION FUNCTIONS

QUESTION 1: How many orders were placed each year

```sql
SELECT
  YEAR(orderdate) as order_year,
  count(quantity) as total_orders
FROM salesdb.orders
FROUP BY order_year;
```

Explanation: 
* `YEAR(orderdate)` extracts the year from the order date
* `COUNT` returns the total number of orders per year

---

### QUESTION 2: How many orders were placed each month

```sql
SELECT
  MONTHNAME(orderdate) as order_month,
  COUNT(quantity) as total_orders
FROM salesdb.orders
GROUP BY order_month;
```
Explanation
* `MONTHNAME()` extracts the month name
* Groups orders by month regardless of year

 ---

 ### DATE FILTERING

 QUESTION: Show all orders placed during the month of February

 ```sql
SELECT
  MONTHNAME(orderdate) as order_month,
  COUNT(quantity) as total_orders,
 FROM salesdb.orders
WHERE MONTHNAME(orderdate) = 'February'
GROUP BY order_month
;
```

Explanation 
* Flters records to include only February orders
* Aggregates total orders for the month

---

### DATE FORMATTING

QUESTION: Display `creaiontime` in the following format: `Day Wed Jan Q1 2025 12:34:56`

```sql
SELECT CONCAT(
                'Day ', DATE_FORMAT(creationtime, %a %b '),
                'Q', QUARTER(creationtime), ' ',
                  DATE_FORMAT(creationtime, '%Y %H:%i: %s')
    ) AS formatted_creationtime
FROM orders;
```

### Key Concepts:
* `%a` - abbreviated weekday
* `%b` - abbreviated month
* `QUARTER()` - quarter of the year
* `%Y` - Year
* `%H:%i:%s` - time

 --- 

 ### DATE DIFFERENCE CALCULATIONS
 QUESTION 1: Calculate the age of employees

 ```sql
SELECT
  employeeid,
  birthdate,
  TIMESTAMPDIFF(year, birthdate, curdate()) as current_age
FROM employees;
```
Explanation: 
* `TIMESTAMPDIFF()` calculates completed years
* `CURDATE()` returns the current date

---

QUESTION 2: Find the average shipping duration in days for each month

```sql
SELECT
  YEAR(orderdate) AS order_year,
  MONTH(orderdate) AS order_month,
  AVG(DATEDIFF(shipdate, orderdate)) AS avg_shipping_days
FROM orders
WHERE shipdate IS NOT NULL
GROUP BY
    YEAR(orderdate),
    MONTH(orderdate)
ORDER BY
    order_year,
    order_month;
```

Explanation:
* `DATEDIFF()` calculates shipping duration in days
* `AVG()` returns the average shipping time per month
* Excludes NULL shipping dates

---

QUESTION 3: Find the number of days between each order and the previous order

```sql
SELECT
      orderid,
      orderdate,
      DATEDIFF(orderdate, LAG(orderdate) OVER(ORDER BY orderdate)
  ) AS days_between_orders
FROM orders
ORDER BY orderdate;
```

Explanation:

* `LAG()` retrieves the previous order date
* The first record returns NULL
---

✔️ NOTES
* Focused solely on date & time functions
* Beginner-friendly with real-world examples
