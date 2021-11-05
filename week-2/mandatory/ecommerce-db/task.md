# E-Commerce Database

In this homework, you are going to work with an ecommerce database. In this database, you have `products` that `consumers` can buy from different `suppliers`. Customers can create an `order` and several products can be added in one order.

## Submission

Below you will find a set of tasks for you to complete to set up a databases of students and mentors.

To submit this homework write the correct commands for each question here:

```sql
--Retrieve all the customers names and addresses who lives in United States
select name, address from customers where country = 'United States' ;

--Retrieve all the customers ordered by ascending name
select * from customers order by name;

--Retrieve all the products which cost more than 100
select * from products where unit_price > 100;

--Retrieve all the products whose name contains the word socks
select * FROM products WHERE product_name LIKE '%socks%';

--Retrieve the 5 most expensive products
select * from  products 
order by unit_price desc 
fetch first 5 rows only;

--Retrieve all the products with their corresponding suppliers. 
--The result should only contain the columns product_name, unit_price and supplier_name
select p.product_name, p.unit_price, s.supplier_name from products p 
join suppliers s on p.supplier_id =s.id;  

--Retrieve all the products sold by suppliers based in the United Kingdom. 
--The result should only contain the columns product_name and supplier_name
select p.product_name, s.supplier_name from products p 
join suppliers s on p.supplier_id = s.id 
where s.country = 'United Kingdom';

--Retrieve all orders from customer ID 1
select * from orders where customer_id = 1;

--Retrieve all orders from customer named Hope Crosby
select * from orders o join customers c on o.customer_id = c.id 
where c.name = 'Hope Crosby';

--Retrieve all the products in the order ORD006. 
--The result should only contain the columns product_name, unit_price and quantity.
select p.product_name, p.unit_price, oi.quantity from orders o  
join order_items oi on oi.order_id = o.id 
join products p on oi.product_id =p.id
where o.order_reference = 'ORD006';

--Retrieve all the products with their supplier for all orders of all customers. 
--The result should only contain the columns name (from customer), order_reference order_date,
-- product_name, supplier_name and quantity.
select c.name, o.order_reference, o.order_date, p.product_name, s.supplier_name, oi.quantity 
from suppliers s  
join products p on p.supplier_id = s.id 
join order_items oi on oi.product_id = p.id 
join orders o on oi.order_id = o.id 
join customers c on o.customer_id = c.id;

```

When you have finished all of the questions - open a pull request with your answers to the `Databases-Homework` repository.

## Setup

To prepare your environment for this homework, open a terminal and create a new database called `cyf_ecommerce`:

```sql
createdb cyf_ecommerce
```

Import the file [`cyf_ecommerce.sql`](./cyf_ecommerce.sql) in your newly created database:

```sql
psql -d cyf_ecommerce -f cyf_ecommerce.sql
```

Open the file `cyf_ecommerce.sql` in VSCode and make sure you understand all the SQL code. Take a piece of paper and draw the database with the different relations between tables. Identify the foreign keys and make sure you understand the full database schema.

## Task

Once you understand the database that you are going to work with, solve the following challenge by writing SQL queries using everything you learned about SQL:

1. Retrieve all the customers names and addresses who lives in United States
2. Retrieve all the customers ordered by ascending name
3. Retrieve all the products which cost more than 100
4. Retrieve all the products whose name contains the word `socks`
5. Retrieve the 5 most expensive products
6. Retrieve all the products with their corresponding suppliers. The result should only contain the columns `product_name`, `unit_price` and `supplier_name`
7. Retrieve all the products sold by suppliers based in the United Kingdom. The result should only contain the columns `product_name` and `supplier_name`.
8. Retrieve all orders from customer ID `1`
9. Retrieve all orders from customer named `Hope Crosby`
10. Retrieve all the products in the order `ORD006`. The result should only contain the columns `product_name`, `unit_price` and `quantity`.
11. Retrieve all the products with their supplier for all orders of all customers. The result should only contain the columns `name` (from customer), `order_reference` `order_date`, `product_name`, `supplier_name` and `quantity`.
12. Retrieve the names of all customers who bought a product from a supplier from China.
