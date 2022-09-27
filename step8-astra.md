<!-- TOP -->
<div class="top">
  <img src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-logo.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Tables with Single-Row Partitions in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 8 of 9</span>
 <a href='command:katapod.loadPage?[{"step":"step9-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">What tables with single-row partitions are good for?</div>

In Cassandra, tables are designed to support specific queries. Tables with 
single-row partitions are generally used to store and retrieve entities 
by their unique identifiers, such as retrieving a *user by email* or *movie by title and year*.

Of course, it is possible to use tables with 
single-row partitions for relationships, such as *user rated movie* in the example below, but tables 
with multi-row partitions are much more suitable for that. 
 
```
-- Not a good way to 
-- store relationships ... 
CREATE TABLE IF NOT EXISTS user_rated_movie (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  PRIMARY KEY ((email, title, year))
);

-- Tables with multi-row partitions 
-- are the way to go ...
-- Get all rating left by a user
CREATE TABLE IF NOT EXISTS ratings_by_user (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  PRIMARY KEY ((email), title, year)
);
--  Get all ratings left for a movie
CREATE TABLE IF NOT EXISTS ratings_by_movie (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  PRIMARY KEY ((title, year), email)
);
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step9-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

