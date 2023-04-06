# 1.8 Dates

## Understanding MySQL data types: storing temporal data:
- As your MySQL database grows in complexity, it becomes increasingly essential to understand the various data types used to store different types of information. In this video, we will take a closer look at storing time-related data in MySQL and explore the five different data types that are available for this purpose.

## The importance of time data:
- Before we dive into the different data types available for storing temporal data, it's essential to understand whether you need to store time-related data in the first place. Depending on your application, you may need to store dates, times, timestamps, years, or other temporal data.

- So, the first question you need to ask yourself is, "Do I need to store time?" If you only need to store the date, then you'll be looking at different data types than if you need to store the date plus time.

## The five different types for storing temporal data
- Let's take a closer look at the five different types you can use to store time-related data in MySQL.

----------------------------------------------------------------
Data type |  Bytes |     Min             |      Max            |
----------|--------|---------------------|---------------------|
DATE      |  3     | 1000-01-01          | 9999-12-31          |
DATETIME  |  8     | 1000-01-01 00:00:00 | 9999-12-31 23:59:59 |
TIMESTAMP |  4     | 1970-01-01 00:00:01 | 2038-01-19 03:14:07 |
YEAR      |  1     | 1901                | 2155                |
TIME      |  3     | -838:59:59          | 838:59:59           |
----------------------------------------------------------------

1 - `Date` : If you only need to store the date, then the DATE type column is your best bet. It is a three-byte data type that can store a vast range of data from the year 1,000 to 9,999.

2 - `Datetime` : If you need to store both the date and time, then DATETIME and TIMESTAMP are the two options you have. DATETIME is an eight-byte data type that can store a massive range of data. So, if you need to store time data up to the year 9,999, DATETIME is the way to go.

3 - `TIMESTAMP` : on the other hand, is a four-byte data type that can store a more limited range of data, from the year 1970 to 2038-01-19. This limitation is referred to as the "2038 problem." If you only need to store time data within this range, TIMESTAMP is the more compact and efficient option.

4 - `YEAR` : If you need to store a year between 1901 and 2155, YEAR would be the most compact way to do it. This type is not very commonly used.

5 - `TIME` : The TIME data type is used to store hours, minutes, and seconds. It can store more than 24 hours, which is useful for storing intervals. This type is useful for a 10-day range denominated in hours, minutes, and sec

-------------

## Choosing between DATETIME and TIMESTAMP

If you need to store both the date and time, you'll need to choose between DATETIME and TIMESTAMP. Both data types have their advantages and disadvantages, so it's essential to understand the differences between the two.

```sql
CREATE TABLE timezone_test(
    'timtstamp' TIMESTAMP  NULL,
    'datetime' DATETIME  NULL 
);

INSERT INTO timezone_test (timtstamp, datetime) VALUES (
    '2023-01-01 00:00:00',
    '2023-01-01 00:00:00'
);

SELECT * FROM timezone_test;

-- output
+---------------------+---------------------+
| timtstamp           | datetime            |
+---------------------+---------------------+
| 2023-01-01 00:00:00 | 2023-01-01 00:00:00 |
+---------------------+---------------------+

set session time_zone = '+05:00';

SELECT * FROM timezone_test;

-- output
+---------------------+---------------------+
| timtstamp           | datetime            |
+---------------------+---------------------+
| 2023-01-01 05:30:00 | 2023-01-01 00:00:00 |
+---------------------+---------------------+

```

As you can see, the TIMESTAMP data type is converted to UTC when added to the database and back to your time zone when retrieved. In contrast, DATETIME does not handle time zones at all. Whatever you put in, you get back out.

This difference is essential to consider when choosing between these two data types, especially if your application requires handling different time zones.

-----

## Storage size

The first difference between DATETIME and TIMESTAMP is storage size. DATETIME is an eight-byte data type, while TIMESTAMP is a four-byte data type. This makes TIMESTAMP more compact and more efficient in terms of storage space.

-----

## Range of data

The second difference between these two data types is the range of data they can store. As mentioned earlier, DATETIME can store time data up to the year 9,999. In contrast, TIMESTAMP can store data only from 1970 to 2038.

Due to this limitation, you may have to use DATETIME in cases where you need to store data beyond 2038.

-----


## Time zones

One final difference between DATETIME and TIMESTAMP is how they handle time zones. With DATETIME, MySQL does not handle time zones at all. Whatever you put in, you get back out. With TIMESTAMP, MySQL tries to help you by converting values to UTC when added to the database and back to your time zone when retrieved.

This difference is essential to consider when choosing between these two data types, especially if your application requires handling different time zones.


-----


## Conclusion

When it comes to storing time-related data in MySQL, it's essential to choose the right data type based on your needs. The DATE, DATETIME, and TIMESTAMP data types are the most commonly used, with TIMESTAMP being the most compact and efficient way to store date and time data.

When choosing between DATETIME and TIMESTAMP, consider storage size, the range of data needed, and how time zones are handled. Ultimately, utilizing MySQL effectively for storing and handling temporal data can help your application function efficiently and accurately.