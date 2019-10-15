# Using Null as an ordinary value

### Description

Consider the Chinook data model.

Suppose you are interested in all employees who are from city atlanta.

```sql
SELECT * FROM employees WHERE city = "atlanta";
```

and the below query will return all employees who are not from atlanta

```sql
SELECT * FROM employees WHERE city NOT IN ("atlanta");
```

What would happen if an employee didn't key in his city into the database? Would the second query return his information?

Well the answer is none of the queries would return his information.

### Why is it bad?

Null is treated as a separate value by itself and should be used with caution.

You might think

```sql
SELECT * FROM employees WHERE city =NULL;

```

would return the rows which have NULL in them. The answer is no. Any sort of comparision with NULL is not true.

### Fix

```sql
SELECT * FROM employees WHERE city IS NULL;

```

is the appropriate way to get all rows which have city marked as NULL.











