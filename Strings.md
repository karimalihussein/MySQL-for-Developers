## 1.3 : Strings

## Understanding MySQL string data types, column sizes, character sets, and collations

- When it comes to storing strings in MySQL, there are a variety of different ways to do it. In fact, there are so many ways that it can take multiple videos just to cover them all. In this video, we'll provide an overview of the different types and then dive deeper into two specific types: fixed-length columns and variable-length columns.

## Types of MySQL string columns:
- When it comes to storing strings in MySQL, there are many different types to choose from. Here's a list of the different types:

1 - `CHAR`: a fixed-length string that is always right-padded with spaces to the specified length when stored.
2 - `VARCHAR`: a variable-length string. The length can vary between 0 and 65,535 characters.
3 - `TINYTEXT`: a string with a maximum length of 255 characters.
4 - `TEXT`: a string with a maximum length of 65,535 characters.
5 - `MEDIUMTEXT`: a string with a maximum length of 16,777,215 characters.
6 - `LONGTEXT`: a string with a maximum length of 4,294,967,295 characters.
7 - `BINARY`: a fixed-length string that is always right-padded with null bytes to the specified length when stored.
8 - `VARBINARY`: a variable-length string. The length can vary between 0 and 65,535 bytes.
9 - `TINYBLOB`: a string with a maximum length of 255 bytes.
10 - `BLOB`: a string with a maximum length of 65,535 bytes.
11 - `MEDIUMBLOB`: a string with a maximum length of 16,777,215 bytes.
12 - `LONGBLOB`: a string with a maximum length of 4,294,967,295 bytes.
13 - `ENUM`: a string object that can have only one value, chosen from the list of values 'permitted' for that column.
14 - `SET`: a string object that can have zero or more values, each of which must be chosen from the list of values 'permitted' for that column.


----------------------------------------------------------------------
| Data Type | Storage requirement  |  Maximum length| Minimum length | 
|-----------|----------------------|----------------|----------------|
| CHAR      | 1 byte per character | 255            | 0              |                  
| VARCHAR   | 1 byte per character | 65,535         | 0              |                  
| TINYTEXT  | 1 byte per character | 255            | 0              |                  
| TEXT      | 2 bytes per character| 65,535         | 0              |                  
| MEDIUMTEXT| 3 bytes per character| 16,777,215     | 0              |                  
| LONGTEXT  | 4 bytes per character| 4,294,967,295  | 0              |                  
| BINARY    | 1 byte per character | 255            | 0              |                  
| VARBINARY | 1 byte per character | 65,535         | 0              |                  
| TINYBLOB  | 1 byte per character | 255            | 0              |                  
| BLOB      | 2 bytes per character| 65,535         | 0              |                 
| MEDIUMBLOB| 3 bytes per character| 16,777,215     | 0              |                  
| LONGBLOB  | 4 bytes per character| 4,294,967,295  | 0              |                  
| ENUM      | 1 or 2 bytes         | 65,535         | 1              |                  
| SET       | 1, 2, 3, 4,or 8 bytes| 64             | 0              |                  
----------------------------------------------------------------------

- The `CHAR` and `VARCHAR` types are the most commonly used string types. The `CHAR` type is a fixed-length string that is always right-padded with spaces to the specified length when stored. The `VARCHAR` type is a variable-length string. The length can vary between 0 and 65,535 characters.

- The `TINYTEXT`, `TEXT`, `MEDIUMTEXT`, and `LONGTEXT` types are similar to the `CHAR` and `VARCHAR` types, except that they have a maximum length of 255, 65,535, 16,777,215, and 4,294,967,295 characters, respectively.

- The `BINARY` and `VARBINARY` types are similar to the `CHAR` and `VARCHAR` types, except that they store binary byte strings rather than nonbinary character strings. The `BINARY` type is a fixed-length string that is always right-padded with null bytes to the specified length when stored. The `VARBINARY` type is a variable-length string. The length can vary between 0 and 65,535 bytes.

