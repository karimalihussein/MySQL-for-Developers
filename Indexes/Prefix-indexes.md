# 2.8: Prefix indexes

## Prefix indexing in MySQL

In this lesson, we're going to dive into the concept of prefix indexing in MySQL. Before that, let's refresh our memory on cardinality and selectivity. In simple terms, cardinality refers to the number of unique values, while selectivity refers to the number of unique rows compared to the total number of rows.

Now, let's see how prefix indexing plays a role in cardinality and selectivity. Suppose you have a long string column, such as an URL or a UID, that's impossible to index entirely. In that case, you can index a part of the string by creating prefix indexes.

Here, we'll explore how prefix indexing can optimize your database performance, how to create prefix indexes, and the drawbacks of using them.


## Advantages of using prefix indexing

- By indexing just a part of a string column, you can make the index much smaller and faster. For example, indexing only the first four or five characters of a string reduces the size of the index while potentially maintaining the selectivity.

Prefix indexing is especially suitable for long, evenly distributed, and unique strings, such as UUIDs and hashes.

## Creating prefix indexes

- To create a prefix index in MySQL, you have to specify the prefix length you want to index. Suppose we have a people table with a string column for the first name, and we want to index the first five characters only:

```sql
ALTER TABLE people ADD INDEX (first_name(5));
```

- In the above statement, we're using the ADD INDEX syntax along with specifying the prefix length of five for the first_name column.

After creating a prefix index, you can confirm its creation by running the following query:

```sql
SHOW INDEXES FROM people;
```

- This query displays all indexes associated with the people table. You can see the first_name column, and the sub_part column that specifies the index's prefix length.

## Determining prefix lengths

- Now that we know how to create prefix indexes let's determine the ideal prefix length of a column. To determine the prefix length of a column to index, we have to calculate the overall selectivity of the column and compare it to the selectivity of the prefix.

Let’s consider an example where we have a table with a column first_name, consisting of 3009 unique first names out of 500,000 people. In this case, the selectivity of the column is:

```sql
SELECT COUNT(DISTINCT first_name) / COUNT(*) as selectivity from people;
```

- Running the above query gets a selectivity of 0.0060.

Now, we can experiment with different lengths in the LEFT() function to determine the smallest prefix length that provides close to full selectivity. Here's a sample of prefixes you can test:

```sql
SELECT COUNT(DISTINCT LEFT(first_name, 4)) / COUNT(*) as left4 from people;
SELECT COUNT(DISTINCT LEFT(first_name, 5)) / COUNT(*) as left5 from people;
SELECT COUNT(DISTINCT LEFT(first_name, 6)) / COUNT(*) as left6 from people;
SELECT COUNT(DISTINCT LEFT(first_name, 7)) / COUNT(*) as left7 from people;
```

- As you increase the prefix length of columns values, we'll notice that the selectivity will also increase. Therefore, we can determine the ideal index for the column based on the minimum prefix length that achieves close to full selectivity.


## Drawbacks of using prefix indexing


- Although prefix indexing is useful in specific contexts, it has a few drawbacks that limit its applicability in sorting tasks.

Firstly, prefix indexes are not suitable for ordering or grouping as the index does not contain the full string value, and therefore cannot be used. This makes it impossible to use a prefix index to sort results by the given column. (You can still sort by the column, but it will not use the index.)


## Summary

In this lesson, we learned about prefix indexing in MySQL. We also learned how to create prefix indexes and how to determine the ideal prefix length of a column. Finally, we learned about the drawbacks of using prefix indexing.

Prefix indexing in MySQL is a useful technique when you have long string columns that you can't index in their entirety, or you can approach full selectivity with a short prefix. It optimizes database performance and makes indexing faster. However, you must keep in mind the cardinality and selectivity of your column values and the prefix length suitable for indexing.

It's a potent tool worth considering to optimize your database queries where suitable.


