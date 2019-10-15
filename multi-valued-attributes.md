# Multi-valued Attribute

## Description

```sql
CREATE TABLE Playlists (id   SERIAL PRIMARY KEY,\
name VARCHAR(1000),track_id   BIGINT UNSIGNED,
FOREIGN KEY (track_id) REFERENCES Tracks(id));

INSERT INTO Playlists (id, name, track_id)VALUES 
(DEFAULT,'favorite', 12);
```

If you would want to store multiple tracks in a playlist, one option would be to convert track\_id to VARCHAR and store a comma separated list of ids in it. This seems like a convenient/easy way out.But what you notice is the other queries become slower and harder to maintain. We argue, through examples below, that it is a bad/anti pattern and should be avoided. We are using [Chinook](https://dataschool.com/assets/images/Chinook%20ERD.png) data model for this article.

## What is it bad?

You can see that below queries become slower

#### Querying Playlists for a Specific Track

```sql
SELECT * FROM Playlists WHERE track_id REGEXP'[[:<:]]12[[:>:]]';
```

#### Querying Tracks for a Given playlist

```sql
SELECT * FROM Playlists AS p JOIN Tracks AS t ON p.track_id REGEXP'[[:<:]]'|| t.id ||'[[:>:]]' WHERE p.id = 1;
```

#### Making Aggregate Queries

```sql
SELECT id as playlist_id, LENGTH(track_id) - LENGTH(REPLACE(track_id,',','')) + 1 AS tracks_in_one_playlist FROM Playlists;
```

#### Updating tracks in a playlist

```sql
UPDATE Playlists SET track_id = track_id ||','|| 1234 WHERE id = 1;

```

#### Validating Playlist primary keys

There are not database level validations as shown below

```sql
INSERT INTO Playlists (id, name, track_id)VALUES 
(DEFAULT,'favorite', '1,233,Not_A_ID');

```

#### Choosing a Separator Character

Say you want to change the separator from ',' to ':'. You have to update all the data in the database and all change queries such as aggregate queries and updating tracks in playlist.

#### List Length Limitations

Based on the length of ids used, you will have different maximum limit on the number of tracks you can associate with a playlist

```sql
UPDATE Playlists SET track_id ='12,13,14' WHERE id = 1;
UPDATE Playlists SET track_id ='121212,12345,1211467'WHERE id = 1;
```

## Fix

Use a standard to one to many representation. Infact check the Chinook to see the standard way to show 1 to many representation.

