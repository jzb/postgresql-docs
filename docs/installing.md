# Install Percona Distribution for PostgreSQL

Percona provides installation packages in `DEB` and `RPM` format for 64-bit Linux distributions. Find the full list of supported platforms on the [Percona Software and Platform Lifecycle page](https://www.percona.com/services/policies/percona-software-support-lifecycle#pgsql).

Like many other Percona products, we recommend installing Percona Distribution for PostgreSQL from Percona repositories by using the **percona-release** utility. The **percona-release** utility automatically enables the required repository for you so you can easily install and update Percona Distribution for PostgreSQL packages and their dependencies through the package manager of your operating system.

## Package contents

In addition to individual packages for Percona Distribution for PostgreSQL components, it also includes two meta-packages: `percona-ppg-server` and `percona-ppg-server-ha`.

Using the meta-package, you can install all components it contains in one go.

### `percona-ppg-server`

The `percona-ppg-server` meta-package installs the PostgreSQL server with the following packages

| Package contents | Description                             |  
| ---------------- | --------------------------------------- | 
| `percona-postgresql%{pgmajorversion}-server` | The PostgreSQL server package. |
| `percona-postgresql-common` > 14.0 | PostgreSQL database-cluster manager. It provides a structure under which multiple versions of PostgreSQL may be installed and/or multiple clusters maintained at one time.|
| `percona-postgresql%{pgmajorversion}-contrib` | A collection of additional PostgreSQLcontrib extensions | 
| `percona-pg-stat-monitor%{pgmajorversion}` | A Query Performance Monitoring tool for PostgreSQL. | 
| `percona-pgaudit` > 14.0 | Provides detailed session or object audit logging via the standard PostgreSQL logging facility. | 
| `percona-pg_repack%{pgmajorversion}`| rebuilds PostgreSQL database objects.| 
| `percona-wal2json%{pgmajorversion}` | a PostgreSQL logical decoding JSON output plugin.|

The `%{pgmajorversion}` variable stands for the major version of PostgreSQL.

### `percona-ppg-server-ha`

The `percona-ppg-server-ha` meta-package installs high-availability components that are recommended by Percona.

| Package contents | Description                             |  
| ---------------- | --------------------------------------- | 
| `percona-patroni`| A high-availability solution for PostgreSQL. | 
| `percona-haproxy`| A high-availability and load-balancing solution |
| `etcd`           | A consistent, distributed key-value store | 
| `python3-python-etcd` | A Python client for ETCD.[^1]

## Procedure

### Install **percona-release**

[Install **percona-release**](https://www.percona.com/doc/percona-repo-config/installing.html) utility. If you have installed it before, [update](https://www.percona.com/doc/percona-repo-config/updating.html) it to the latest version.

### Enable the repository

Percona provides [two repositories](repo-overview.md) for Percona Distribution for PostgreSQL. We recommend enabling the Major release repository to timely receive the latest updates. 

To enable a repository, we recommend using the `setup` command: 

```
$ sudo percona-release setup ppg-15
```


### Install Percona Distribution for PostgreSQL packages

Install Percona Distribution for PostgreSQL using the commands of your package manager (the procedure differs
depending on the package manager of your operating system).

=== "On Debian and Ubuntu using `apt`"

     **NOTE**: Debian and other systems that use the `apt` package manager include the upstream PostgreSQL server package (postgresql-15) by default. The components of Percona Distribution for PostgreSQL 15 can only be installed together with the PostgreSQL server shipped by Percona (percona-postgresql-15). If you wish to use Percona Distribution for PostgreSQL, uninstall the PostgreSQL package provided by your distribution (postgresql-15) and then install the chosen components from Percona Distribution for PostgreSQL.

     Install the **percona-postgresql-15** package using **apt install**.

     ```
     $ sudo apt install percona-postgresql-15
     ```
     
=== "On Red Hat Enterprise Linux and derivatives using `yum`"

     **Platform Specific Notes**

     If you intend to install Percona Distribution for PostgreSQL on Red Hat Enterprise Linux v8, disable the ``postgresql``  and ``llvm-toolset``modules:


     ```
     $ sudo dnf module disable postgresql llvm-toolset
     ```


     On CentOS 7, you should install the ``epel-release`` package:


     ```
     $ sudo yum -y install epel-release
     $ sudo yum repolist
     ```

     Install the **percona-postgresql-15** package using **yum install**.

     ```
     $ sudo yum install percona-postgresql15-server
     ```

#### Install the Percona Distribution for PostgreSQL components

Note that this package will not install the components. Use the following commands to install components’ packages:

=== "On Debian and Ubuntu"

     Install `pg_repack`:

     ```
     $ sudo apt install percona-postgresql-15-repack
     ```

     Install `pgAudit`:

     ```
     $ sudo apt install percona-postgresql-15-pgaudit
     ```

     Install `pgBackRest`:

     ```
     $ sudo apt install percona-pgbackrest
     ```

     Install `Patroni`:

     ```
     $ sudo apt install percona-patroni
     ```

     [Install `pg_stat_monitor`](pg-stat-monitor.md)


     Install `pgBouncer`:

     ```
     $ sudo apt install percona-pgbouncer
     ```

     Install `pgAudit-set_user`:

     ```
     $ sudo apt install percona-pgaudit15-set-user
     ```

     Install `pgBadger`:

     ```
     $ sudo apt install percona-pgbadger
     ```

     Install `wal2json`:

     ```
     $ sudo apt install percona-postgresql-15-wal2json
     ```

     Install PostgreSQL contrib extensions:

     ```
     $ sudo apt install percona-postgresql-contrib
     ```

     Install HAProxy

     ```
     $ sudo apt install percona-haproxy
     ```

=== "On Red Hat Enterprise Linux and derivatives"

     Install `pg_repack`:

     ```
     $ sudo yum install percona-pg_repack15
     ```

     Install `pgaudit`:

     ```
     $ sudo yum install percona-pgaudit
     ```

     Install `pgBackRest`:

     ```
     $ sudo yum install percona-pgbackrest
     ```

     Install `Patroni`:

     ```
     $ sudo yum install percona-patroni
     ```

     [Install `pg_stat_monitor`](pg-stat-monitor.md):


     Install `pgBouncer`:

     ```
     $ sudo yum install percona-pgbouncer
     ```

     Install `pgAudit-set_user`:

     ```
     $ sudo yum install percona-pgaudit15_set_user
     ```

     Install `pgBadger`:

     ```
     $ sudo yum install percona-pgbadger
     ```

     Install `wal2json`:

     ```
     $ sudo yum install percona-wal2json15
     ```

     Install PostgreSQL contrib extensions:

     ```
     $ sudo yum install percona-postgresql15-contrib
     ```

     Install HAProxy
     
     ```
     $ sudo yum install percona-haproxy
     ```



Some extensions require additional setup in order to use them with Percona Distribution for PostgreSQL. For more information, refer to [Enabling extensions](#enabling-extensions).


### Starting the service

=== "On Debian and Ubuntu"
     
     The installation process automatically initializes and starts the default database. You can check the database status using the following command:

     ```
     $ sudo systemctl status postgresql.service
     ```

=== "On Red Hat Enterprise Linux and derivatives"

     After the installation, the default database storage is not automatically initialized. To complete the installation and start Percona Distribution for PostgreSQL, initialize the database using the following command:

     ```
     /usr/pgsql-15/bin/postgresql-15-setup initdb
     ```

     Start the PostgreSQL service:

     ```
     $ sudo systemctl start postgresql-15
     ```

Next steps: [connect to PostgreSQL](#connect-to-the-postgresql-server).


### Enabling extensions

Some extensions require additional configuration before using them with Percona Distribution for PostgreSQL. This sections provides configuration instructions per extension.

**Patroni**

Patroni is the third-party high availability solution for PostgreSQL. The [High Availability in PostgreSQL with Patroni](solutions/high-availability.md) chapter provides details about the solution overview and architecture deployment. 

While setting up a high availability PostgreSQL cluster with Patroni, you will need the following components:

- Patroni installed on every ``postresql`` node. 

- Distributed Configuration Store (DCS). Patroni supports such DCSs as ETCD, zookeeper, Kubernetes though [ETCD](https://etcd.io/) is the most popular one. It is available upstream as DEB packages for Debian 10, 11 and Ubuntu 18.04, 20.04, 22.04.  

     For CentOS 8, RPM packages for ETCD is available within Percona Distribution for PostreSQL.  You can install it using the following command: 

     ```sh
     $ sudo yum install etcd python3-python-etcd
     ```
  
- [HAProxy](http://www.haproxy.org/).

See the configuration guidelines for [Debian and Ubuntu](solutions/ha-setup-apt.md) and [RHEL and CentOS](solutions/ha-setup-yum.md). 


!!! admonition "See also"

    - [Patroni documentation](https://patroni.readthedocs.io/en/latest/SETTINGS.html#settings)

    - Percona Blog: 

        - [PostgreSQL HA with Patroni: Your Turn to Test Failure Scenarios](https://www.percona.com/blog/2021/06/11/postgresql-ha-with-patroni-your-turn-to-test-failure-scenarios/) 
        
**pgBadger**

Enable the following options in `postgresql.conf` configuration file before starting the service:

```
log_min_duration_statement = 0
log_line_prefix = '%t [%p]: '
log_checkpoints = on
log_connections = on
log_disconnections = on
log_lock_waits = on
log_temp_files = 0
log_autovacuum_min_duration = 0
log_error_verbosity = default
```

For details about each option, see [pdBadger documentation](https://github.com/darold/pgbadger/#POSTGRESQL-CONFIGURATION).

**pgAudit set-user**

Add the `set-user` to `shared_preload_libraries` in `postgresql.conf`. The recommended way is to use the [ALTER SYSTEM](https://www.postgresql.org/docs/14/sql-altersystem.html) command. [Connect to psql](#connect-to-the-postgresql-server) and use the following command:

```sql
ALTER SYSTEM SET shared_preload_libraries = 'set-user';
```

Start / restart the server to apply the configuration.

You can fine-tune user behavior with the [custom parameters](https://github.com/pgaudit/set_user#configuration-options) supplied with the extension.

**wal2json**

After the installation, enable the following option in `postgresql.conf` configuration file before starting the service:

```
wal_level = logical
```

### Connect to the PostgreSQL server

By default, `postgres` user and `postgres` database are created in PostgreSQL upon its installation and initialization. This allows you to connect to the database as the `postgres` user.

```
$ sudo su postgres
```

Open the PostgreSQL interactive terminal:

```
$ psql
```

!!! hint

    You can connect to `psql` as the `postgres` user in one go:

    ```
    $ sudo su postgres psql
    ```

To exit the `psql` terminal, use the following command:

```
$ \q
```


[^1]: Is included in repositories for RHEL 8 / CentOS 8 operating systems