# 🍕 Pizza Sales Analysis using SQL

This project focuses on analyzing pizza sales data using **SQL queries**.  
The goal is to extract valuable insights such as total orders, revenue, most popular pizzas, and revenue contribution of each category.  

The dataset contains details of **orders, order details, pizzas, and pizza types**.  
By writing SQL queries, we can answer important business questions and support data-driven decision-making.

---

##  Table of Contents
1. About the Project
2. Dataset
3. Tools & Technologies
4. SQL Queries
5. Insights
6. How to Run 
7. License

---

##  About the Project
The purpose of this project is to:
- Analyze customer orders  
- Identify top-performing pizzas  
- Understand sales distribution by category  
- Calculate revenue contribution of each pizza type  

This analysis can help a pizza business optimize its menu, pricing, and marketing strategies.  

---

## 📊 Dataset
The dataset consists of four tables:  

- **orders** → Contains order IDs and order dates  
- **order_details** → Links each order with pizzas and their quantities  
- **pizzas** → Includes pizza IDs, prices, and size information  
- **pizza_types** → Contains pizza categories and names  

---

## 🛠 Tools & Technologies
- **SQL (MySQL / PostgreSQL / SQLite)** – For querying the dataset  
- **Markdown** – For project documentation  
- **GitHub** – To share and version control the project  

---

## 🧩 SQL Queries

### 1. Retrieve the total number of orders placed
```sql
SELECT COUNT(order_id) AS Total_Orders
FROM orders;
```

---

### 2. Calculate the total revenue generated from pizza sales
```sql
SELECT 
     ROUND(SUM(order_details.quantity * pizzas.price),2) AS Total_Revenue
FROM order_details 
JOIN pizzas
ON order_details.pizza_id = pizzas.pizza_id;
```

---

### 3. Identify the highest-priced pizza
```sql
SELECT pizza_types.name, pizzas.price
FROM pizza_types 
JOIN pizzas
ON pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY price DESC 
LIMIT 1;
```

---

### 4. Find the total quantity of each pizza category ordered
```sql
SELECT pizza_types.category, SUM(order_details.quantity) AS quantity
FROM pizza_types 
JOIN pizzas
ON pizza_types.pizza_type_id = pizzas.pizza_type_id
JOIN order_details
ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.category 
ORDER BY quantity DESC;
```

---

### 5. List the top 5 most ordered pizza types along with their quantities
```sql
SELECT pizza_types.name, SUM(order_details.quantity) AS Quantity
FROM pizza_types 
JOIN pizzas
ON pizza_types.pizza_type_id = pizzas.pizza_type_id
JOIN order_details
ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY Quantity DESC 
LIMIT 5;
```

---

### 6. Calculate the percentage contribution of each pizza type to total revenue
```sql
SELECT pizza_types.category, 
       SUM(order_details.quantity * pizzas.price) / 
       (SELECT ROUND(SUM(order_details.quantity * pizzas.price),2) 
        FROM order_details 
        JOIN pizzas
        ON order_details.pizza_id = pizzas.pizza_id) * 100 AS Revenue
FROM pizza_types 
JOIN pizzas
ON pizza_types.pizza_type_id = pizzas.pizza_type_id
JOIN order_details 
ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.category 
ORDER BY Revenue;
```

---

### 7. Determine the top 3 most ordered pizza types based on revenue
```sql
SELECT pizza_types.name, SUM(order_details.quantity * pizzas.price) AS Revenue
FROM pizza_types 
JOIN pizzas
ON pizza_types.pizza_type_id = pizzas.pizza_type_id
JOIN order_details 
ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name 
ORDER BY Revenue DESC 
LIMIT 3;
```

---

## 📈 Insights
- **Total Orders** → Helps understand customer demand.  
- **Total Revenue** → Provides overall sales performance.  
- **Highest Priced Pizza** → Identifies premium offerings.  
- **Category-wise Quantity** → Shows which category is most popular.  
- **Top 5 Ordered Pizzas** → Highlights best-selling items.  
- **Revenue Contribution by Category** → Helps in menu optimization.  
- **Top 3 by Revenue** → Reveals the most profitable pizzas.  

---

## 🚀 How to Run
1. Load the pizza sales dataset into your SQL database (MySQL, PostgreSQL, etc.).  
2. Copy the queries from this repository.  
3. Run the queries in your SQL editor.  
4. Analyze the results and compare insights.  

---







