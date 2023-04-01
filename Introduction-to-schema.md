## 1.1 : Introduction to schema

- The importance of schema design in database performance

* Before we dive into query optimization, indexes, and other fun stuff, let's take a step back and talk about an often overlooked aspect of database performance: schema design. Schema refers to the structure of your database tables, including column types, sizes, and attributes. Your schema can either set you up for success or cause problems down the road, so it's important to get it right from the start.


----
## Writing a schema

- When it comes to creating your schema, you have two options: write the definitions by hand or let your framework generate them. While both methods are valid, letting your framework generate the schema can save you some time and effort. However, it's important to remember that you are still ultimately responsible for the schema, regardless of how it's created.

MySQL offers a variety of data types, and we'll cover most of them in detail later on. But before we do, it's important to keep three guiding principles in mind when choosing a data type:

- Use the smallest data type that will work for your data. For example, if you have a column that will only ever contain numbers between 0 and 255, you should use the TINYINT data type instead of INT. This will save you a lot of space in your database.

1 - Pick the smallest data type that will hold all of your data
2 - Pick the simplest column type that accurately reflects your data (e.g. use a numeric type for numbers, not a string)
3 - Ensure your schema accurately reflects the reality of your data (e.g. don't make a non-nullable column nullable)

- The first principle is pretty straightforward: use the smallest data type that will work for your data.
- The second principle is a bit more nuanced.

-- By following these principles, you can create a compact and efficient schema that accurately reflects your data. This will make your database faster and easier to maintain.

----
## Why schema design matters

You may be thinking, "disks are cheap, why does compactness matter?" While it's true that disks are relatively inexpensive, compactness can improve database performance in several ways:

Faster data access: The more compact your schema is, the faster the database can access the data. This is because the database doesn't need to spend extra time searching for the data within larger column types.
Efficient indexing: When it comes time to create indexes, a compact schema can improve index speed and efficiency. This is because indexes are stored in memory, and a smaller schema means less memory usage.
In other words, optimizing your schema isn't about minimizing disk space usage, but rather enabling the database to access and index your data more efficiently.

----
## Common data types

Now that we know why schema design matters, let's take a closer look at some of the most common data types in MySQL:

- INT: This is the most common numeric data type in MySQL. It can hold numbers between -2147483648 and 2147483647. If you need to store larger numbers, you can use the BIGINT data type, which can hold numbers between -9223372036854775808 and 9223372036854775807.

- VARCHAR: This is the most common string data type in MySQL. It can hold strings up to 65535 characters in length. If you need to store longer strings, you can use the TEXT data type, which can hold strings up to 4294967295 characters in length.

- DATETIME: This is the most common date/time data type in MySQL. It can hold dates between 1000-01-01 00:00:00 and 9999-12-31 23:59:59. If you need to store dates before 1000 AD or after 9999 AD, you can use the TIMESTAMP data type, which can hold dates between 1970-01-01 00:00:01 UTC and 2038-01-19 03:14:07 UTC.

- DECIMAL: This is the most common decimal data type in MySQL. It can hold numbers between -99999999999999999999999999999.99999999999999999999999999999 and 99999999999999999999999999999.99999999999999999999999999999. If you need to store larger numbers, you can use the DOUBLE data type, which can hold numbers between -1.7976931348623157E+308 and 1.7976931348623157E+308.

- FLOAT: This is the most common floating point data type in MySQL. It can hold numbers between -3.402823466E+38 and -1.175494351E-38, 0 and 1.175494351E-38, and 1.175494351E-38 and 3.402823466E+38. If you need to store larger numbers, you can use the DOUBLE data type, which can hold numbers between -1.7976931348623157E+308 and 1.7976931348623157E+308.

When choosing a data type, it's important to consider your data and choose the simplest and smallest type that accurately represents it. For example, if you're storing ages, you may choose an INT type rather than a VARCHAR type, as integer values are simpler and more compact.


----
## Conclusion

While schema design may not be the most glamorous aspect of database development, it's a crucial one that can significantly impact your database's performance. By following the three guiding principles of compactness, simplicity, and accuracy, you can create a schema that effectively reflects your data and enables fast data access and indexing.

