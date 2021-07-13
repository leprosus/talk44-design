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

### List of databases that will be compared

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
- has high fault tolerant;
- can work with geo points.

**MySQL / MariaDB**

The group of databases supports clustering but open source solutions are unstable. And we don't review proprietary
solutions. Therefore, they do not have this ability.

The databases have transaction.

Their functionality provides all necessary things to provide normalization of data.

And the solutions work with different triggers.

The weak side of the databases is fault tolerant. You can face data structure violation. And you will need to restore
data after fault.

The database group doesn't work with geo data.

**PostgreSQL**

The group of databases supports clustering but open source solutions are unstable. And we don't review proprietary
solutions. Therefore, they do not have this ability.

The databases have transaction.

Their functionality provides all necessary things to provide normalization of data.

And the solutions work with different triggers.

PostgreSQL has several extensions that add ability to work with geo data.

**SQLite**

SQLite is very simple database that can't work as cluster solution from box but there is cluster SQLite solution that
names as DQLite.

How MySQL provides SQLite does transactions as well, has all necessary for data normalisation and can do transaction.

The database doesn't work with geo data.

**Summary table**

| Databases       | Clustering | Transactions | Normalization | Triggers | Fault tolerant | Geo points |
|-----------------|------------|--------------|---------------|----------|----------------|------------|
| MySQL / MariaDB | 10         | 9            | 10            | 10       | 6              | 0          |
| PostgreSQL      | 10         | 10           | 10            | 10       | 10             | 8          |
| SQLite          | 10         | 7            | 8             | 10       | 4              | 0          |

The best solution for the project is PostgreSQL because it scored max points.

## Message Queue

In order to organize distributed scalable software there is needed to have some data bus.

There isn't especial requirements for a message queue.

Main technical expectations:

- it can work with topics (it is necessary for separation queues);
- it can return a message back to a queue if a consumer was able to execute a task;
- can work as distributed solution;
- has simple API;
- can make snapshotting to a hard disk.

Using [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem) we
need [Consistency](https://en.wikipedia.org/wiki/Consistency_model)
and [Partition tolerance](https://en.wikipedia.org/wiki/Network_partition) as with database.

### List of messages queues that will be compared

Since we design the project without funds we need only open source solutions here.

- [RabbitMQ](https://en.wikipedia.org/wiki/RabbitMQ)
- [NATS](https://en.wikipedia.org/wiki/NATS_Messaging)
- [Kafka](https://ru.wikipedia.org/wiki/Apache_Kafka)

List of criteria:

- distributed solution;
- simple API;
- can make snapshotting;
- high performance.

**RabbitMQ**

One of the most popular solutions. It can work as distributed system, has persistent disk storage and has sufficient
performance. But it has very complex redundant interface.

**NATS**

It is pure golang solution. Can work as cluster. It can't work with persistent disk saving but has special version that
has all necessary features (the solution requires several dedicated servers or VPS).

NATS has average in complexity API.

Since NATS is an in-memory message queue it has extremely high performance.

**Kafka**

One of the most old solution as RabbitMQ.

And it has the same features as RebbitMQ has excepting API:
- can work as distributed system;
- has persistent disk storage;
- their performance is higher than RabbitMQ has but is lower that NATS has;
- has one of the simplest API.

**Summary table**

| Message Queue | Distributed | Simple API | Snapshotting | Performance |
|---------------|-------------|------------|--------------|-------------|
| RabbitMQ      | 10          | 5          | 10           | 7           |
| NATS          | 10          | 7          | 8            | 10          |
| Kafka         | 10          | 10         | 10           | 9           |

The best solution for the project is Kafka because it scored max points.
