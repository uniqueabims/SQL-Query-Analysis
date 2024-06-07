### SQL Query Analysis for Car Sales Data
### Introduction

This section includes a series of SQL questions answered as part of a comprehensive data analysis project. Each question was designed to address specific business needs and extract meaningful insights from a large dataset. 

**Question 1: Pull Unique Product Lines**
- **Objective**: Identify and retrieve unique product lines used in production.
- **SQL Query**:
    ```sql
    SELECT DISTINCT productline
    FROM products;
    ```
- **Explanation**: This query retrieves distinct values from the `productline` column in the `products` table, ensuring that each product line is listed only once.
- **Result**: A list of unique product lines used in production.

**Question 2: Information on Shipped Orders by Customer 103**
- **Objective**: Show details of shipped orders made by customer number 103.
- **SQL Query**:
    ```sql
    SELECT 
        customers.customerNumber,
        orders.orderNumber,
        orders.orderDate,
        orders.status
    FROM 
        customers
    JOIN 
        orders ON customers.customerNumber = orders.customerNumber
    WHERE 
        customers.customerNumber = 103
        AND orders.status = 'Shipped';
    ```
- **Explanation**: This query joins the `customers` and `orders` tables to retrieve orders for customer number 103 where the status is 'Shipped'.
- **Result**: A table containing customer number, order number, order date, and status for shipped orders by customer 103.

**Question 3: Retrieve Specific Job Titles**
- **Objective**: Retrieve employees holding the job titles "Sales Rep" or "Marketing Manager".
- **SQL Query**:
    ```sql
    SELECT *
    FROM employees
    WHERE jobTitle 
    IN ("Sales Rep", "Marketing Manager");
    ```
- **Explanation**: This query filters the `employees` table to select only those with the job titles "Sales Rep" or "Marketing Manager".
- **Result**: A list of employees who are either Sales Reps or Marketing Managers.

**Question 4: Customers in USA with High Credit Limit**
- **Objective**: Show information about customers in the USA with a credit limit above $100,000.
- **SQL Query**:
    ```sql
    SELECT contactLastName, contactFirstName, creditLimit
    FROM customers
    WHERE country = "USA"
    AND creditlimit > "100000"
    ORDER BY contactLastName ASC;
    ```
- **Explanation**: This query retrieves customers from the `customers` table who reside in the USA and have a credit limit over $100,000, sorted by last name.
- **Result**: A sorted list of customer last names, first names, and credit limits for high-credit customers in the USA.

**Question 5: Number of Products by Product Line**
- **Objective**: Show the number of products produced using various product lines.
- **SQL Query**:
    ```sql
    SELECT productLine, COUNT(productCode) AS number_of_products
    FROM products
    GROUP BY productLine;
    ```
- **Explanation**: This query groups the `products` table by `productLine` and counts the number of products in each line.
- **Result**: A table showing the number of products for each product line.

**Question 6: Total Units Sold for Each Product**
- **Objective**: Calculate the total number of units sold for each product, filtering results to include products with more than 500 units sold.
- **SQL Query**:
    ```sql
    SELECT productName, SUM(quantityInStock) as total_units_sold
    FROM products
    GROUP BY productName
    HAVING total_units_sold > 500
    ORDER BY total_units_sold;
    ```
- **Explanation**: This query sums the `quantityInStock` for each `productName`, filters for products with more than 500 units sold, and orders the results by the total units sold.
- **Result**: A list of products with total units sold greater than 500.

**Question 7: Number of Employees per Office**
- **Objective**: Determine the number of employees in each office.
- **SQL Query**:
    ```sql
    SELECT e.officeCode, o.city, o.country, COUNT(employeenumber) as total_employees
    FROM employees as e
    INNER JOIN offices as o
    ON e.officeCode = o.officeCode 
    GROUP BY e.officeCode, o.officecode, o.city, o.country;
    ```
- **Explanation**: This query joins the `employees` and `offices` tables to count the number of employees in each office, grouped by office code, city, and country.
- **Result**: A table showing the number of employees in each office.

**Question 8: Number of Orders by Customer**
- **Objective**: Identify the number of orders made by each customer and determine which customer made the most orders.
- **SQL Query**:
    ```sql
    SELECT c.customerNumber, c.customerName, COUNT(orderNumber) AS number_of_orders
    FROM customers AS c
    INNER JOIN orders AS o
    ON c.customerNumber = o.customerNumber
    GROUP BY c.customerNumber, c.customerName
    ORDER BY number_of_orders DESC;
    ```
- **Result**: A table showing customer number, customer name, and the number of orders made by each customer, sorted by the number of orders.

- **Top Customer**:
    ```sql
    SELECT c.customerNumber, c.customerName, COUNT(orderNumber) AS number_of_orders
    FROM customers AS c
    INNER JOIN orders AS o
    ON c.customerNumber = o.customerNumber
    GROUP BY c.customerNumber, c.customerName
    ORDER BY number_of_orders DESC
    LIMIT 1;
    ```
- **Result**: The customer who made the most orders.

**Question 9: Comprehensive Customer Order History**
- **Objective**: Gain a comprehensive understanding of customers' order history, including those who have not yet placed any orders.
- **SQL Query**:
    ```sql
    SELECT c.customernumber, c.customername, o.orderdate
    FROM customers AS c
    LEFT JOIN orders as o
    ON c.customerNumber = o.customerNumber;
    ```
- **Result**: A table showing customer numbers, names, and order dates, including customers who have not placed any orders.

- **Active Customers**:
    ```sql
    SELECT c.customernumber, c.customername, o.orderdate
    FROM customers AS c
    LEFT JOIN orders as o
    ON c.customerNumber = o.customerNumber
    WHERE orderDate IS NOT NULL;
    ```
- **Result**: Customers who have placed orders.

- **Inactive Customers**:
    ```sql
    SELECT c.customernumber, c.customername, o.orderdate
    FROM customers AS c
    LEFT JOIN orders as o
    ON c.customerNumber = o.customerNumber
    WHERE orderDate IS NULL;
    ```
- **Result**: Customers who have not placed any orders.

**Question 10: Peak Shipped Order Times**
- **Objective**: Determine the year, month, and day of the week with the most shipped orders.
- **SQL Query**:
    ```sql
    SELECT DAYNAME(shippedDate) AS Day, MONTHNAME(shippedDate) AS Month, YEAR(shippedDate) AS Year, COUNT(status) as most_order
    FROM orders
    GROUP BY shippedDate
    HAVING shippedDate IS NOT NULL
    ORDER BY most_order DESC;
    ```
- **Explanation**: This query groups the `orders` table by shipped date and counts the number of shipped orders to find the peak times.
- **Result**: A table showing the day, month, and year with the most shipped orders.
