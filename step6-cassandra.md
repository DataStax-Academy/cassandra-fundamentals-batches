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
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 6 of 9</span>
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Create table "genres"</div>

Our next table will store information about movie genres as shown below. This table 
with *single-row partitions* and a *simple partition key* is for you to define.

| genre     | description |
|-----------|-------------|
| Adventure |  A story about a protagonist who journeys to epic or distant places to accomplish something. |
| Fantasy   |  A story about magic or supernatural forces. | 

<br/>

✅ Create the table:
<details>
  <summary>Solution</summary>

```
CREATE TABLE IF NOT EXISTS genres (
  genre TEXT,
  description TEXT,
  PRIMARY KEY ((genre))
);
```

</details>

<br/>

✅ Insert the rows:
<details>
  <summary>Solution</summary>

```
INSERT INTO genres (genre, description) 
VALUES ('Adventure', 'A story about a protagonist who journeys to epic or distant places to accomplish something.');
INSERT INTO genres (genre, description) 
VALUES ('Fantasy', 'A story about magic or supernatural forces.');
```

</details>

<br/>

✅ Retrieve one row:
<details>
  <summary>Solution</summary>

```
SELECT * FROM genres
WHERE genre = 'Fantasy';
```

</details>

<br/>

✅ Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM genres;
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

