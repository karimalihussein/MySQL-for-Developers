# 3.1: Introduction to queries

## Schema

We started at the very bottom with the schema. We talked about what does your data look like? How can we represent that in MySQL and what is the most compact way that we can store that data? That gives us our good foundation.

The schema is the structure of the data in your database. It defines the types of data that can be stored in your database, and the relationships between those types. The schema is defined in a file called `schema.graphql`, which is located in the `prisma` directory.

## Indexes

Then we talked about what indexes are, how they work, how the B-tree works, primary keys, secondary keys, how they're linked together. We talked about that for a long time!

Indexes are a way to speed up your queries. They are a data structure that is used to store data in a sorted order. They are used to quickly find data in a database without having to search through every single row. They are defined in the `schema.prisma` file.

## Queries

Now we're going to talk about queries. Queries are the way that we can read data from our database. We can use queries to get data from our database, to filter data, to sort data, to aggregate data, to do all kinds of things.

Now we get to talk about querying our data, actually accessing our data. We're going to use all of this knowledge that we learned before. We're going to use all of that in this section. I'm hoping, my hope is that all of those things we've learned already are going to make this section really easy. The number one rule for writing good queries is user indexes. So we already know so much about indexes that I'm hoping all of this is going to come together in the querying section.