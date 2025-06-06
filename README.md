# Task-4

**Step-by-Step SQL Tasks & Queries :-

1. Simple SELECT with WHERE, ORDER BY

-- Get top 5 most recent orders above $100
SELECT order_id, customer_id, order_date, total_amount
FROM orders
WHERE total_amount > 100
ORDER BY order_date DESC
LIMIT 5;
2. JOINs (INNER, LEFT, RIGHT)

-- INNER JOIN: Show order details with customer names
SELECT o.order_id, c.name AS customer_name, o.order_date, o.total_amount
FROM orders o
INNER JOIN customers c ON o.customer_id = c.customer_id;

-- LEFT JOIN: Show all customers and their orders (if any)
SELECT c.name, o.order_id, o.total_amount
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id;

-- RIGHT JOIN: Not available in SQLite; use LEFT JOIN from reverse
-- In MySQL or PostgreSQL:
SELECT o.order_id, c.name
FROM orders o
RIGHT JOIN customers c ON o.customer_id = c.customer_id;
3. Subqueries

-- Customers who made orders above the average order amount
SELECT name
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
    WHERE total_amount > (SELECT AVG(total_amount) FROM orders)
);
4. Aggregate Functions (SUM, AVG)

-- Total revenue by product category
SELECT p.category, SUM(oi.price * oi.quantity) AS total_revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.category
ORDER BY total_revenue DESC;
5. Create a View for Reusable Analysis

-- Create a view for monthly revenue
CREATE VIEW monthly_revenue AS
SELECT DATE_TRUNC('month', o.order_date) AS month, SUM(o.total_amount) AS revenue
FROM orders o
GROUP BY month
ORDER BY month;
To query the view:

SELECT * FROM monthly_revenue;
6. Query Optimization: Creating Indexes

-- Create index on customer_id for faster JOINs
CREATE INDEX idx_orders_customer_id ON orders(customer_id);

-- Create index on order_date for faster time-based queries
CREATE INDEX idx_orders_order_date ON orders(order_date);

*** Task 4: SQL for Data Analysis – Work Summary
In this task, I performed data analysis using SQL on an eCommerce database. The goal was to extract useful business insights by writing various types of SQL queries. I used MySQL (or PostgreSQL/SQLite) to write and execute the queries.

** Data Extraction:

Used SELECT, WHERE, and ORDER BY to retrieve filtered and sorted data from the tables.

Example: Found top 5 most recent orders above a certain amount.

** Joins for Combining Data:

Performed INNER JOIN, LEFT JOIN, and RIGHT JOIN to combine data from multiple related tables.

Example: Joined orders with customers to get customer names for each order.

** Subqueries:

Wrote subqueries to analyze data based on other derived results.

Example: Found customers who spent more than the average order value.

** Aggregate Functions:

Used functions like SUM() and AVG() with GROUP BY to calculate totals and averages.

Example: Calculated total revenue per product category.

** Views:

Created a reusable SQL VIEW for monthly revenue analysis.

Example: Monthly summary of total order amounts.

** Optimization:

Created INDEX on important columns to improve query performance.

Example: Indexed customer_id and order_date for faster access.


** Outcome:
Through this task, I learned how to manipulate and analyze structured data using SQL. It helped me understand how real-world data is stored in relational databases and how to extract meaningful insights efficiently.
