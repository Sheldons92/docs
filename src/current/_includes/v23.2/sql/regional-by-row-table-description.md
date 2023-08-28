In a _regional by row_ table, individual rows are optimized for access from different home regions. Every row in a regional by row table has a [column of type `crdb_internal_region`]({% link {{ page.version.version }}/alter-table.md %}#crdb_region) that represents the row's home region. By default, this column is called `crdb_region` and is hidden. The `REGIONAL BY ROW` setting automatically divides a table and all of [its indexes]({% link {{ page.version.version }}/table-localities.md %}#indexes-on-regional-by-row-tables) into [partitions]({% link {{ page.version.version }}/partitioning.md %}), with each partition optimized for access from a different region. Like [regional tables](table-localities.html#regional-tables), _regional by row_ tables are optimized for access from a single region. However, that region is specified at the row level instead of applying to the whole table.

Use regional by row tables when your application requires low-latency reads and writes at a row level where individual rows are primarily accessed from a single region. For example, a users table in a global application may need to keep some users' data in specific regions for better performance.

For an example of a table that can benefit from the _regional by row_ setting in a multi-region deployment, see the `users` table from the [MovR application]({% link {{ page.version.version }}/movr.md %}).

For instructions showing how to set a table's locality to `REGIONAL BY ROW` and configure its home regions, see [`ALTER TABLE ... SET LOCALITY`]({% link {{ page.version.version }}/alter-table.md %}#crdb_region).