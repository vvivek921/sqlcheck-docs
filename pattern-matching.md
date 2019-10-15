# Pattern Matching

### Description

You might have a VARCHAR column and you might want to run full table scan on that column by below query.

```sql
SELECT * FROM playlists WHERE name like "%sleep%";
```

### Why is it bad?

The above query is a very bad idea as it performs a full table scan and checks for thw substring sleep in each column.

### Fix

Alternatives:

* Use a specialised datastore for text search. Eg: elasticsearch
* Use storage engine or vendor that supports text search.







