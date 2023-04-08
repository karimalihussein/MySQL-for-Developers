# 2.13: Indexing for wildcard searches

## Wildcard searches in MySQL

In this article, we'll discuss wildcard string searches in MySQL and how indexes can affect these searches. Searching for part of a column using wildcard characters can be useful when you want to find all rows that contain specific words or phrases. However, it's important to understand how indexes work with these searches to optimize the speed of your queries.

Let's say we want to search for all rows where the email column starts with the name "aaron." We can use the LIKE operator and the % wildcard character to find all matches:


```sql
SELECT * FROM people WHERE email LIKE 'aaron%';
```
- This query will return all rows where the email column starts with "aaron." The % character matches any sequence of characters, meaning that we don't care what comes after "aaron."


## Adding an index

If we plan on running this query frequently on a large table, we'll want to add an index to speed up the search. We can add an index to the email column by running the following command:

```sql
ALTER TABLE people ADD INDEX (email);
```

- Now, if we run the same query and use the EXPLAIN command to see how MySQL is executing the query, we should see that MySQL is using our newly-created index:

```sql
SELECT * FROM people WHERE email LIKE 'aaron%';

EXPLAIN SELECT * FROM people WHERE email LIKE 'aaron%';

+----+-------------+--------+-----------------------+-------+---------+-----+------+----------+
| id | select_type | table  | type  | possible_keys | key   | key_len | ref | rows | filtered |
+----+-------------+--------+-----------------------+-------+---------+-----+------+----------+
|  1 | SIMPLE      | people | range | email         | email | 1022    | NULL|  180 |   100.00 |
+----+-------------+--------+-----------------------+-------+---------+-----+------+----------+
```


## Querying for specific words or phrases
It's important to note that MySQL can only use an index up until it reaches a wildcard character, such as %. If we want to search for specific words or phrases within a larger column, we need to be careful with how we structure our queries.

For example, let's say we want to find all rows where the email column contains the word "aaron" anywhere within the column:

```sql
SELECT * FROM people WHERE email LIKE '%aaron%';
```

- This query will return all rows where the email column contains the word "aaron" anywhere within the column. However, since we have a wildcard character at the beginning of the search string, MySQL cannot use the index we created on the email column. This means the query will be slower than if we had used a wildcard character only at the end of the search string.


## Searching by domain

If we want to search for rows based on the domain of the email address, we may be tempted to put the wildcard at the beginning of the string. However, as we mentioned earlier, MySQL cannot use an index when a wildcard character is at the beginning of a search string.

To get around this limitation, we can create a generated column that stores only the domain of the email address, and then create an index on that column. This allows us to perform a strict equality check, rather than a wildcard search.

For example, we can create a email_domain column that extracts the domain from the email address:



```sql
ALTER TABLE people ADD COLUMN email_domain VARCHAR(255) AS (SUBSTRING_INDEX(email, '@', -1));
```

- Then, we can add an index on this column and perform a search like so:

```sql
ALTER TABLE people ADD INDEX (email_domain);
SELECT * FROM people WHERE email_domain = 'example.com';
```

- By creating a generated column and indexing it, we can perform more efficient searches on specific parts of larger columns.


## Full text indexes
While B-tree indexes work well for wildcard searches at the end of a search string, they may not be sufficient for more complex text searches. In these cases, we can use a full text index.

Full text indexes allow us to search for specific words or phrases within a larger text column with much greater efficiency than using a simple wildcard search. We'll look at how to use full text indexes in MySQL in the next video.

## Conclusion

In this article, we discussed how to use wildcard searches in MySQL and how indexes can affect these searches. We also looked at how to create a generated column and index it to perform more efficient searches on specific parts of larger columns.

Wildcard string searches can be useful for searching for specific words or phrases within larger columns in MySQL. However, it's important to understand how indexes affect these searches, and how to structure the search string to ensure efficient indexing. By creating generated columns and indexing specific parts of larger columns, we can greatly improve the speed of our queries.
