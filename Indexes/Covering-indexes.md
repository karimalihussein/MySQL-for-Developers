# 2.10: Covering indexes

## Covering indexes in MySQL

- Covering indexes are not a separate type of index in MySQL, but rather a special situation in which an index covers the entire set of requirements for a single query. In this video, we will delve deeper into what covering indexes are, how they work, and when to use them.

## What are covering indexes?

A covering index is a regular index that provides all the data required for a query without having to access the actual table. When a query is executed, the database looks for the required data in the index tree, retrieves it, and returns the result. This eliminates the need for the engine to access the actual table, saving a secondary traversal to gather the rest of the data.

For an index to be considered a covering index, it must have all the data needed for a particular query. This includes the columns being selected, the columns being filtered on, and the columns being used for sorting. If an index satisfies all of these requirements, it is said to be a "covering index" for that query.

## How do covering indexes work?

To understand how covering indexes work, it is useful to know a bit about the inner workings of indexes in MySQL. In MySQL, the primary key is a clustered index, which means that the data is physically sorted in the order of the primary key.

A secondary index, on the other hand, is a separate data structure that maintains a copy of part of the data. When you create a composite index, MySQL creates a B-tree on the specified columns to index them. This B-tree contains a copy of the indexed columns and a pointer to the corresponding row in the clustered index.

When a query is executed, the engine traverses the B-tree to find the required rows and then follows the pointer to fetch the corresponding rows from the clustered index. However, with a covering index, the engine can retrieve all the data it needs from the secondary index itself, without having to access the clustered index.

This is possible because a covering index includes all the columns required for the query and does not need to access the clustered index to retrieve additional data.

## When to use covering indexes

Covering indexes are useful when you need to retrieve a large number of rows from a table. In this case, the engine can retrieve all the data it needs from the index itself, without having to access the table. This can significantly reduce the amount of I/O required to execute the query.

Covering indexes are powerful tools that can significantly improve query performance. However, they are not suitable for all situations.

Because a covering index must include all of the columns required for a query, it can be challenging to find a covering index in the real world. This is particularly true for queries that require multiple columns or involve complex filtering or sorting.

When designing indexes, it is essential to strike a balance between creating indexes that optimize query performance and maintaining the overall performance of the database system. Indexes can have a significant impact on database performance, and an excessive number of indexes can lead to slower performance. It may or may not make sense to try to design for a covering index.

In general, it is best to create indexes that meet the specific needs of your queries while minimizing the number of indexes required. This approach will help ensure optimal query performance while maintaining the overall performance of your database system.

## Conclusion

Covering indexes are a powerful tool in the arsenal of any developer. They can significantly improve query performance by eliminating the need to access the actual table and fetching all the required data from the index itself.

While covering indexes are not suitable for all situations, they can be a game-changer for queries with straightforward requirements.