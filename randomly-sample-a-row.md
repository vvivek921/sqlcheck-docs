# Randomly Sample a Row

### Description

Consider a case where you want to randomly pick a track from Chinook data model.

A common anti pattern would be 

```sql
SELECT * FROM tracks ORDER BY RAND() LIMIT 1;
```

### Why is it bad?

The above query will perform a full table scan.

### Fix

A better idea would be to try to sample on the primary id of the table. There are multiple variants to do this:

* Get min index and max index and generate a random number between those two\(assuming primamry key was auto increment and you don't delete rows\)
* Simplest solution would be to read all primary ids and pick an id randomly. All the ids should fit in memory. Even if you have 1 million rows, the ids should take MBs of RAM when in memory.

