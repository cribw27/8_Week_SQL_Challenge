# Answers - Case Study #1 - Danny's Diner
#### Create Database and insert values
```sql
CREATE DATABASE dannys_diner;
USE dannys_diner;

CREATE TABLE sales (
  customer_id VARCHAR(1) NOT NULL,
  order_date DATE NOT NULL,
  product_id INTEGER NOT NULL
);

INSERT INTO sales (customer_id, order_date, product_id) VALUES
  ('A', '2021-01-01', 1),
  ('A', '2021-01-01', 2),
  ('A', '2021-01-07', 2),
  ('A', '2021-01-10', 3),
  ('A', '2021-01-11', 3),
  ('A', '2021-01-11', 3),
  ('B', '2021-01-01', 2),
  ('B', '2021-01-02', 2),
  ('B', '2021-01-04', 1),
  ('B', '2021-01-11', 1),
  ('B', '2021-01-16', 3),
  ('B', '2021-02-01', 3),
  ('C', '2021-01-01', 3),
  ('C', '2021-01-01', 3),
  ('C', '2021-01-07', 3);

CREATE TABLE menu (
  product_id INTEGER NOT NULL,
  product_name VARCHAR(5) NOT NULL,
  price INTEGER NOT NULL
);

INSERT INTO menu (product_id, product_name, price) VALUES
  (1, 'sushi', 10),
  (2, 'curry', 15),
  (3, 'ramen', 12);

CREATE TABLE members (
  customer_id VARCHAR(1) NOT NULL,
  join_date DATE NOT NULL
);

INSERT INTO members (customer_id, join_date) VALUES
  ('A', '2021-01-07'),
  ('B', '2021-01-09');
```
#### 1. What is the total amount each customer spent at the restaurant?

```sql
SELECT
  s.customer_id
  , SUM(m.price) AS total_spend
FROM dannys_diner.sales AS s
INNER JOIN dannys_diner.menu AS m 
  ON m.product_id = s.product_id
GROUP BY 1
ORDER BY 1;
```

#### 2.How many days has each customer visited the restaurant?

```sql
SELECT
  customer_id
  , COUNT(DISTINCT order_date) AS number_of_visits
FROM dannys_diner.sales
GROUP BY customer_id;
```

#### 3.What was the first item from the menu purchased by each customer?

```sql
WITH min_order_date AS (
  SELECT
    customer_id
    , MIN(order_date) AS min_order_date
  FROM dannys_diner.sales
  GROUP BY 1
)

SELECT
  DISTINCT s.customer_id
  , m.product_name
FROM dannys_diner.sales s
JOIN dannys_diner.menu m ON m.product_id = s.product_id
JOIN min_order_dates
	ON s.customer_id = min_order_dates.customer_id 
    AND s.order_date = min_order_dates.min_order_date
ORDER BY s.customer_id;
```

#### 4.What is the most purchased item on the menu and how many times was it purchased by all customers?

```sql

#### 5.Which item was the most popular for each customer?

```sql

#### 6.Which item was purchased first by the customer after they became a member?

```sql

#### 7.Which item was purchased just before the customer became a member?

```sql

#### 8.What is the total items and amount spent for each member before they became a member?

```sql

#### 9.If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?

```sql

#### 10.In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?

```sql
