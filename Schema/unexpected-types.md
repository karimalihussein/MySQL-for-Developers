## 1.10: Unexpected types

## Data types you might not expect

- As a programmer, you're probably familiar with a variety of data types — strings, numbers, dates, and JSON, among others. But did you know that there are a few data types that are a little more unusual? In this video, we'll take a look at some of the more fun and wacky data types in MySQL.


## MySQL Booleans

- Let's start with booleans. While booleans are a common data type in many languages, MySQL doesn't actually have a native boolean type. Instead, MySQL uses a TINYINT column to simulate a boolean value.

However, you can still use the keyword BOOLEAN in your table definition, which will be interpreted as a TINYINT column. The BOOLEAN keyword is just a shorthand way of creating a tiny int column, defaulting to null.

You can also create a boolean value using a zero-length character column that's nullable. However, this method is less recommended as it can make your data look confusing and difficult to understand. It is neat though!

## Zip codes

- When it comes to USA zip codes, they are always 5 digits long. However, sometimes these codes may also include leading zeros. If you store these zip codes as integers, any leading zeros would be stripped, resulting in missing data.

As such, it's usually better to store zip codes as 5 character strings. However, if you need to store an extended zip code (which includes a dash and an additional 4 digits), you'll need to create a string column that's 10 characters long.

It's essential to understand data when it comes to zip codes, as there are exceptions to the rule. For example, there's a Saks Fifth Avenue in New York that has its own zip code: "10022-SHOE." Always make sure you have a good handle on your data before deciding how to store it.

## IP addresses

- Finally, let's take a look at IP addresses. While they usually appear as strings, you can also store them as integers for better organization and analysis.

MySQL has a built-in function INET_ATON() that converts an IPv4 address to an integer, and INET_NTOA() to convert an integer back to an IP address.

If you need to support both IPv4 and IPv6 addresses, you may need to use a binary column that's 16 bytes long.

## Summary
- exmaple of a boolean column and how it's stored in MySQL as a tiny int column with a default value of null and zip codes and how they're stored as strings and how to store IP addresses as integers 

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  is_admin BOOLEAN DEFAULT NULL,
  zip_code VARCHAR(5),
  ip_address INT UNSIGNED
);

INSERT INTO users (name, is_admin, zip_code, ip_address) VALUES
  ('John', TRUE, '10022', INET_ATON("127.0.0.1"));

SELECT * FROM users;

+----+------+---------+----------+------------+
| id | name | is_admin | zip_code | ip_address |
+----+------+---------+----------+------------+
|  1 | John |       1 |    10022 |  2130706433 |
+----+------+---------+----------+------------+
1 row in set (0.00 sec)

```

While these data types might seem a little strange, they are illustrative of a point that by understanding the implications of data types and storing data in the most efficient way possible, you can set yourself up for success when it comes to querying and analyzing your data.

So take the time to explore your data, think about the most efficient way to store it, and have fun with these unusual data types. You never know how they might come in handy!

