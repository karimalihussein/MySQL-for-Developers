## 1.3 : Decimals

## Storing decimals in MySQL

MySQL does not have a native decimal type. Instead, it uses the `FLOAT` and `DOUBLE` types. These types are not suitable for storing monetary values, because of the way they are stored internally. The `FLOAT` type is stored as a 4-byte floating point number, and the `DOUBLE` type is stored as an 8-byte floating point number. This means that the precision of the `FLOAT` type is limited to 7 decimal places, and the precision of the `DOUBLE` type is limited to 15 decimal places. This is not enough precision for storing monetary values.

If you're working on a project that requires the storage of decimal values, you may wonder what the best practice is for MySQL. You don't want to end up with inaccurate or imprecise data, and your choice of data type can make a big difference. In this video, we'll explore the different options you have for storing decimals in MySQL and when to use each one.

## The four types of decimal data types

- There are four different types of data types in MySQL that can store decimal values:
  1 - DECIMAL: a fixed-precision data type that stores exact values.
  2 - NUMERIC: an alias for DECIMAL, the two are the same thing in MySQL.
  3 - FLOAT: a floating-point data type that stores approximate values.
  4 - DOUBLE: a floating-point data type that stores larger and more precise values than FLOAT.
- Each of these data types has its own use case, and which one you choose depends on the precision and accuracy you require. Let's take a look at each one in more detail.

## DECIMAL

- The DECIMAL data type is the most accurate data type for storing decimal values. It stores exact values, and it's the only data type that can store values with a precision of 65 digits. This is the data type you should use if you need to store exact decimal values.

## NUMERIC

- The NUMERIC data type is an alias for DECIMAL. It's the same thing as DECIMAL, and it's included in MySQL for compatibility with other database systems. You can use NUMERIC in place of DECIMAL, and vice versa.

## FLOAT

- The FLOAT data type is a floating-point data type that stores approximate values. It's not as accurate as DECIMAL, but it's more efficient. It's the data type you should use if you need to store approximate decimal values.

## DOUBLE

- The DOUBLE data type is a floating-point data type that stores larger and more precise values than FLOAT. It's not as accurate as DECIMAL, but it's more efficient. It's the data type you should use if you need to store larger and more precise decimal values.

## When to use decimal

- If you need to store values that require absolute precision, such as currency or other financial data, you should use the DECIMAL data type. With DECIMAL, you can specify the maximum number of digits and how many digits should occur after the decimal point.

For example, suppose you want to store a maximum of 10 digits, with two digits after the decimal, the syntax would be:

`DECIMAL(10,2)`

- The first argument specifies the maximum number of digits, while the second argument specifies how many should appear after the decimal. The number of digits before the decimal is determined by the first value subtracted by the second.

## When to use float or double

If you don't require precise decimal values, you can use either FLOAT or DOUBLE. Both of these data types store approximate values, but DOUBLE can store larger and more precise values than FLOAT.

If you're using a data type for scientific calculations, where relative precision is more important than absolute precision, you might also consider using FLOAT or DOUBLE.

- Example

Let's see how these data types work in action. We'll create a table called decimals and insert data into two columns D1 and D2. Both columns will be defined as DOUBLE data types.

```sql
CREATE TABLE decimals (
  id INT AUTO_INCREMENT PRIMARY KEY,
  D1 DOUBLE,
  D2 DOUBLE,
);

INSERT INTO decimals (D1, D2)
VALUES (100.4, 20.4), (-80.0, 0.0);

SELECT * FROM decimals;
```

- Output

```sql
+----+-------+------+
| id | D1    | D2   |
+----+-------+------+
|  1 | 100.4 | 20.4 |
|  2 | -80.0 |  0   |
+----+-------+------+
```

- Now, if we try to add the values in columns D1 and D2, we might expect the result to be 40.8, but that's not what we get:

```sql
SELECT SUM(D1), SUM(D2) FROM decimals;
```

- Output

```sql
+------------------+----------+
| SUM(D1)          | SUM(D2)  |
+------------------+----------+
| 20.4000000000006 | 20.4     |
+------------------+----------+
```

- We can see that the sums are close to the expected result, but not exactly the same, and that's because DOUBLE is an approximation of a value, not an exact one. If we want to get the exact result, we need to use the DECIMAL data type.

## When to use numeric

- The NUMERIC data type is an alias for DECIMAL. It's the same thing as DECIMAL, and it's included in MySQL for compatibility with other database systems. You can use NUMERIC in place of DECIMAL, and vice versa.

## Conclusion

- In this lesson, we've explored the different types of decimal data types in MySQL. We've seen that DECIMAL is the most accurate data type for storing decimal values, and that FLOAT and DOUBLE are floating-point data types that store approximate values. We've also seen that NUMERIC is an alias for DECIMAL, and that it's included in MySQL for compatibility with other database systems.

When working with decimal values in MySQL, it's important to choose the correct data type for your needs. If you require absolute precision in your values, DECIMAL is the best choice. If you don't require exact values, FLOAT or DOUBLE may be more appropriate. Which one you choose just depends on the range of data you're storing and the amount of precision you need.

Remember, when working with FLOAT or DOUBLE, results will not be exactly precise, and values may be slightly different from what you expect.

## Exercise

- Create a table called employees with the following columns:
- id (an integer, primary key, and auto-incremented),
- name (a string),
- salary (a decimal with a maximum of 10 digits and 2 digits after the decimal point),

2 - Insert the following data into the employees table:

| id  | name | salary   |
| --- | ---- | -------- |
| 1   | John | 55000.50 |
| 2   | Mary | 67000.00 |
| 3   | Jane | 85000.75 |

3 - Display all the data in the employees table.
4 - Write a query to calculate the total salary of all employees.
5 - Write a query to calculate the sum of the salaries of all employees

- bonus
  6 - Create a new table called sales with the following columns:
- id (an integer, primary key, and auto-incremented),
- product (a string),
- price (a decimal with a maximum of 10 digits and 2 digits after the decimal point),
- quantity (an integer),

7 - Insert the following data into the sales table:

| id  | product | price | quantity |
| --- | ------- | ----- | -------- |
| 1   | Laptop  | 25.50 | 2        |
| 2   | Phone   | 17.75 | 3        |
| 3   | Tablet  | 20.86 | 4        |

8 - Write a query to calculate the total revenue generated by all sales.

## Solution

```sql
CREATE TABLE employees (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  salary DECIMAL(10,2)
);

INSERT INTO employees (name, salary)
VALUES ('John', 55000.50), ('Mary', 67000.00), ('Jane', 85000.75);

SELECT * FROM employees;

SELECT SUM(salary) FROM employees;

SELECT SUM(salary) AS total_salary FROM employees;

CREATE TABLE sales (
  id INT AUTO_INCREMENT PRIMARY KEY,
  product VARCHAR(255),
  price DECIMAL(10,2),
  quantity INT
);

INSERT INTO sales (product, price, quantity)
VALUES ('Laptop', 25.50, 2), ('Phone', 17.75, 3), ('Tablet', 20.86, 4);

SELECT SUM(price * quantity) AS total_revenue FROM sales;
```
