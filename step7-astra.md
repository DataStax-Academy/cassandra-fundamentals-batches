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
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 7 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Deleting a movie rating</div>

Finally, for your practice, use a *multi-partition batch* to delete the previously inserted and updated movie rating.

✅ Delete the movie rating:  
<details>
  <summary>Solution</summary>

```
BEGIN BATCH
  DELETE FROM ratings_by_user 
  WHERE email = 'joe@datastax.com' 
    AND title = 'Alice in Wonderland' 
    AND year  = 2010;
  DELETE FROM ratings_by_movie 
  WHERE email = 'joe@datastax.com' 
    AND title = 'Alice in Wonderland' 
    AND year  = 2010;
APPLY BATCH;  
```

</details>

<br/>

✅ Verify that the rating is no longer in the tables:
<details>
  <summary>Solution</summary>

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

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

