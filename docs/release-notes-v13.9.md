# Percona Distribution for PostgreSQL 13.9 (2022-11-24)

| Release date:     | November 24, 2022      |
|:------------------|:----------------------|
| **Installation**: | [Installing Percona Distribution for PostgreSQL](installing.md) |


Percona Distribution for PostgreSQL is a collection of tools to assist you in managing PostgreSQL. Percona Distribution for PostgreSQL
installs PostgreSQL and complements it by a selection of extensions that
enable solving essential practical tasks efficiently.

This release of Percona Distribution for PostgreSQL is based on [PostgreSQL 13.9](https://www.postgresql.org/docs/13/release-13-9.html).

Percona Distribution for PostgreSQL now includes the [meta-packages](installing.md/package-contents) that simplify its installation. The `percona-ppg-server` meta-package installs PostgreSQL and the extensions, while `percona-ppg-server-ha` package installs high-availability components that are recommended by Percona.


The following is the list of extensions available in Percona Distribution for PostgreSQL.

| Extension           | Version        | Description                  |
| ------------------- | -------------- | ---------------------------- |
| [Patroni](https://patroni.readthedocs.io/en/latest/) | 2.1.4 | a HA (High Availability) solution for PostgreSQL |
| [Pgaudit](https://www.pgaudit.org/)             | 1.5.2   | provides detailed session or object audit logging via the standard logging facility provided by PostgreSQL                |
|[`pgAudit set user`](https://github.com/pgaudit/set_user)| 4.0.0|  provides an additional layer of logging and control when unprivileged users must escalate themselves to superuser or object owner roles in order to perform needed maintenance tasks.|
| [pgBackRest](https://pgbackrest.org/)           | 2.41    | a backup and restore solution for PostgreSQL       |
|[`pgBadger`](https://github.com/darold/pgbadger) | 12.0       | a fast PostgreSQL Log Analyzer.|
|[`pgBouncer`](https://www.pgbouncer.org/) | 1.17.0 | lightweight connection pooler for PostgreSQL|
| [pg_repack](https://github.com/reorg/pg_repack) | 1.4.8   | rebuilds PostgreSQL database objects           |
| [pg_stat_monitor](https://github.com/percona/pg_stat_monitor)| 1.1.1 | collects and aggregates statistics for PostgreSQL and provides histogram information.       |
| [PostgreSQL Common](https://packages.debian.org/sid/percona-postgresql-common)| 241 | PostgreSQL database-cluster manager. It provides a structure under which multiple versions of PostgreSQL may be installed and/or multiple clusters maintained at one time.|
|[`wal2json`](https://github.com/eulerto/wal2json) |2.5        | a PostgreSQL logical decoding JSON output plugin.|
|[HAProxy](http://www.haproxy.org/) | 2.5.9 | a high-availability and load-balancing solution |

Percona Distribution for PostgreSQL also includes the following packages:

- `llvm` 12.0.1 packages for Red Hat Enterprise Linux 8  and compatible derivatives. These fix compatibility issues with LLVM from upstream. 
- supplemental ETCD packages which can be used for setting up Patroni clusters. These packages are available for the following operating systems:

|  Operating System   |Package               | Version | Description        |
| ------------------- | ---------------------| --------| -------------------|
| RHEL 7              |`python3-python-etcd` | 0.4.3   | A Python client for ETCD     |
| RHEL 8              | `etcd`               | 3.3.11  | A consistent, distributed key-value store|
|                     | `python3-python-etcd`| 0.4.3   | A Python client for ETCD     |


                                                      
Percona Distribution for PostgreSQL is also shipped with the [libpq](https://www.postgresql.org/docs/13/libpq.html) library. It contains "a set of
library functions that allow client programs to pass queries to the PostgreSQL
backend server and to receive the results of these queries." 
