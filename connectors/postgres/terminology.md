---
description: Definitions of the Postgres terminology we use in our errors and messaging
---

# Terminology

<table><thead><tr><th width="192">Term</th><th width="345.3333333333333">Definition</th><th>Postgres Documentation</th></tr></thead><tbody><tr><td>Primary Key</td><td>A column or group of columns that can be used to uniquely identify a row in a table. This requires that the values be both unique and not empty. </td><td><a href="https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-PRIMARY-KEYS">5.4.4. Primary Keys</a></td></tr><tr><td>Foreign Key</td><td>A column that matches the value appearing in a column of another table and maintains the referential integrity between two related tables.</td><td><a href="https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-FK">5.4.5. Foreign Keys</a></td></tr><tr><td>Generated Column</td><td>Whalesync requires that your primary key has a default value generated via a function. This guarantees that there will be a value even if you don't map the primary key column.</td><td><a href="https://www.postgresql.org/docs/current/ddl-default.html">5.2. Default Values</a></td></tr></tbody></table>

Whalesync requires that every table you map has a **single** primary key and that it is generated because it is essential that we can uniquely identify a row of data every time in order to be able to sync it correctly to or from another application. The primary key guarantees uniqueness and the generation means there will always be a good, viable value.&#x20;

See [Postgres snippets](primary-key-snippets.md) for helpful generation functions as well as defining the primary and foreign keys of a table.
