# 1.9 Json

## MySQL JSON columns: when, why, and how to use them
MySQL has proper first-party support for JSON (JavaScript Object Notation) columns. Developers can use JSON columns in much of the same way that they use other data types in MySQL, such as strings, numbers, and datetimes.

In this video, we'll explore the use cases for JSON columns, and take an in-depth look at how to use them within the MySQL schema. We'll discuss the syntax for creating JSON objects in a MySQL database, and examine the use of JSON functions for retrieving and manipulating data. Finally, we'll consider the best practices for storing JSON data, and provide some guidelines for when and why to use JSON columns in your MySQL database.


## Creating and validating JSON objects

- To begin with, let's explore the syntax for creating and validating JSON objects in a MySQL database. The data type that you're looking for when working with JSON is simply JSON. For example, to create a new table with a JSON column in it, you might use the following code:

```sql
CREATE TABLE has_json (
  id INT(11) NOT NULL AUTO_INCREMENT,
  json JSON NULL,
  PRIMARY KEY (id)
);
```

When working with JSON data, MySQL is much more strict than with other text data types. The JSON data must be valid according to the JSON specification, or MySQL will reject it. This helps ensure that you're not storing incorrectly formatted data in your JSON columns.

For example, let's say we insert an invalid JSON object into our has_json:

```sql
INSERT INTO has_json (json) VALUES ('{"foo": "bar"}');
```

- When we try to insert this data, we'll get an error message because the JSON object is not valid, as it is missing quotes around the key and value.


```sql
ERROR 3140 (22032): Invalid JSON text: "The document root must not be followed by other values." at position 0 in value for column 'json'.
```

- By contrast, when we insert a valid JSON object, we can retrieve it without any issue:

```sql
INSERT INTO has_json (json) VALUES ('{"key": "value"}');
SELECT json FROM has_json;

-- Output
+---------------------+
| json                |
+---------------------+
| {"key": "value"}    |
+---------------------+
```

- In this case, we can see that the JSON object was successfully inserted into the database, and that we can retrieve it without any issue.

## Retrieving data from JSON columns
- Once you have valid JSON data in your MySQL database, you can use various functions and operators to retrieve and manipulate it.

- Suppose we want to retrieve just the key from this JSON object. We could use the -> operator, like so:

```sql
SELECT `json`->>"$.key" as key FROM has_json;

-- Output
+------+
| key  |
+------+
| value|
+------+
``` 
The ->> operator is used to extract a JSON object at a specific path. This is called the "JSON unquoting operator."

## Indexing JSON columns
One important consideration when using JSON columns in MySQL is that they cannot be directly indexed. Instead, MySQL supports indexing for generated columns on a specified JSON path. This means you can create an index on a specific key within a JSON object, but not on the entire object itself.

For example, consider the following code:

```sql
ALTER TABLE has_json ADD INDEX my_index ((`json`->>"$.key"));
```

- Here, we're creating an index on the key field within the JSON object of our column. This allows MySQL to perform faster lookups for queries that involve this particular JSON path.


## When and why to use JSON columns


Before we wrap up, let's consider the best practices for storing JSON data in MySQL. While JSON columns in MySQL can be incredibly powerful, they should not be used as a replacement for traditional schema design! Instead, use JSON columns in situations where there is no well-defined schema or the schema changes frequently.

For example, a JSON column might make sense when you're storing payloads from third-party services or APIs that have different response formats. A JSON column can also be useful when you're storing nested or hierarchical data that doesn't fit neatly into a relational database design.

One caveat when using JSON columns is that they can be quite heavy, especially if you're storing large amounts of JSON data. As with any data type in MySQL, only select the data you need when you're querying, and avoid retrieving JSON data unnecessarily.

## Conclusion

- In this video, we've explored the benefits and best practices for using JSON columns in MySQL. We've looked at how to create and validate JSON objects in a MySQL schema, and shown how to use various functions and operators to retrieve and manipulate data. Finally, we've considered the use cases for JSON data, and provided some guidelines for when and why to use JSON columns in your MySQL database.

- While JSON columns can be a powerful addition to your MySQL schema, it's important to use them judiciously and in accordance with best practices. By following these guidelines, you can ensure that your use of JSON columns aligns with your broader schema design and helps you build more efficient and scalable applications.