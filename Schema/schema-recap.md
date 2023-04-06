# 1.13: Schema recap

## Overview of MySQL schema design

- Designing a schema is an essential part of building a database. It is the foundation on which all other operations will be performed, and as such, a key component of the development process. In this video we'll recap what we've learned in the Schema section so far.



## Understanding MySQL data types

- When designing a schema, the first step is to understand the different data types that are available in MySQL. These include strings, numbers, dates, and JSON. Choose the appropriate data type for each column to ensure that it can store the required data and that the database is optimised for performance.

## Choosing the right column attributes

- Once the data type has been determined, it's essential to choose the right column attributes. In addition to the data type, columns can have attributes such as nullable, unsigned, and auto-increment. Choosing the right attributes is important to ensure that the data is accurately represented in the database.

For example, when dealing with numeric data, it's essential to choose the correct data range. If a column can never be negative, then it should be set to unsigned. Similarly, if the data can never be null, don't make the column nullable.

## Keeping schemas small and simple

- A good schema should be simple and small. This means not having unnecessary columns and tables. Keeping it small and simple will make it easier to maintain and optimise. It will also make it easier to manage changes as requirements change over time.



-----

## Summary

- In this section, we've learned about the importance of schema design and how to design a schema that is both simple and efficient. We've also learned about the different data types that are available in MySQL and how to choose the right column attributes. In the next section, we'll learn about how to create and modify a schema using MySQL Workbench.

- Designing a schema is a critical step in building a database. Although requirements change over time, spending time at the beginning can help set you up for success.