# 2.15: Invisible indexes

## Making indexes invisible in MySQL

Sometimes you might need to drop an index in MySQL, but you're not entirely sure of the ramifications. You might feel nervous and want to make sure you've looked at every query that uses this index. This is where making an index invisible in MySQL comes in handy. In this video, we'll look at how to make indexes invisible and why you might want to do so.



## Why make an index invisible?

- Making an index invisible in MySQL is a great way to test out the performance of your application without having to drop the index entirely. This can be useful if you're not sure if the index is being used or if you're not sure if it's being used correctly.

- For example, let's say we have a table with a full-text index on the first_name, last_name, and bio columns. We want to drop this index, but we're not sure if it's being used. We can make the index invisible and see if the application still runs as expected. If it does, we can be confident that the index isn't being used and we can drop it.

- If the application doesn't run as expected, we can make the index visible again and investigate why it's being used. This can help us determine if the index is being used correctly or if we need to make changes to the queries that use it.

- Note that making an index invisible in MySQL doesn't actually drop the index. It just makes it invisible to the optimizer. This means that the index will still be there and you can make it visible again at any time.

- There are times when you need to drop an index due to its inefficiency or because it's no longer used by your queries. However, before you do so, you get nervous and start thinking, "What if I've missed something?" Making an index invisible allows you to monitor how your queries perform without the index without having to rebuild it. If everything goes well, you can drop the index. But if something goes wrong, you can quickly turn the index back on without any hassle. Thus, making an index invisible reduces the risks and potential complications of dropping an index.

## How to make an index invisible?
- Making an index invisible is a straightforward process in MySQL:
```sql
ALTER TABLE people ALTER INDEX email_idx INVISIBLE;
```

This command makes the email_idx index invisible so that it is no longer used in any queries.

To verify that the index is invisible, you can use the show indexes from [table] command again. This time, you'll notice that the email_idx index still exists, but its "Visible" column is set to "NO."


- If you want to use the index again, you can revert it back to its visible state using the "alter index [index_name] visible" command.

```sql
ALTER TABLE people ALTER INDEX email_idx VISIBLE;
```

- This command makes the index visible again so that MySQL uses it in queries.

- Note that you can also make an index invisible when you create it. To do so, you can use the "invisible" keyword in the create index statement.

```sql
CREATE INDEX email_idx ON people (email) INVISIBLE;
```

- This command creates an invisible index called email_idx on the email column of the people table.

## Benefits of making an index invisible

Making an index invisible enables you to test your queries without risking data loss or any adverse impact on system performance. Once you make an index invisible, MySQL will stop using it in any queries, but it will still maintain this index's integrity. If something goes wrong during testing, it's easy to revert back to the original index state.

You can monitor your system's performance with minimal to no effect on your workflow. Once you are confident of your system's stability with the invisible index, you can fully drop the index.