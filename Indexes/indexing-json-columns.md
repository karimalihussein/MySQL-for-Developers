# 2.12: Indexing JSON columns

## How to index JSON in MySQL: generated columns and function-based indexes

A powerful feature of MySQL is its ability to store and manipulate JSON data. However, indexing JSON in MySQL can be tricky. Luckily, MySQL provides two viable methods to index specific keys out of a JSON blob: generating a column and creating a function-based index. In this video, we'll take a look at both methods.

## The problem with JSON blobs

- Let's say you have a table full of JSON data. Inside the JSON blob, you have an email address. The problem? You can't just index a JSON blob because MySQL doesn't support indexing JSON blobs. There are other databases that use different types of indexing to index an entire blob, but MySQL doesn't have that. Instead, you have to find a way to index a specific key inside the JSON blob.

## Method 1: generating a column

The first method we will cover is generating a column. This method works in MySQL 5.7 and 8. Here's how it works:

1 - Alter the table to add a new generated column. We'll call it email and make it VARCHAR(255).
2 - Index the new email column.
Let's break these steps down further.

* Step 1: Alter the table
- Here, we're using the GENERATED ALWAYS AS syntax to create a computed column that extracts the email key from the JSON blob.

```sql
ALTER TABLE json_data ADD COLUMN email VARCHAR(255) GENERATED ALWAYS AS (`json` ->> '$.email');
```

- Step 2: Index the new column

```sql
ALTER TABLE json_data ADD INDEX (email);
```

- Now that we have generated and indexed the new column, we can use it to quickly find rows based on their email value.

## Method 2: Function-based index

The second method is to create a function-based index. This method only works in MySQL 8. Using this method we skip the intermediate column and put an index directly on the function itself.

Here, we're using the CAST function to turn the JSON extract into a CHAR(255) value that can be indexed and setting the collation to utf8mb4_bin.

```sql
ALTER TABLE json_data ADD INDEX ((
    CAST(`json`->>'$.email') AS CHAR(255) COLLATE utf8mb4_bin)
));
```

## Conclusion

- Using generated columns or function-based indexes makes it possible to index JSON in MySQL. Each method has its pros and cons, but the end result is the same: a fast and efficient way to search and sort your JSON data.