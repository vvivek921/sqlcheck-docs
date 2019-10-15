# Column Wildcard Usage

### Description

```sql
CREATE TABLE Order (
-- others
status
VARCHAR(100) CHECK (status IN ('DELIVERED' , 'SHIPPING' , 'ACCEPTED' ))
);

```

The above seems like a good idea to add checks on the various values that status can take. Some databases support ENUM data type with a similar functionality

### Why is it bad?

The downside of the above is

*  what if you want to add one more status to the order say "PROCURING". That would be an alter query.
* What if you want to get all unique statuses. You would have to do a UNIQUE query.

### Fix

A better option would be to create a new table OrderStatus and refer to status\_id from Order table. That gives you enum like feature and also more flexibility for extending the enum values.





