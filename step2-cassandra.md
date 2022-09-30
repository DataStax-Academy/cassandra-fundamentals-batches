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
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 2 of 8</span>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Syntax</div>

For batches, Cassandra Query Language has the `BEGIN BATCH` statement with the following simplified syntax:

<pre class="non-executable-code">
BEGIN [UNLOGGED | COUNTER] BATCH 
  INSERT ...; | UPDATE ...; | DELETE ...;
  [...]
APPLY BATCH;
</pre>

A batch starts with `BEGIN BATCH` and ends with `APPLY BATCH`. It can contain one or more 
`INSERT`, `UPDATE` or `DELETE` statements. Single-partition batches can even contain lightweight transactions, but
multi-partition batches cannot. The order of statements 
in a batch is not important as they can be executed in arbitrary order. 

Notice the `UNLOGGED` and `COUNTER` options. They should never be used as they have no useful applications or 
there exist better alternatives. Unlogged batches break the atomicity guarantee and counter batches are not safe to 
replay automatically as counter updates are not idempotent.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
