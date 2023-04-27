<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Exercise 2.3: Denormalizing</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:academy@datastax.com">email</a>.</span>
  </div>
</div>


<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 3 of 4</span>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Create a "videos_by_actor" table</div>

Notice that our `encoding` column is actually something called a User Defined Type (or UDT for short). Fear not! We will be talking about these in the next exercise. For now, copy and paste this code to create the UDT so that our create table works correctly.

✅ Create the `encoding` UDT:
```
CREATE TYPE IF NOT EXISTS video_encoding (
  encoding TEXT,
  height INT,
  width INT,
  bit_rates SET<TEXT>
);
```

✅ Create table `videos_by_actor`:
```
CREATE TABLE videos_by_actor ( 
  actor TEXT,
  added_date TIMESTAMP, 
  video_id TIMEUUID, 
  character_name TEXT, 
  description TEXT,
  encoding FROZEN<video_encoding>, 
  tags SET<TEXT>,
  title TEXT,
  user_id UUID,
  PRIMARY KEY ((actor), added_date, video_id, character_name) 
) WITH CLUSTERING ORDER BY (added_date DESC, video_id ASC, character_name ASC);
```


✅ Load `videos_by_actor.csv` into the `videos_by_actor` table using the `COPY` command:
```
COPY videos_by_actor (actor,added_date,video_id,character_name,description,encoding,tags,title,user_id) 
FROM 'assets/videos_by_actor.csv' WITH HEADER = true;
```

✅ Run a query to retrieve the video information for a particular actor:
```
SELECT * FROM videos_by_actor WHERE actor = 'Leonardo DiCaprio' LIMIT 10;
```

✅ Try selecting just the actor and the `added_date` columns:
```
SELECT actor, added_date FROM videos_by_actor WHERE actor = 'Leonardo DiCaprio' LIMIT 10;
```

Notice the order of added dates.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
