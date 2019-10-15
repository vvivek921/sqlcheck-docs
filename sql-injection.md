# SQL Injection

### Description

When you write a query at application layer, which takes parameters of the query from the end user, the application should be defensive and should check for malicious input. 

### Why is it bad?

Consider the below query at application layer on \

What would happen if name were a string

```python
$ query = 'SELECT * FROM playlists WHERE name = ' + name + ';'
```

Imagine that the name is a request from the end user\(think web request from a web endpoint\) and it is being passed onto build a query without escaping it.

```text
";DROP DATABASE"
```

Well you wouldn't want to be in such a situation. 

Or let's consider this example

```python
$ query = 'SELECT * FROM playlists WHERE '+ key  +  ' = ' + value +  ';'
```

Maybe you have written this with an intent to add a dynamic where clause.

What would happen if key was 1 and and value was 1?  It would result in a full scan and all the rows in playlists would be returned.

### Fix

Look into [parametrization](https://rosettacode.org/wiki/Parametrized_SQL_statement) at application layer to avoid these issues.

