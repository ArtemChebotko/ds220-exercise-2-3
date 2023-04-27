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
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 4</span>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Explore the KillrVideo dataset</div>

With all of the success you've been having on the video sharing development team, you have been promoted and assigned to work on a high-priority project to incorporate movie content into the KillrVideo application.
Your new team is normalizing their video and actor metadata into separate tables and currently are stuck figuring out how to join tables in Cassandra. Having been around the Cassandra block a few times, you know that JOINs are expensive and not supported. It is up to you to show your team the optimal way of performing these queries.

The video metadata is similar to what was in the video sharing domain:

| Column Name      | Data Type |
|------------------|-----------|
| video_id         | timeuuid  |
| added_date       | timestamp |
| description      | text      |
| encoding         | video_encoding |
| tags             | set<text> |
| title            | text      |
| user_id          | uuid      |

<br/>

There is also the additional following metadata:

| Column Name      | Data Type |
|------------------|-----------|
| actor            | text      |
| character        | text      |
| genre            | text      |

<br/>

With this metadata, the data model must support the following queries:
* Q1: Retrieve videos an actor has appeared in (newest first).
* Q2: Retrieve videos within a particular genre (newest first).


✅ Review the contents of the CSV files with video metadata:
```
cat assets/videos_by_genre.csv
```

```
cat assets/videos_by_actor.csv
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
