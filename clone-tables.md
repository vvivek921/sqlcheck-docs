---
description: t
---

# Cloning Tables or Columns based on meta data

### Description

For the chinook database, imagine that you have lot of tracks to store and CRUD queries are very slow.

One quick solution would be to create a new table for every track based on it's genre id . 

So you will end up with multiple tables where each table will be tracks\_123, where 123 is the genre id for all the tracks in that table.

This solution seems decent as it improves CRUD by reducing the size of data. 

### Why is it bad?

But think about the below questions:

* How do you maintain unique id across all tracks tables'.
* Suppose you mislabeled a track's genre id. Does running an update on genre id suffice?
* Suppose you want to join tracks with some other tables and add a filter an tracks name. How will you do it?
* Later you realized that tracks genre distribution is not uniform and you would want to change how tracks are manually partitioned across tables. What will be the changes in your application logic queries?

The cons generally outweight the pros for manual partitioning.

### Fix

 Better options are:

*  would be to use databases inbuilt horizontal partitioning as mentioned [here](https://dev.mysql.com/doc/refman/8.0/en/partitioning-types.html).
* or relook at normalization and do a vertical partitioning and store some of the columns in a separate table. 

