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
 <a href='command:katapod.loadPage?[{"step":"step6-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 7 of 9</span>
 <a href='command:katapod.loadPage?[{"step":"step8-cassandra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Create table "actors"</div>

Our last table will store information about movie actors as shown below. This table 
with *single-row partitions* and a *composite partition key* is for you to define.

| first_name | last_name  | dob        |
|----------- |------------|------------|
| Johnny     | Depp       | 1963-06-09 |
| Anne       | Hathaway   | 1982-11-12 | 

<br/>

✅ Create the table:
<details>
  <summary>Solution</summary>

```
CREATE TABLE IF NOT EXISTS actors (
  first_name TEXT,
  last_name TEXT,
  dob DATE,
  PRIMARY KEY ((first_name, last_name))
);
```

</details>

<br/>

✅ Insert the rows:
<details>
  <summary>Solution</summary>

```
INSERT INTO actors (first_name, last_name, dob) 
VALUES ('Johnny', 'Depp', '1963-06-09');
INSERT INTO actors (first_name, last_name, dob) 
VALUES ('Anne', 'Hathaway', '1982-11-12');
```

</details>

<br/>

✅ Retrieve one row:
<details>
  <summary>Solution</summary>

```
SELECT * FROM actors
WHERE first_name = 'Johnny'
  AND last_name = 'Depp';
```

</details>

<br/>

✅ Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM actors;
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step6-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step8-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

