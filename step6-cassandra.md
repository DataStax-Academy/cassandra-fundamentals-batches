<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Atomicity and Batches in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 6 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Adding a movie rating</div>

In this example, we use a *multi-partition batch* to add the same movie rating into two different tables 
`ratings_by_user` and `ratings_by_movie`. Since the tables store copies of the same data, any inserts, updates and deletes 
must go to both tables. In this case, atomicity is important to ensure that copies of the same data are in sync.
This is a classic example of using multi-partition batches for keeping denormalized and duplicated data consistent.

✅ Create the tables:
```
DROP TABLE IF EXISTS ratings_by_user;
CREATE TABLE ratings_by_user (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  PRIMARY KEY ((email), title, year)
);

DROP TABLE IF EXISTS ratings_by_movie;
CREATE TABLE ratings_by_movie (
  title TEXT,
  year INT,
  email TEXT,
  rating INT,
  PRIMARY KEY ((title, year), email)
);
```

✅ Insert the movie rating: 
```
BEGIN BATCH
  INSERT INTO ratings_by_user (email, title, year, rating) 
  VALUES ('joe@datastax.com', 'Alice in Wonderland', 2010, 9);
  INSERT INTO ratings_by_movie (email, title, year, rating) 
  VALUES ('joe@datastax.com', 'Alice in Wonderland', 2010, 9);
APPLY BATCH;  
```

✅ Update the movie rating: 
```
BEGIN BATCH
  UPDATE ratings_by_user SET rating = 10 
  WHERE email = 'joe@datastax.com' 
    AND title = 'Alice in Wonderland' 
    AND year  = 2010;
  UPDATE ratings_by_movie SET rating = 10 
  WHERE email = 'joe@datastax.com' 
    AND title = 'Alice in Wonderland' 
    AND year  = 2010;
APPLY BATCH;  
```

✅ Retrieve the movie rating:
```
SELECT * FROM ratings_by_user  
WHERE email = 'joe@datastax.com' 
  AND title = 'Alice in Wonderland' 
  AND year  = 2010;
SELECT * FROM ratings_by_movie  
WHERE email = 'joe@datastax.com' 
  AND title = 'Alice in Wonderland' 
  AND year  = 2010;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

