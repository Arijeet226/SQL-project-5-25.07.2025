# SQL-project-5-25.07.2025
# Background
This is a powerful SQL project – “Customer Purchase Portfolio Analysis”
How to analyze Customers, Orders, and Products data
Use of SQL JOINs, GROUP BY, COUNT, SUM, and other key functions
How to extract meaningful insights like most loyal customers, highest spenders, and purchase patterns
### The questions I wanted to answer through my SQL queries were:
## Q1 Q1.TOTAL ORDER PLACED PER CUSTOMER
```sql
SELECT customer_id,COUNT(*) AS order_count
FROM  orders
GROUP BY customer_id;
```
## Q2.TOTAL QUANTITY PURCHASED BY CUSTOMERS
```sql
SELECT customer_id,SUM(quantity) AS quantity_purchased
FROM orders
GROUP BY customer_id;
```
![](https://github.com/Arijeet226/SQL-project-4-23.07.2025/blob/ce3a0e87e0f30f791cd3557665b60ad205cff18b/graphics/TICKET_SOLD.png)
## Q3.REVENUE PER CUSTOMER
```sql
SELECT c.customer_id, CONCAT(c.first_name,' ',c.last_name) AS customer_name,
SUM(o.quantity*p.unit_price) AS revenue
FROM orders o
JOIN customers c ON o.customer_id=c.customer_id
JOIN products p ON o.product_id=p.product_id
GROUP BY c.customer_id
ORDER BY revenue DESC;
```
## Q4.MONTHLY REVENUE TREND
```sql
SELECT SUM(o.quantity*p.unit_price)AS revenue,DATE_FORMAT(order_date,'%y-%m')AS month
FROM  orders o
JOIN products p ON o.product_id=p.product_id
GROUP BY month
ORDER BY month DESC;
```
## Q5.TOP SELLING PRODUCT
```sql
SELECT p.name,SUM(o.quantity) AS unit_sold
FROM orders o
JOIN products p ON o.product_id=p.product_id
GROUP BY p.name
ORDER BY unit_sold DESC
LIMIT 5;
```
## Q6.PRODUCT NEVER ORDERED
```sql
SELECT product_id,name
FROM products
WHERE product_id NOT IN(SELECT DISTINCT product_id FROM orders);
```
![](https://github.com/Arijeet226/SQL-project-4-23.07.2025/blob/ce3a0e87e0f30f791cd3557665b60ad205cff18b/graphics/TOTAL%20FLIGHTS.png)
## Q7.AVERAGE BASKET SIZE PER CUSTOMER
```sql
SELECT customer_id,ROUND(AVG(quantity),2) AS avg_quantity
FROM orders
GROUP BY customer_id;
```
![](https://github.com/Arijeet226/SQL-project-4-23.07.2025/blob/ce3a0e87e0f30f791cd3557665b60ad205cff18b/graphics/PRICE%20paid%20by%20ticket_id.png)
## Q8.TOTAL REVENUE BY PRODUCT CATEGORY
```sql
SELECT p.category,ROUND(SUM(o.quantity*p.unit_price),2) AS revenue
FROM orders o
JOIN products p ON o.product_id=p.product_id
GROUP BY category
ORDER BY revenue DESC;
```
![](https://github.com/Arijeet226/SQL-project-4-23.07.2025/blob/ce3a0e87e0f30f791cd3557665b60ad205cff18b/graphics/membership.png)
## Q9.DAILY ORDER AND REVENUE FOR A GIVEN WEEK(2024-06-07)TO(2024-07-13)
```sql
SELECT o.order_date,COUNT(*)AS orders,SUM(o.quantity*p.unit_price) AS revenue
FROM orders o
JOIN products p ON o.product_id=p.product_id
WHERE order_date BETWEEN '2024-06-07' AND '2024-06-13'
GROUP BY order_date;
```
## Q10.AVERAGE ORDER VALUE
```sql
SELECT (ROUND(SUM(o.quantity*p.unit_price),2))/(COUNT(DISTINCT order_id))AS avg_order_value
FROM orders o
JOIN products p
ON o.product_id=p.product_id;
```
