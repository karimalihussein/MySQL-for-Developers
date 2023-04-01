# 1.6 Long strings

## Introduction

- When it comes to managing data in MySQL, there are several types of columns that you can use to store different types of data. In this video, we will be focusing on TEXT and BLOB columns, which are used to store large amounts of text and binary data, respectively. We will dive into what sets these columns apart from other data types and explore the different variations available.

## Text columns

- TEXT columns are used to store character data, such as strings of text. Unlike other string data types we've talked about, TEXT columns allow you to store much larger amounts of data, making them a great option for storing long blocks of text. However, it's important to note that text columns are not indexable (without using full text indexes) and cannot be sorted on their full values. A workaround is to index only a prefix of the columns or to sort by only the first few thousand characters.

- There are four types of text columns in MySQL: TINYTEXT, TEXT, MEDIUMTEXT, and LONGTEXT. As the name suggests, each type has a cap for the amount of data it can hold. The TINYTEXT column can hold up to 255 characters, while the LONGTEXT column can hold up to 4 gigabytes of data.


## Blob columns

- BLOB columns, on the other hand, are used to store binary data. They are similar to TEXT columns in that they allow you to store much larger amounts of data compared to other data types. However, BLOB columns do not have a character set or a collation like TEXT columns do.

- Like TEXT columns, there are four types of blob columns: TINYBLOB, BLOB, MEDIUMBLOB, and LONGBLOB. They differ in the amount of data they can hold, with the LONGBLOB column being able to store up to 4 gigabytes of data.

## Storing files in blob columns
- While BLOB columns can hold binary data such as images or audio files, it's not recommended to store them in the database. It's usually better to store these types of files somewhere else and leave a pointer in a VARCHAR column to that location.

## Best practices

When using text or blob columns, it's important to consider two things: how much data you need to store and how you will access that data. Here are some best practices to keep in mind:

Only select the columns that you need: Because of how large TEXT and BLOB columns are stored on the disk, it's best to only select them when you need them. Refactor your data so that BLOB columns can be joined in when necessary.
Don't index or sort entire columns: Because of the size of TEXT and BLOB columns, it's not feasible to index or sort on the entire column. You should only index or sort on a prefix of the column.
Use VARCHAR columns for smaller amounts of data: If you only need to store a few hundred characters, consider using VARCHAR instead of text columns. This can help with indexing and sorting.


# Conclusion
In conclusion, TEXT and BLOB columns are useful data types in MySQL for storing large amounts of text and binary data. They have different variations available depending on how much data you need to store. While they have benefits in terms of storage, it's important to follow best practices to avoid potential issues with indexing, sorting and retrieval speed.
