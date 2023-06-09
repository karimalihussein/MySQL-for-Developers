# 2.4: Secondary keys

## Understanding secondary keys in MySQL

- When it comes to discussing database keys, primary keys often take up the spotlight. However, that does not mean that secondary keys, also known as indexes, are not equally important. In this video, we will explore secondary keys in MySQL and how they relate to primary keys.


## What are secondary keys in MySQL?

- A secondary key is simply any index that is not the primary key of a table. Every MySQL table has one primary key and can have multiple secondary keys. It is crucial to note that primary and secondary keys are still related to each other, and understanding this relationship is crucial to working with them effectively.


## Understanding primary and secondary key relationship

- To better understand the relationship between primary and secondary keys, we need to look at an example. Consider a people table with the columns id, name, and email.

### Creating a secondary key
- We can create a secondary key on name using the following MySQL query:

```sql
CREATE TABLE people (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  PRIMARY KEY (id),
  INDEX (name)
);

ALTER TABLE people ADD INDEX (name);
```

- An index on the name column is now created, and we can use it to query the people table.

## Querying people table using secondary key

- Here is a sample query that retrieves all the rows of a person whose name is Suzanne using the secondary key:

```sql
SELECT * FROM people WHERE name = 'Suzanne';
```
- This query returns a single row containing the ID, name, and email.

- How the query works
When executed, MySQL uses the B-tree index created on the name column to locate the row with the specified name. It begins at the root node of the index and works its way down through the branches until it reaches the leaf node representing the row with the matching name.

- Now, since the name column is a secondary key, it does not store all the data required for the query. It only contains the indexed column name and a pointer to the rest of the row. MySQL must perform a second lookup to retrieve the rest of the data related for that row.


## Relationship between secondary and primary keys

- Every secondary key has the primary key appended to it, as each leaf node in the secondary key contains a pointer back to the row. When you perform a query with a secondary key, MySQL first traverses the secondary index tree, finds the corresponding primary key, and then looks up that primary key in the primary index tree to retrieve all the data.

## Importance of compact primary keys

- As previously mentioned, each leaf node in a secondary key has the primary key appended to it. Therefore, it is crucial to choose compact primary keys that require a minimal amount of storage space.

## Summary

- In this lesson, we learned about secondary keys in MySQL and how they relate to primary keys. We also learned about the importance of compact primary keys and how they affect the performance of secondary keys.

As previously mentioned, each leaf node in a secondary key has the primary key appended to it. Therefore, it is crucial to choose compact primary keys that require a minimal amount of storage space.