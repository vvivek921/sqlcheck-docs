# Implicit columns

### Description

We often use wildcards to fetch data.  The below seems like a reasonable way to get a track information

```sql
SELECT * FROM tracks WHERE id = 1
```

### Why is it good to not use wildcards?

However explicitly mentioning the columns has many advantages:

* The network latency reduces which reduces query latency. Basically you will have to move less\(explicitly stated\) columns from datastore to application which will improve query latency.
* When you read with a wildcard, most ORMs return integer indexed data. This sort of code is very brittle and will break when add another column.

### Fix

Explicitly mention your columns.

