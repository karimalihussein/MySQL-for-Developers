# 2.17: Foreign keys

## Foreign keys in MySQL

- In this lesson, we will explore the concept of foreign keys and how they can be used to build and maintain data relationships within relational databases.

## Foreign keys vs. foreign key constraints

To start, it's important to understand the difference between foreign keys and foreign key constraints. A foreign key is a column or set of columns in a table that references the primary key of another table. This enables related data to be linked together in separate tables.

On the other hand, a foreign key constraint is a condition that ensures the referential integrity of the data by enforcing a relationship between the foreign key and the referenced primary key. This means that the constraint will guarantee that all data references are valid and consistent, preventing data from being added, updated, or deleted in a way that would break the relationships between tables.

It's worth noting that foreign keys can exist without constraints, but constraints are helpful to maintain referential integrity. Constraints also require additional computation to maintain, so at a certain scale, you may need to consider dropping some constraints if they become too costly in terms of performance.

## Creating tables with foreign keys

- Let's take a look at a simple example of creating two tables with a foreign key constraint. We'll start with a parent table and a child table. Here's the code to create the parent table:

```sql
CREATE TABLE parent (
  ID BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY
);
```

- This creates a table parent with a single column id as a primary key. Now let's create the child table with a foreign key constraint that references the parent table:

```sql
CREATE TABLE child (
  ID BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  parent_id BIGINT UNSIGNED,

  FOREIGN KEY (parent_id) REFERENCES parent(ID)
);

```

This creates a table child with two columns, id and parent_id. The parent_id column references the primary key of the parent table using a foreign key constraint. This constraint enforces the referential integrity of the data, ensuring that any data added to the child table is consistent with the data in the parent table.

However, it's important to note that when creating a foreign key constraint, the referenced column must be of the same data type as the referencing column. For instance, if the id column in the parent table is unsigned, the parent_id column in the child table must also be unsigned. Additionally, the length and character set of string columns used for referencing each other should match for optimal performance.

## Modifying data with foreign keys

Now that we have our tables set up with a foreign key constraint, let's take a look at how data can be modified with this constraint in place.

First, let's insert some data into the child table:

```sql
INSERT INTO child (parent_id) VALUES (1);
```

This code attempts to insert a record into the child table with a parent_id value of 1. However, since the parent table is currently empty, this will fail because there is no data to reference.

Let's insert a record into the parent table to correct that:

```sql
INSERT INTO parent (ID) VALUES (1);
```

- Now that we have a record in the parent table, we can successfully insert a record into the child table:

```sql
INSERT INTO child (parent_id) VALUES (1);
```

- This code inserts a record into the child table with a parent_id value of 1. Since the parent_id column has a foreign key constraint that references the id column in the parent table, this will succeed because the parent_id value of 1 exists in the parent table.

The foreign key constraint ensures that this data is consistent and reflects a valid relationship between the two tables.

If we try to delete the record from the parent table, we would encounter another issue:

```sql
DELETE FROM parent WHERE ID = 1;
```

This code attempts to delete the record from the parent table with an ID of 1. Since there is still a record in the child table that references this ID, the foreign key constraint will prevent this deletion from taking place.

To enable cascading deletes or nullifying deleted references, additional options can be set on the foreign key constraint. It is important to consider the scale and impact of these options to avoid unintended consequences such as excessive data deletion or corruption.

## Summary

- In this lesson, we explored the concept of foreign keys and how they can be used to build and maintain data relationships within relational databases. We also looked at how foreign keys can be used to enforce referential integrity and how they can be used to modify data in a way that maintains the integrity of the data.

Foreign keys are an important tool for maintaining relationships and ensuring the integrity of data in a relational database. By linking tables together and enforcing referential integrity, foreign keys help ensure consistency and accuracy in data management.

While foreign key constraints can be expensive to maintain at a large scale, they are helpful to ensure data integrity in many situations.