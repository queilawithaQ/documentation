---
title: Using Apache Cassandra In CD/CD With CodeShip Basic
shortTitle: Apache Cassandra
tags:
  - services
  - databases
  - db
  - cassandra
menus:
  basic/db:
    title: Apache Cassandra
    weight: 5
categories:
  - Databases
redirect_from:
  - /databases/cassandra/
  - /classic/getting-started/cassandra/
---

* include a table of contents
{:toc}

[Apache Cassandra](https://cassandra.apache.org/) **2.1.21** is installed on the build VMs, but not running by default.

To use the service during your builds, start the service with the following command:

```shell
sudo /etc/init.d/cassandra start
```

If you require a CLI tool to access the Cassandra server, try [cqlsh](https://pypi.python.org/pypi/cqlsh) available via pip.

```shell
pip install cqlsh
cqlsh --cqlversion="3.2.1"
```
