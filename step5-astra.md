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
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 5 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Updating a shopping cart</div>

Next, for your practice, use a *single-partition batch* to add another movie into the same shopping cart and update the running total. 

✅ Update the shopping cart: 
<details>
  <summary>Solution</summary>

```
BEGIN BATCH
  INSERT INTO shopping_cart 
         (cart_id, title, year, price, user) 
  VALUES (b7255608-4a42-4829-9b84-a355e0e5100d, 
         'Edward Scissorhands', 1990, 3.99, 
         'joe@datastax.com');
  UPDATE shopping_cart SET total = 6.97
  WHERE cart_id = b7255608-4a42-4829-9b84-a355e0e5100d
  IF total = 2.98;
APPLY BATCH;  
```

</details>

<br/>

✅ Retrieve the shopping cart:
<details>
  <summary>Solution</summary>

```
SELECT total, price, title, year 
FROM shopping_cart
WHERE cart_id = b7255608-4a42-4829-9b84-a355e0e5100d;
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

