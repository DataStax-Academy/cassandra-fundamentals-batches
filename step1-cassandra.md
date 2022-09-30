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
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Atomic batches</div>

In Cassandra, individual insert, update and delete operations are atomic and isolated, meaning that 
either an operation occurs or nothing occurs (atomicity) and any partially updated data is not visible (isolated) 
to other operations. To achieve atomicity for a set of operations, Cassandra provides atomic batches. 

An *atomic batch* can group related insert, update and delete operations into 
a single indivisible statement that guarantees *atomicity* during its execution. More specifically, 
in the context of batches, *atomicity* means that if at least one operation in a batch succeeds, 
all other operations are guaranteed to succeed.

Logically, there are two categories of batches that provide different guarantees and support different use cases: 
- A *single-partition batch* is an atomic batch where all operations work on the same partition and that, under the hood, 
can be executed as a single write operation. As a result, single-partition batches guarantee both 
all-or-nothing *atomicity* and *isolation*. The main use case for single-partition batches is 
updating *related data* that may become corrupt unless atomicity is enforced.
- A *multi-partition batch* is an atomic batch where operations work on different partitions 
that belong to the same table or different tables. Multi-partition batches only guarantee *atomicity*. Their main use case 
is updating *the same data* duplicated across multiple partitions due to denormalization. Atomicity ensures that all duplicates 
are consistent.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
