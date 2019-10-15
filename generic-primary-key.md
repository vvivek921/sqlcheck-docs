# Namesake Primary key

### Description

It has become so common to use ID as the primary key in a table, that we that has kind of unspoken definition of primary key.

But primary key is not a column, it is a constraint to uniquely identify each row.

### Some misuses

Examples:

* In a table containing information on albums, creating two columns ID and ALBUM\_ID. You could, because of a bug in application, end up adding up the same album twice into the database.
*  create an association tables between albums and artists and have three columns ID, ALBUM\_ID, ARTIST\_ID. Here ID is not serving any purpose. It doesn't stop you from adding an album to artist association twice.

### Fix

Think of a primary key as a constraint, not a column as such. One rule of thumb is to refrain from ID named columns.



