# Feasibility study

## Databases

Since we create a design before developing here, therefore, we need to consider a relational database to store all data.

Because it implies the following:

- we know all domains properties and dependencies;
- the domains will not be expended or the expending will not require irreversible changes;
- we need to have [database normalization](https://en.wikipedia.org/wiki/Database_normalization) with automatic
  integrity control.

The final solution has to:

- organize clustering out of the box;
- have transactions;
- do not break the data in case of a crash;
- be fault tolerant;
- support Linux OS.

Using [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem) we
need [Consistency](https://en.wikipedia.org/wiki/Consistency_model)
and [Partition tolerance](https://en.wikipedia.org/wiki/Network_partition).

### List databases that will be compared

Since we design the project without funds we need only open source solutions here.

- [MySQL](https://en.wikipedia.org/wiki/MySQL)
- [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL)
- [SQLite](https://en.wikipedia.org/wiki/SQLite)
- [MariaDB](https://en.wikipedia.org/wiki/MariaDB)

List of criteria:

- clustering support;
- have transactions;
- can provide normalization of data;
- has triggers for automation;
- has high fault tolerant

**MySQL / MariaDB**

The group of databases supports clustering but open source solutions are unstable. And we don't review proprietary
solutions. Therefore, they do not have this ability.

The databases have transaction.

Their functionality provides all necessary things to provide normalization of data.

And the solutions work with different triggers.

The weak side of the databases is fault tolerant.
You can face data structure violation.
And you will need to restore data after fault.

**PostgreSQL**

The group of databases supports clustering but open source solutions are unstable. And we don't review proprietary
solutions. Therefore, they do not have this ability.

The databases have transaction.

Their functionality provides all necessary things to provide normalization of data.

And the solutions work with different triggers.

**SQLite**

SQLite is very simple database that can't work as cluster solution from box but there is cluster SQLite solution that
names as DQLite.

How MySQL provides SQLite does transactions as well, has all necessary for data normalisation and can do transaction.

**Summary table**

| Databases       | Clustering | Transactions | Normalization | Triggers | Fault tolerant |
|-----------------|------------|--------------|---------------|----------|----------------|
| MySQL / MariaDB | 10         | 9            | 10            | 10       | 6              |
| PostgreSQL      | 10         | 10           | 10            | 10       | 10             |
| SQLite          | 10         | 7            | 8             | 10       | 4              |

The best solution for the project is PostgreSQL because it scored max points. 