- The `TINYBLOB`, `BLOB`, `MEDIUMBLOB`, and `LONGBLOB` types are similar to the `TINYTEXT`, `TEXT`, `MEDIUMTEXT`, and `LONGTEXT` types, except that they store binary byte strings rather than nonbinary character strings.

- The `ENUM` type is a string object that can have only one value, chosen from the list of values 'permitted' for that column. An ENUM can have a maximum of 65,535 distinct values.

- The `SET` type is a string object that can have zero or more values, each of which must be chosen from the list of values 'permitted' for that column. A SET can have a maximum of 64 distinct members.

- While this may seem overwhelming, one important thing to focus on is understanding the differences between fixed-length and variable-length columns.

# Fixed-length columns
- Fixed-length columns are usually used for storing data that is a consistent size. This could be data like two-digit prefixes, MD5 hashes, or alphanumeric serial numbers. Fixed-length columns are declared using the CHAR data type and require you to specify the column size.

```sql
CREATE TABLE strings (
  fixed_five CHAR(5),
  fixed_32 CHAR(32)
);
```

- In the example above, we've created two fixed-length columns. The fixed_five column can store up to five characters, while the fixed_32 column can store up to 32 characters. It's essential to note that, no matter how many characters you store in a fixed-length column, it will always occupy the full amount of space specified.

# Variable-length columns
Variable-length columns, on the other hand, do not have a fixed size. The amount of space required depends on the data being stored in the column. Variable-length columns are declared using the VARCHAR data type, and you have to specify the maximum column size.

```sql
CREATE TABLE strings (
  variable_length VARCHAR(100)
);
```

-in the example above, we've created a variable-length column that can store up to 100 characters. Since variable-length columns do not occupy the full amount of space specified, they can be more efficient when it comes to storage. However, it's essential to choose the smallest possible data type for the data you are trying to store.


# Character sets and collations

A character set defines what characters are allowed to go into a column. MySQL supports a wide range of character sets, which you can view from the information_schema database. utf8 and utf8mb4 are the character sets you will likely use, with the latter being the default in MySQL 8.

Collations, on the other hand, determine how two or more strings are compared or sorted. A collation is a group of rules that decide whether two strings are equivalent or not. The default collation for MySQL 8 is utf8mb4_0900_ai_ci, with the ai indicating that the collation is accent-insensitive, and ci meaning that it is case-insensitive.

```sql
CREATE TABLE strings (
  variable_length VARCHAR(100) CHARSET utf8mb4 COLLATE utf8mb4_general_ci
);
```

- In the example above, we've created a VARCHAR column with a character set of utf8mb4 and a collation of utf8mb4_general_ci. The character set defines what characters are allowed to go into the column, while the collation determines how two or more strings are compared or sorted.

# Conclusion

- In this article, we've covered the different types of string columns that MySQL supports. We've also looked at the differences between fixed-length and variable-length columns, and how to specify the character set and collation for a column.

## Exercise

- Create a table called strings with the following columns:
  - id: an INT column that is the primary key and auto-incrementing.
  - fixed_five: a CHAR column that can store up to five characters.
  - fixed_32: a CHAR column that can store up to 32 characters.
  - variable_length: a VARCHAR column that can store up to 100 characters.
  - character_set: a VARCHAR column that can store up to 100 characters and has a character set of utf8mb4 and a collation of utf8mb4_general_ci.


# Answer

```sql
CREATE TABLE strings (
  id INT PRIMARY KEY AUTO_INCREMENT,
  fixed_five CHAR(5),
  fixed_32 CHAR(32),
  variable_length VARCHAR(100),
  character_set VARCHAR(100) CHARSET utf8mb4 COLLATE utf8mb4_general_ci
);

INSERT INTO strings (fixed_five, fixed_32, variable_length, character_set)
VALUES ('abcde', '12345678901234567890123456789012', 'This is a variable-length column', 'This is a column with a character set and collation');

SELECT * FROM strings;
```