# 1.7 Enums:

## The power of enums in MySQL

- When working with string data in MySQL, it's essential to ensure that you're storing valid data in your table columns. One way to do this is by using enums, a special data type that allows you to specify a predefined list of allowable values for a column. In this video, we'll explore the power of enums in MySQL and how you can use them to store and manage data more effectively.

## What are enums?

- Enums look like strings, but under the hood, they're stored as integers. Enums give you the readability of a string with the compact data type of an integer. An enum column has a predefined list of allowable values, and any attempt to enter a value outside this list will result in an error. This feature simplifies data validation in your database.

- To see how enums work, let's create an orders table with a size column declared as an ENUM. We'll pass through five different options that represent the allowable values for the column:

```sql
CREATE TABLE orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  size ENUM('extra small', 'small', 'medium', 'large', 'extra large')
);

INSERT INTO orders (size) VALUES ('small'), ('medium'), ('large');
```

- As you can see, we've inserted data into the size column using strings. However, if we perform a simple query that forces the values to be integers, we'll see that these strings are actually stored as integers under the hood:
```sql
SELECT size, size+0 FROM orders;

-- Output:

+--------+--------+
| size   | size+0 |
+--------+--------+
| small  |      2 |
| medium |      3 |
| large  |      4 |
+--------+--------+
```

- As you can see, the strings are stored as integers under the hood. This is because enums are stored as integers, and the values are assigned based on the order in which they're declared. In this case, 'extra small' is assigned a value of 1, 'small' is assigned a value of 2, and so on.


# Benefits of enums: Using enums in MySQL has several benefits, including:

- Data validation: As mentioned earlier, enums offer data validation, which helps to ensure that only valid data is entered into a column. When attempting to enter an invalid value, an error is thrown, preventing the data from being inserted into the database.

- Readability: Since enums allow you to store readable values in your database, it's easier to read the stored data at a glance. You don't need to memorize integers to understand the data; the values make sense in plain English.

- Compact data type: Enums are compact data types, which means they take up less storage space than other data types, such as strings. This feature makes them ideal for databases with large amounts of data.

- Downsides of enums: While enums offer several benefits, there are some downsides to using them, including:

- Changes to the schema: If a business requirement changes, and you need to add another option to the allowable values, you'll have to alter the schema of your table to add a new enum. While this process is not difficult, it can be inconvenient.

- Ordering: When sorting data using enums, MySQL sorts by the underlying integer value rather than the actual string. While this can be useful in some cases, it can also be quite confusing, especially if you're not expecting it.


- Using integer enums: Finally, it's important to note that integer enums can be confusing and should be avoided if possible. If you must use integer enums, it's best to use a TINYINT column instead.

- In this lesson, we've explored the power of enums in MySQL and how you can use them to store and manage data more effectively. Enums are a great way to simplify data validation in your database and ensure that only valid data is entered into your table columns. They also offer the readability of strings with the compact data type of integers. However, there are some downsides to using enums, including the fact that they can be confusing and that you can't add new options to the allowable values without altering the schema of your table. If you're working with string data in MySQL, enums are a great option to consider.


- Enums in MySQL are a powerful feature that can simplify database design, increase security, and improve readability. With a predefined list of allowable values for a column, the benefits of enums are clear. However, it's also important to keep in mind the limitations and potential drawbacks of using enums, such as the need to alter the schema if allowable values change. Overall, if used correctly, enums can be a valuable tool when working with string data in MySQL.
