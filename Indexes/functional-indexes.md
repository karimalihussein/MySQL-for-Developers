# 2.11: Functional indexes

## Function-based indexes in MySQL
- An index is a way of organizing data in a table to improve the speed of data retrieval operations. In this article, we will explore a specific type of index called function-based indexes.

## What are function-based indexes?

Function-based indexes are used in cases where you need to create an index on a function rather than a column. For example, consider a scenario where you need to retrieve all the records where the birth month is February. You might have a birthday column in your table, but applying a function such as month() to it will not allow you to use an index. This is where function-based indexes come in handy.

A function-based index is created by applying a function to one or more columns of a table, and then creating an index on the results of that function. This allows you to search for records based on the results of that function, while still taking advantage of the speed and efficiency benefits of an index.



## Creating a function-based index

- To better understand how to create a function-based index in MySQL, let's take a look at a sample table called people.

```sql
CREATE TABLE people (
  id INT(11) NOT NULL AUTO_INCREMENT,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  birthday DATE NOT NULL,
  PRIMARY KEY (id)
);
```

- Suppose we want to create an index to retrieve records where the birth month is February. We can create a function-based index using the month() function as shown below:


```sql
ALTER TABLE people ADD INDEX idx_month_birth ((MONTH(birthday)));
```

- The above statement will create an index on the results of the month() function applied to the birthday column. This will allow us to search for records where the birth month is February as shown below:
- in the above SQL statement, we are creating an index called idx_month_birth on the results of the MONTH(birthday) function. The double parentheses are used to denote that we are creating a function-based index.

## Conclusion

- In this article, we have learned about function-based indexes

- Function-based indexes are particularly useful in scenarios where the thing that you're trying to index is not a column, but rather the result of some set of operations or functions. They allow you to search for records based on the results of a function, while still taking advantage of the speed and efficiency benefits of an index. Use them in cases where standard indexes cannot meet your needs.