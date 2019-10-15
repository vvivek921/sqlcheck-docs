# Skipping foreign key constraints

### Description

Consider the relation of artists and albums from  [Chinook](https://dataschool.com/assets/images/Chinook%20ERD.png) data model for this article.

From a logical layout perspective, You want album to refer to an artist id only if such as artist exists. Basically what you want is data integrity. You can maintain this at the application level or at the database level.

### Why is it bad?

People give lot of reasons for not maintaining this at the database level by not defining the foreign key constraint:

* Adding foreign key constraints adds overhead on query latency 
* The index created for foreign key will take up more RAM,etc

### Fix

But there is one reason why you should NOT skip foreign key constraints: Developers are humans and tend to make mistakes. Not having foreign constraints would mean you can delete an artist from artists table and end up with albums which have an invalid artist id. It's better to be penny wise and pay upfront by adding foreign key constraints rather than be pound foolish and end up in situations where you have to run after getting your data in database restored to a backed up version, as you have deleted artists who have albums tagged to them.



