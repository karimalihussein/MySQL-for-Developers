## 1.5 Binary strings


## The power of binary and varbinary columns in MySQL

- When talking about MySQL, the CHAR and VARCHAR columns are the most commonly known ways to store string values. However, there are other columns available in MySQL that can store string-ish values, such as the BINARY and VARBINARY columns. These store bytes of data rather than characters, allowing users to store raw binary data, little bits of binary data that cannot be represented as strings, or do not need to be stored in that way.

## Understanding binary and varbinary columns

- The BINARY and VARBINARY columns are quite similar to the CHAR and VARCHAR columns, with one main difference. While the CHAR and VARCHAR columns store characters and follow the rules of character sets and collations, the binary and VARBINARY columns store bytes only. In other words, there is no character set or collation to be concerned about; it is just raw binary data.

- The BINARY column is a fixed length column, while the VARBINARY column is a variable length column. With VARBINARY columns, you can store up to a set number of bytes, rather than fixed data types. Although not too commonly used, BINARY and VARBINARY columns provide an efficient way to store binary data, such as hashes or UUIDs.


## How to use binary columns in MySQL

- To illustrate how to use binary columns in MySQL, we will use a simple example: storing hashes. To start, we will create a table with two columns: one BINARY column and one variable BINARY column.

```sql
CREATE TABLE bins (
  bin BINARY(16),
  varbin VARBINARY(100)
);
```

- Next, we will generate some binary data using the MD5 function. This function returns the MD5 hash of a given string. For example, the MD5 hash of "hello" is "5d41402abc4b2a76b9719d911017c592". We can turn this hash into binary data using the UNHEX function.

```sql
SELECT UNHEX(MD5('hello'));
```

- This will return the following result:

```
+----------------------------------+
| UNHEX(MD5('hello'))              |
+----------------------------------+
| 0x5d41402abc4b2a76b9719d911017c592 |
+----------------------------------+
```

- The output will be a binary representation of the hash, but it will still be displayed as a string of hexadecimal digits in TablePlus. To see the actual binary data, we need to connect to the MySQL server using the command-line client with the "skip binary as hex" flag.

```sql
mysql -u root -p --skip-binary-as-hex
```

- Now, we can insert the binary data into the table.

```sql
INSERT INTO bins (bin, varbin) VALUES (UNHEX(MD5('hello')), UNHEX(MD5('hello')));
```



