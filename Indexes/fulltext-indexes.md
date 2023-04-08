# 2.14: Fulltext indexes

## Full-text searching in MySQL

Searching for data in a database is a crucial aspect of creating effective applications. While simple string searches can help find basic results, what happens when you're searching across multiple columns or trying to find specific words within a block of text? That's where full-text indexing and full-text searching come in handy in databases like MySQL.

In this video, we'll go over how to use full-text indexing in MySQL, including adding indexes and implementing full-text searches with natural language and boolean modes.

## Adding full-text indexes

- To add a full-text index to a table in MySQL, you can use an ALTER TABLE statement. In this example, we'll be adding a full-text index across the first_name, last_name, and bio columns in our people table.

```sql
ALTER TABLE people ADD FULLTEXT INDEX `fulltext`(first_name, last_name, bio);
```

- Note the use of the FULLTEXT keyword to create a full-text index instead of a regular B-tree index.

Creating a full-text index can take some time, so be prepared for it to take longer than a regular index. You can check that the index was created successfully by running SHOW INDEXES FROM people; which should display the new full-text index.

## Implementing full-text searches

- With the full-text index in place, we can start implementing full-text searches.



## Natural language mode

By default, full-text searches in MySQL are done in natural language mode. Natural language mode matches the search query against the indexed columns and returns the most relevant results.

For example, to search for all people with the first name "Aaron," we can use the following query:

```sql
SELECT * FROM people WHERE MATCH(first_name, last_name, bio) AGAINST('Aaron');
```

- This query will search across all three indexed columns and display all rows where "Aaron" appeared.

- Note that we're using the MATCH function to perform the full-text search. This function takes two arguments: the columns to search and the search query. The search query can be a single word or a phrase.

- The AGAINST keyword is used to specify the search query. In this case, we're searching for the word "Aaron."

- If we want to search for a phrase, we can wrap the phrase in double quotes:

```sql
SELECT * FROM people WHERE MATCH(first_name, last_name, bio) AGAINST('"Aaron Smith"');
```

- This query will return all rows where the phrase "Aaron Smith" appeared.

- Note that the search query is case-insensitive, so "Aaron" and "aaron" will return the same results.

- If we want to search for multiple words, we can use boolean mode to specify how the words should be matched.

```sql
SELECT * FROM people WHERE MATCH(first_name, last_name, bio) AGAINST('Aaron +Smith');
```


## Boolean mode

- Boolean mode allows us to specify how the search query should be matched. In this mode, we can use the + and - operators to specify whether a word should be included or excluded from the results.

For more advanced full-text searches, you can switch to boolean mode. Boolean mode allows you to use modifiers, like +, -, >, <, and parentheses in your search query.

Here's an example of a boolean search query:

```sql
SELECT * FROM people
  WHERE MATCH(first_name, last_name, bio) AGAINST('+Aaron -Francis' IN BOOLEAN MODE);
```

This query will search for all rows where "Aaron" appears and exclude any rows where "Francis" appears. The + indicates that "Aaron" is a required search term, and the - indicates that "Francis" is excluded.

In boolean mode, you can also add quotation marks to search for an exact phrase or use the NEAR operator to search for words within a certain distance of each other.

- This query will return all rows where the word "Aaron" appeared, but the word "Francis" did not.

- Note that we're using the IN BOOLEAN MODE modifier to specify that we want to use boolean mode.

- We can also use the > and < operators to specify a minimum or maximum number of times a word should appear in the results.

```sql
SELECT * FROM people
  WHERE MATCH(first_name, last_name, bio) AGAINST('Aaron >1' IN BOOLEAN MODE);
```

- This query will return all rows where the word "Aaron" appeared more than once.

- We can also use the > and < operators to specify a minimum or maximum number of times a word should appear in the results.

```sql
SELECT * FROM people
  WHERE MATCH(first_name, last_name, bio) AGAINST('Aaron >1' IN BOOLEAN MODE);
```


## Sorting results by relevancy

When using natural language mode, MySQL automatically orders the results by their relevancy score, with the most relevant result at the top. However, in Boolean mode, you need to manually sort the results.

Luckily, MySQL returns the relevancy score as part of the search query results. You can use this score to sort the results using an ORDER BY statement.

## Conclusion

Full-text indexing and searching in MySQL can be a powerful tool for searching across multiple columns and finding specific words or phrases within text blocks. While it may not be as robust as a standalone search engine, it's a great option if you're already using MySQL as your database and want to avoid adding another tool to your infrastructure.

With the ability to add full-text indexes and implement both natural language and boolean searches, you can fine-tune your search queries to find exactly what you need. So next time you need to search across multiple columns in your database, give full-text indexing a try!
