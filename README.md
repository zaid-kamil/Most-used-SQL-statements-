## The Most Used SQL Statements for Data Science Tasks


### 1. SELECT
The `SELECT` statement retrieves data from one or more tables.

```sql
SELECT column1, column2, column3
FROM table_name
WHERE condition;
```

Example: Select all customers aged 18 and over.

```sql
SELECT *
FROM customers
WHERE age >= 18;
```

### 2. JOIN
The `JOIN` statement combines data from two or more tables.

**INNER JOIN:** Returns only matching rows.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
```

**LEFT JOIN:** Returns all rows from the left table, and matching rows from the right table.

```sql
SELECT customers.customer_name, orders.order_id
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```

**RIGHT JOIN:** Returns all rows from the right table, and matching rows from the left table.

```sql
SELECT customers.customer_name, orders.order_id
FROM customers
RIGHT JOIN orders ON customers.customer_id = orders.customer_id;
```

**OUTER JOIN:** Returns all rows from one or both tables, including non-matching rows.

```sql
SELECT customers.customer_name, orders.order_id
FROM customers
LEFT OUTER JOIN orders ON customers.customer_id = orders.customer_id;
```

### 3. WHERE
The `WHERE` statement filters data based on specified conditions.

Example: Select employees in the Sales department earning over $50,000.

```sql
SELECT name, department, salary
FROM employees
WHERE department = 'Sales' AND salary > 50000;
```

### 4. GROUP BY
The `GROUP BY` statement groups data and aggregates results.

Example: Calculate the average salary by department.

```sql
SELECT department, AVG(salary) as avg_salary
FROM employees
GROUP BY department;
```

### 5. HAVING
The `HAVING` statement filters grouped data.

Example: Find customers who ordered at least 50 units.

```sql
SELECT customer_id, SUM(quantity) AS total_quantity
FROM orders
GROUP BY customer_id
HAVING SUM(quantity) >= 50;
```

### 6. Window Function
Window functions perform calculations across rows related to the current row.

**ROW_NUMBER():** Assigns a unique number to each row.

```sql
SELECT column1, ROW_NUMBER() OVER (ORDER BY column1) AS row_num
FROM table_name;
```

**SUM():** Calculates the sum within a partition.

```sql
SELECT column1, SUM(column3) OVER (PARTITION BY column1) AS column3_sum
FROM table_name;
```

**RANK():** Assigns a rank to each row within a partition.

```sql
SELECT column1, RANK() OVER (PARTITION BY column1 ORDER BY column3 DESC) AS rank_num
FROM table_name;
```

**AVG():** Calculates the average within a partition.

```sql
SELECT column1, AVG(column3) OVER (PARTITION BY column1) AS column3_avg
FROM table_name;
```

### 7. UNION
The `UNION` operator combines the results of two or more `SELECT` statements.

Example: List all people in New York from customers and employees tables.

```sql
SELECT name, city
FROM customers
WHERE city = 'New York'
UNION
SELECT name, city
FROM employees
WHERE city = 'New York';
```

### 8. CREATE
The `CREATE` statement creates new database objects.

Example: Create a new `customers` table.

```sql
CREATE TABLE customers (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  email VARCHAR(100),
  phone VARCHAR(20)
);
```

### 9. INSERT
The `INSERT` statement adds new data to a table.

Example: Insert a new student.

```sql
INSERT INTO students (id, name, major, gpa)
VALUES (1234, 'John Doe', 'Computer Science', 3.5);
```

### 10. UPDATE
The `UPDATE` statement modifies existing data in a table.

Example: Update a student's major and GPA.

```sql
UPDATE students
SET major = 'Mathematics', gpa = 3.7
WHERE id = 1234;
```

### Examples for Difficult Ones

**Window Function Example: Cumulative Sum**

```sql
SELECT customer_id, order_date, order_amount,
       SUM(order_amount) OVER (ORDER BY order_date) AS cumulative_amount
FROM orders
WHERE customer_id = 1;
```

This query calculates the cumulative sum of `order_amount` for a specific customer, ordered by the `order_date`.

**Window Function Example: Moving Average**

```sql
SELECT order_date, order_amount,
       AVG(order_amount) OVER (ORDER BY order_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM orders;
```


This query calculates a 3-day moving average of `order_amount`, including the current day and the two preceding days.
---
By mastering these 10 SQL statements, you'll be able to handle 90% of your data science tasks efficiently.
---

`thanks`
