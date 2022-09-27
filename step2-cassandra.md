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
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 2 of 9</span>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Creating tables</div>

To create a table, Cassandra Query Language has the `CREATE TABLE` statement with the following simplified syntax:

<pre class="non-executable-code">
CREATE TABLE [ IF NOT EXISTS ] [keyspace_name.]table_name
( 
  column_name data_type [ , ... ] 
  PRIMARY KEY ( 
   ( partition_key_column_name  [ , ... ] )
   [ clustering_key_column_name [ , ... ] ]
  )     
)
[ WITH CLUSTERING ORDER BY 
   ( clustering_key_column_name ASC|DESC [ , ... ] )
];
</pre>

First, notice that a table is created within an existing keyspace. If a *keyspace name* is omitted, the current working keyspace is used.

Second, *keyspace*, *table* and *column* *names* can contain alphanumeric characters and underscores. By default, 
names are case-insensitive, but case sensitivity can be forced by using double quotation marks around a name.

Third, there are many CQL *data types*, including native, collection and user-defined data types. For now, we will use some of the simplest and self-descriptive ones like `TEXT`, `INT`, `FLOAT`, and `DATE`.

Fourth, notice that there are additional 
parentheses around the partition key columns that can be omitted when the partition key has only one column (a.k.a. 
*simple partition key*) and are required when the partition key has more than one column (a.k.a. 
*composite partition key*). 

Finally, when a clustering key is defined, ordering is optionally specified in the last clause with ascendant order being the default. 

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
