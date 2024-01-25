# java-DB-aggregate-function

1. Select the total number of Orders.
```
SELECT COUNT(*) AS TotalOrders
FROM Orders;
```
2. Select number of orders that have ship region.
```
SELECT COUNT(*) AS ShipRegionOrders
FROM Orders
WHERE ship_region IS NOT NULL
```
3. Select the most expensive product.
```
SELECT products.product_name, products.unit_price up
FROM products
ORDER BY up DESC
LIMIT 1;
```
4. Select total price of order with id = 10258;
```
SELECT SUM(unit_price * quantity) AS TotalPrice
FROM order_details
WHERE order_id = 10258;
```
5. Select the least expensive product from order with id = 10263
```
SELECT products.product_name AS LeastExpensiveProduct
FROM order_details od
JOIN products ON od.product_id = products.product_id
WHERE od.order_id = 10263;
```
6. Select all products that have price which is above the average price.
```
SELECT *
FROM Products
WHERE unit_price > (SELECT AVG(unit_price) FROM Products);
```
7. Calculate number of products from category Seafood.
```
SELECT COUNT(*) AS SeafoodProductsCount
FROM Products
WHERE category_id = (SELECT category_id FROM Categories WHERE category_name = 'Seafood');
```
8. Sumarize total value of products in orders made in 1996 (before discount).
```
SELECT SUM(od.unit_price * od.quantity) AS TotalValue
FROM order_details od
JOIN orders o ON od.order_id = o.order_id
WHERE o.order_date BETWEEN '1996-01-01' AND '1996-12-31';
```
