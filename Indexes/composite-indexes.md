# 2.9: Composite indexes

## Mastering Composite indexes in MySQL

- In our previous discussions about indexing, we focused on single column indexes. While they are essential to know, there's something even more interesting to learn about: composite indexes (also known as multi-column or composite indexes). Composite indexes cover multiple columns instead of having individual indexes on each column. Understanding and effectively using composite indexes can elevate you from a decent database user to an advanced one. In this video, we'll discuss what composite indexes are, how to create them, and when they can and can't be used.

## Creating a composite index

Let's start with creating a composite index on our people table. We have been adding single column indexes like this:

```sql
ALTER TABLE people ADD INDEX first_name (first_name);
ALTER TABLE people ADD INDEX last_name (last_name);
ALTER TABLE people ADD INDEX birthday (birthday);
```
- Now, we'll create a composite index covering the first_name, last_name, and birthday columns:

```sql
ALTER TABLE people ADD INDEX multi (first_name, last_name, birthday);
```

- When you inspect the indexes on the people table, you'll notice the multi index with a sequence in the index column. This sequence indicates the order of the columns in the index, which is crucial for how the index can be used.

- Let's take a look at the query plan for the following query: 

```sql
SHOW INDEXES FROM people;
```

| Table  | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality  | Index_type |
|--------|------------|----------|--------------|-------------|-----------|--------------|------------|
| people |     1      | multi    |      1       | first_name  | A         | 3017         | BTREE      |
| people |     1      | multi    |      2       | last_name   | A         | 419540       | BTREE      |
| people |     1      | multi    |      3       | birthday    | A         |  419583      | BTREE      |

## Rules for composite indexes

### There are two main rules for using composite indexes:

1. Left-to-right, no skipping: MySQL can only access the index in order, starting from the leftmost column and moving to the right. It can't skip columns in the index.

2. Stops at the first range: MySQL stops using the index after the first range condition encountered.


## Analyzing index usage

- To understand how MySQL uses composite indexes, you can use the EXPLAIN statement. For example, let's analyze the following query:


```sql
EXPLAIN SELECT * FROM people WHERE first_name = 'Aaron' AND last_name = 'Francis';

+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
| id | select_type | table  | type  | possible_keys | key    | key_len |    ref     | rows | filtered |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
|  1 | SIMPLE      | people | ref   | multi         | multi  | 3       |const,const |  1   |   100.00 |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
```

- The EXPLAIN output shows that the multi index is being used, with a key length of 404 bytes. This indicates that MySQL is using both the first_name and last_name parts of the index.

If we add birthday to the mix, the key_len jumps to 407.

- Let's take a look at the following query:

```sql
EXPLAIN SELECT * FROM people WHERE first_name = 'Aaron' AND last_name = 'Francis' and birthday = '1989-02-14';

+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
| id | select_type | table  | type  | possible_keys | key    | key_len |    ref     | rows | filtered |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
|  1 | SIMPLE      | people | ref   | multi         | multi  | 407     |const,const |  1   |   100.00 |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
```

- However, if you change the query to include a range condition on last_name, then the key_len drops back down to 404.

- Let's take a look at the following query:

```sql
EXPLAIN SELECT * FROM people WHERE first_name = 'Aaron' AND last_name < 'Francis' and birthday = '1989-02-14';

+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
| id | select_type | table  | type  | possible_keys | key    | key_len |    ref     | rows | filtered |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
|  1 | SIMPLE      | people | range | multi         | multi  | 404     |const,const |  55  |   10.00  |
+----+-------------+--------+-------+---------------+--------+---------+------------+------+----------+
```

- This is because MySQL can't use the index for the last_name range condition. It can only use the index for the first_name equality condition.

- The key length remains 404 bytes, meaning MySQL stops using the index at the first range condition (last_name in this case) and doesn't use the birthday part of the index.

## Tips for defining composite indexes

- Now that you understand how MySQL uses composite indexes, let's look at some tips for defining them.

- First, you should always define the most selective columns first. This means that the columns that have the most unique values should be first in the index. This is because MySQL can use the index to eliminate rows more efficiently if the most selective columns are first.

Choosing the right order for columns in a composite index depends on the access patterns of your application. Consider the following tips when defining composite indexes:

1 - Equality conditions that are commonly used would be good candidates for being first in a composite index.
2 - Range conditions or less frequently used columns would be better candidates for ordering later in the composite index.
Composite indexes can significantly improve the performance of your database queries. Understanding and effectively using them is essential for advanced database users. Remember to consider your access patterns and carefully define the order of your columns to create efficient composite indexes.

