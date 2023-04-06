## 1.2 : Integers

### Understanding integers: types and ranges

- When it comes to databases, one of the most important aspects is understanding the different data types that can be used to store information. In this video, we'll focus specifically on integers, the different types of columns that can hold integer values, and the ranges for each.

-----
## Getting started.

- To demonstrate the different types of columns that can hold integer values, we'll be using a simple example: a books table. The table has an ID and a title, and we'll be defining the number of pages column. Before we can do that, however, we need to figure out the data type and any other attributes that are required. 

-----
## Types of columns that hold integer values.
  There are five data types that can be used to store integers: 

* TINYINT
* SMALLINT
* MEDIUMNINT
* INT
* BIGINT

It's worth noting that any other types of integers that you come across are likely aliases, meaning that they're just different words that refer to the same data type. For example, "integer" is simply another word for "int".

-----
## Ranges for each data type.

- Each data type for integers has different storage requirements, which means that they're able to store different amounts of data. Here are the ranges for each data type:

------------------------------------------------------------------------------------------------------------
| Data Type | Storage Requirements | Minimum Signed | Maximum Signed | Minimum Unsigned | Maximum Unsigned |
|-----------|----------------------|----------------|----------------|------------------|------------------|
| TINYINT   | 1 byte               | -128           | 127            | 0                | 255              |
| SMALLINT  | 2 bytes              | -32,768        | 32,767         | 0                | 65,535           |
| MEDIUMINT | 3 bytes              | -8,388,608     | 8,388,607      | 0                | 16,777,215       |
| INT       | 4 bytes              | -2,147,483,648 | 2,147,483,647  | 0                | 4,294,967,295    |
| BIGINT    | 8 bytes              | -2^63          | 2^63-1         | 0                | 2^64-1           |
------------------------------------------------------------------------------------------------------------

-----
## Understanding negative numbers.

- In databases, negative numbers are supported by dedicating one of the bits to the sign (either positive or negative), with the remaining bits reserved for the value. For example, a TINYINT with negative numbers enabled has one bit dedicated to the sign and seven bits for the value, which means it can store values from -128 to 127.

-----
## Defining the number of pages column.

- For our books table, we'll be defining the number of pages column, which we expect will never exceed 65,000 pages. Given this, we don't need to use the INT data type, which can hold up to 4.2 billion values. Instead, we can use the SMALLINT data type, which occupies two bytes and can store values from 0 to 65,535.

However, we also need to specify that negative numbers aren't supported for this column. We can do this by adding the unsigned keyword, which tells MySQL that we're not interested in negative numbers.

-----
## Common misconception: INT(11)

- It's common to see something like INT(11) and assume that the 11 controls the range of data that can be stored. However, the number in parentheses has no effect on the underlying storage or the range of the column. This notation was only ever intended to define a display width. It is deprecated and will be removed soon.

-----

## Summary

- In this lesson, we learned about the different types of columns that can hold integer values, and the ranges for each. We also learned about negative numbers and how they're stored in databases, and we defined the number of pages column for our books table.


## Conclusion
 
- Understanding the different types of columns that can hold integer values and their respective ranges is crucial to designing a database schema that's both efficient and scalable. By selecting the appropriate data type for each column, we can avoid unnecessary storage requirements and ensure efficient queries.


## Exercise: 
- In this exercise, we'll be creating a books table with an ID, title, and number of pages column. The number of pages column should be defined as a SMALLINT and should not allow negative numbers.

## Solution:


```sql
CREATE TABLE books (
  id INT(11) NOT NULL AUTO_INCREMENT,
  title VARCHAR(255) NOT NULL,
  number_of_pages SMALLINT(5) UNSIGNED NOT NULL,
  PRIMARY KEY (id)
);
```















