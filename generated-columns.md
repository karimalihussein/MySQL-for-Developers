# 1.11 : Generated columns

## How to use generated columns in MySQL

- MySQL is a powerful database management system that offers a wide range of features to make it easy for developers to work with data. One of the many features available is generated columns, which can help to automate certain tasks and calculations.

In this post, we're going to look at what generated columns are, how to use them, and some common use cases.


## What are generated columns?

- Generated columns are a way to make MySQL do more work on your behalf, by allowing you to create columns that are based on other columns in your table. Essentially, a generated column is a column that is computed by an expression, rather than being explicitly stored in the table.

The idea is that you can define a column using a formula or calculation, and MySQL will automatically calculate the values for that column based on the data in other columns.



## Example: creating a table with generated columns

- Let's take a look at an example of how to create a table with generated columns. In this example, we're going to create a table called emails, which will have two columns - email and domain.

The email column is a varchar(255), which represents an email address. The domain column will be generated based on the contents of the email column.

To create the generated column, we'll use the AS keyword and a function called substring index. The substring index function allows us to extract the domain from the email address.

Here's what the SQL code looks like:

```sql
CREATE TABLE emails (
  email VARCHAR(255),
  domain VARCHAR(255) AS (SUBSTRING_INDEX(email, '@', -1))
);

INSERT INTO emails (email) VALUES ('karim@gmail.com');

SELECT * FROM emails;

+-------------------+----------+
| email             | domain   |
+-------------------+----------+
| karim@gmail.com  | gmail.com |
+-------------------+----------+
1 row in set (0.00 sec)
```

- As you can see, the domain column is automatically populated with the domain name from the email address. This is a great example of how generated columns can help to automate certain tasks and calculations.

- In this example, we used the substring index function to extract the domain name from the email address. However, there are many other functions that can be used to create generated columns, such as the concat function, which allows you to combine two or more columns into a single column.

- you cannot insert data into a generated column. This is because the value of a generated column is calculated based on the data in other columns, and is not explicitly stored in the table.

- You can also use generated columns to perform calculations on data. For example, you could create a column that calculates the total price of an order, based on the price of each item in the order.

Notice that the domain column is defined as varchar(255) AS (substring_index(email, '@', -1)). This means that the value of the domain column will be computed based on the contents of the email column, using the substring_index function.

## Virtual vs. stored generated columns

- One important thing to note about generated columns is that they can be either virtual or stored.

A virtual column is calculated at runtime and does not take up any space on the disk. This means that it may take longer to calculate, but it doesn't impact the overall size of the table.

A stored column, on the other hand, is calculated during data insertion or update and saved to disk, just like a regular column. This means that it might be faster to retrieve data from a stored column, but it will take up more space on the disk.

When creating a generated column, you can specify whether it should be virtual or stored by using the VIRTUAL or STORED keyword. If you don't specify anything, the column will default to being virtual.



## Example: creating a virtual column

- Let's take a look at an example of how to create a virtual column. In this example, we're going to create a table called orders, which will have two columns - id and total.

The id column is an integer that represents the order ID. The total column will be a virtual column that calculates the total price of the order, based on the price of each item in the order.

To create the virtual column, we'll use the AS keyword and a function called sum. The sum function allows us to add up the values in a column.

Here's what the SQL code looks like:

```sql
CREATE TABLE orders (
  id INT,
  price DECIMAL(10,2),
  quantity INT,
  total DECIMAL(10,2) GENERATED ALWAYS AS (price * quantity) STORED
);

INSERT INTO orders (id, price, quantity) VALUES (1, 10.00, 2);

SELECT * FROM orders;

+----+-------+----------+-------+
| id | price | quantity | total |
+----+-------+----------+-------+
|  1 | 10.00 |        2 | 20.00 |
+----+-------+----------+-------+
1 row in set (0.00 sec)
```

- As you can see, the total column is automatically populated with the total price of the order. This is a great example of how generated columns can help to automate certain tasks and calculations.

- In this example, we used the sum function to add up the price of each item in the order. However, there are many other functions that can be used to create generated columns, such as the concat function, which allows you to combine two or more columns into a single column.

- you cannot insert data into a generated column. This is because the value of a generated column is calculated based on the data in other columns, and is not explicitly stored in the table.

-------
## Use cases for generated columns

### There are many potential use cases for generated columns. Here are a few examples:

* Extracting data from JSON objects - If you have a column that contains a big JSON blob, you can use a generated column to extract a specific key from the blob and create a new column with just that data. This can make it easier to query the data and improve performance.

* Performing calculations - You can use generated columns to perform calculations such as converting units, applying tax rates, and more. This can be useful for creating reports or performing other data analysis tasks.

* Normalizing data - If you have a column that contains redundant data, you can use a generated column to extract that data and create a new table with just the unique values. This can make it easier to manage your data and eliminate redundancy.


------

## Summary

- Generated columns are a powerful feature of MySQL that can help you automate certain tasks and calculations. By defining a column using a formula or calculation, you can save yourself time and effort, and ensure that your data is always up-to-date.

In this post, we covered the basics of generated columns, including how to create them, the differences between virtual and stored columns, and some common use cases. We hope you found this post informative and useful, and that you'll consider using generated columns in your own MySQL database.










