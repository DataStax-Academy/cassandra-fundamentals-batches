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
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 8 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"finish-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Batch limitations</div>

*Single-partition batches* are quite efficient and can performance better than individual statements 
because batches save on client-coordinator and coordinator-replicas communication. However, sending 
a large batch with hundreds of statements to one coordinator node can also negatively affect 
workload balancing. 

*Multi-partition batches* are substantially more expensive as they require maintaining a *batchlog* 
in a separate Cassandra table. Therefore, even with respect to the main use case of updating 
the same data duplicated across multiple partitions due to denormalization, use multi-partition batches 
only when atomicity is truly important for your application. There are other ways to check and ensure consistency among duplicates 
for less critical data without sacrificing write performance. 

Finally, do not use batches to group operations just for the sake of grouping. 
This example is an anti-pattern:

```
-- This is an anti-pattern
BEGIN BATCH
  INSERT INTO users (email, name, age, date_joined) 
  VALUES ('joe@datastax.com', 'Joe', 25, '2020-01-01');
  INSERT INTO users (email, name, age, date_joined) 
  VALUES ('jen@datastax.com', 'Jen', 27, '2020-01-01');
  INSERT INTO movies (title, year, duration, avg_rating, price) 
  VALUES ('Alice in Wonderland', 2010, 108, 8.33, 1.99);
  INSERT INTO movies (title, year, duration, avg_rating, price) 
  VALUES ('Alice in Wonderland', 1951, 75, 6.5, 0.99);  
APPLY BATCH;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"finish-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

