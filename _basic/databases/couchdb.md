---
title: Using CouchDB In CI/CD with CodeShip Basic
shortTitle: CouchDB
tags:
  - services
  - databases
  - couchdb
  - db
menus:
  basic/db:
    title: CouchDB
    weight: 7
categories:
  - Databases    
---

* include a table of contents
{:toc}

[CouchDB](https://couchdb.apache.org) **3.0.0** runs by default on port 5984. The default user is `admin` and the default password is `password`.

You can verify it is running with the following command:

```shell
curl http://127.0.0.1:5984
```
