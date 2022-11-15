<!-- TOP -->
<div class="top">
  <img src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-logo.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Atomicity and Batches in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step2-astra"}]' 
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 3 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Connect to Astra DB and create a database</div>

✅ Create an application token with the *Database Administrator* role to access Astra DB. Skip this step is you already have a token.

<ul>
  <li>Sign in (or sign up) to your Astra account at <a href="https://astra.datastax.com" target="_blank">astra.datastax.com</a></li>
  <li>Create an application token with the <i>Database Administrator</i> role by following <a href="https://awesome-astra.github.io/docs/pages/astra/create-token/" target="_blank">these instructions</a></li>
</ul>

You can reuse the same token in our other labs, too.

✅ Setup Astra CLI by providing your application token:
```
astra setup
```

✅ List your existing Astra DB databases:
```
astra db list
```

✅ Create database `cassandra-fundamentals` and keyspace `ks_batches` if they do not exist:
```
astra db create cassandra-fundamentals -k ks_batches --if-not-exist --wait
```

This operation may take a bit longer when creating a new database or resuming an existing hibernated database.

✅ Verify that database `cassandra-fundamentals` is `ACTIVE` and keyspace `ks_batches` exists:
```
astra db get cassandra-fundamentals
```

✅ Start the CQL shell and connect to database `cassandra-fundamentals` and keyspace `ks_batches`:
```
clear
astra db cqlsh cassandra-fundamentals -k ks_batches
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
 <a href='command:katapod.loadPage?[{"step":"step2-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
