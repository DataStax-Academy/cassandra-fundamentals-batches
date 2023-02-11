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
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 3 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Connect to Cassandra and create a keyspace and tables</div>

✅ Start Cassandra:
```
./cassandra
```

✅ Start the CQL shell:
```
cqlsh
```

✅ Create the keyspace:
```
CREATE KEYSPACE IF NOT EXISTS ks_batches
WITH replication = {
  'class': 'NetworkTopologyStrategy', 
  'DC-Houston': 1 };

USE ks_batches;
```

✅ Create and populate the tables:
```
CREATE TABLE IF NOT EXISTS users (
  email TEXT,
  name TEXT,
  age INT,
  date_joined DATE,
  PRIMARY KEY ((email))
);
INSERT INTO users (email, name, age, date_joined) 
VALUES ('joe@datastax.com', 'Joe', 25, '2020-01-01');
INSERT INTO users (email, name, age, date_joined) 
VALUES ('jen@datastax.com', 'Jen', 27, '2020-01-01');
INSERT INTO users (email, name, age, date_joined) 
VALUES ('jim@datastax.com', 'Jim', 31, '2020-05-07');

CREATE TABLE IF NOT EXISTS movies (
  title TEXT,
  year INT,
  duration INT,
  avg_rating FLOAT,
  price DECIMAL,
  PRIMARY KEY ((title, year))
);
INSERT INTO movies (title, year, duration, avg_rating, price) 
VALUES ('Alice in Wonderland', 2010, 108, 8.33, 1.99);
INSERT INTO movies (title, year, duration, avg_rating, price) 
VALUES ('Alice in Wonderland', 1951, 75, 6.5, 0.99);
INSERT INTO movies (title, year, duration, avg_rating, price) 
VALUES ('Edward Scissorhands', 1990, 98, 8.5, 3.99);
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
