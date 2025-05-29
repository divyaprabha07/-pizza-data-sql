# -pizza-data-sql
here i used pizza sales dataset in csv file format .after cleaning and check the data type ,import the data into postgresql.
ensure all the columns are same as csv file.
then i write a query using  WHERE,ORDER BY,GROUP BY clauses to get top 5 most oredered pizzas.
![image alt](https://github.com/divyaprabha07/-pizza-data-sql/blob/cfaca035e53c843b0e4abcd81684fb82d87532f5/Screenshot%20(6).png)
then i create one table (pizza_info) after joined to pizza dataset.i am using INEER,RIGHT,LEFT joins.

![Screenshot (8)](https://github.com/user-attachments/assets/f78b6816-c967-4165-b26b-9a1ae14e3402)


i write a subquery to  Find pizzas that sold more than the average total orders.

-- Find pizzas that sold more than the average total orders
SELECT pizza_name, total_quantity
FROM (
    SELECT pizza_name, SUM(quantity) AS total_quantity
    FROM pizza_dataset
    GROUP BY pizza_name
) AS pizza_totals
WHERE total_quantity > (
    SELECT AVG(quantity)
    FROM pizza_dataset
);

after that create a view using this code
-- View for monthly sales summary
CREATE VIEW monthly_sales_summary AS
SELECT 
    DATE_TRUNC('month', order_date::DATE) AS month,
    SUM(quantity) AS total_pizzas_sold,
    SUM(total_price) AS total_revenue
FROM pizza_dataset
GROUP BY month
ORDER BY month;
