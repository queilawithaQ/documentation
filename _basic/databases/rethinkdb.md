---
title: Using RethinkDB In CI/CD with CodeShip Basic
shortTitle: RethinkDB
tags:
  - services
  - databases
  - rethinkdb
  - db
menus:
  basic/db:
    title: RethinkDB
    weight: 6
redirect_from:
  - /databases/rethinkdb/
  - /classic/getting-started/rethinkdb/
categories:
  - Databases
---

* include a table of contents
{:toc}

[RethinkDB](https://www.rethinkdb.com) can be [installed](https://www.rethinkdb.com/docs/install/ubuntu) and run on Basic with the following steps:

```shell
source /etc/lsb-release && echo "deb http://download.rethinkdb.com/apt $DISTRIB_CODENAME main" | sudo tee /etc/apt/sources.list.d/rethinkdb.list
wget -qO- https://download.rethinkdb.com/apt/pubkey.gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get install -y rethinkdb
sudo cp /etc/rethinkdb/default.conf.sample /etc/rethinkdb/instances.d/instance1.conf
echo 'http-port=50836' | sudo tee --append /etc/rethinkdb/instances.d/instance1.conf
sudo service rethinkdb start
```
