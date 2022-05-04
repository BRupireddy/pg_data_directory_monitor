# pg_data_directory_monitor
An external module providing a way to monitor PostgreSQL data directory's disk space and disallowing writes to the database (either by setting default_transaction_read_only or transaction_read_only or any other means) whenever data directory occupies, say, a preconfigured disk percentage X% of total available disk space. This module helps to avoid crashes due to out of disk space or "no space left on device". It can check the total disk space on which the data directory is hosted/mounted and frequently (every minute or so, after a configurable amount of time) check the data directory total size.

Also, possibly reason about the data directory growth - user's database, WAL file growth (archive failure, infrequent checkpoints, inactive replication slots, high-write activity) etc.

Although this module looks invasive in the sense that it disallows writes, it helps to avoid crashes which might lead to disk scalings (given the fact that disk scale operations aren't always cheaper and easier)  to bring the server back online.

NOTE: This module is under development.
