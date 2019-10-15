# External data storage

### Description

For the [Chinook](https://dataschool.com/assets/images/Chinook%20ERD.png) data model, you might be thinking about adding a photo for album cover.  One solution might be to add photos in a File system and add a column in the albums table, pointing to the photo.

### Why is it bad?

* Every deletion in the albums row should be accompanied by a deletion in the file system. But the database doesn't guarantee atomicity.
* You have to ensure backups in the filesystem containing images separately. That's an additional over head for the DBA.

### Fix

Use the Blob data type to store images in the datastore row.

