---
description: Create multiple Columns to store multiple attribute values for a key
---

# Data In Metadata

### Description

Suppose you have an Orders table in your retail database. You want to tag each order few attributes such as "first order","coupon purchase",etc.

One possible solution could be as below:

```sql
CREATE TABLE Orders (
  Id      INT,
  OrderDate DATE,
  ------
  TAG_1 VARCHAR(10),
  TAG_2 VARCHAR(10),
  TAG_3 VARCHAR(10),
  TAG_4 VARCHAR(10),
  TAG_5 VARCHAR(10)
  PRIMARY KEY (Id)
);
```

### Why is it bad?

These seems like a decent solution, but imagine how would you:

* Query all Orders with tag "coupon purchase"
* What if an Order has more than 5 tags
* Get aggregate metrics in Tag data on orders.

### Fix

The best solution for the above is to move all tags to a separate table and reference to the orders table with order\_id.

```sql
CREATE TABLE Tags (
  Id      INT,
  order_id order_id FOREIGN,
  ------
);
```



