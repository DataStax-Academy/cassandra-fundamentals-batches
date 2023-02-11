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
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 4 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Creating a shopping cart</div>

In this example, we use a *single-partition batch* to add two movies into a new shopping cart 
with id `b7255608-4a42-4829-9b84-a355e0e5100d`. We also add up the movie prices and insert 
the resulting total using a separate statement. This is a classic example of when atomicity is important: 
all the three `INSERT` statements are related and must succeed for the cart state to be correct. In addition, 
since this is a new shopping cart, we use a lightweight transaction with `IF NOT EXISTS` 
to ensure that the batch cannot be executed on an existing shopping cart. `IF NOT EXISTS` can be used with any of 
the `INSERT` statements because this single-partition batch is executed as a single write operation internally.

✅ Create the table:
```
DROP TABLE IF EXISTS shopping_cart;
CREATE TABLE shopping_cart (
  cart_id UUID,
  title TEXT,
  year INT,
  price DECIMAL,
  user TEXT STATIC,
  total DECIMAL STATIC,
  PRIMARY KEY ((cart_id), title, year)
);
```

✅ Insert two movies into the shopping cart: 
```
BEGIN BATCH
  INSERT INTO shopping_cart 
         (cart_id, title, year, price, user) 
  VALUES (b7255608-4a42-4829-9b84-a355e0e5100d, 
         'Alice in Wonderland', 2010, 1.99, 
         'joe@datastax.com');
  INSERT INTO shopping_cart 
         (cart_id, title, year, price, user) 
  VALUES (b7255608-4a42-4829-9b84-a355e0e5100d, 
         'Alice in Wonderland', 1951, 0.99, 
         'joe@datastax.com');
  INSERT INTO shopping_cart (cart_id, total) 
  VALUES (b7255608-4a42-4829-9b84-a355e0e5100d, 2.98)
  IF NOT EXISTS;
APPLY BATCH;  
```

✅ Retrieve the shopping cart:
```
SELECT total, price, title, year 
FROM shopping_cart
WHERE cart_id = b7255608-4a42-4829-9b84-a355e0e5100d;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

