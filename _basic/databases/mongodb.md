---
title: Using MongoDB In CI/CD with Codeship Basic
shortTitle: MongoDB
tags:
  - services
  - databases
  - mongodb
  - mongo
  - db
menus:
  basic/db:
    title: MongoDB
    weight: 3
redirect_from:
  - /databases/mongodb/
  - /classic/getting-started/mongodb/
categories:
  - Databases  
---

* include a table of contents
{:toc}

[MongoDB](https://www.mongodb.com) `3.6.3` runs on the default port **27017** and doesn't require any credentials.

## Other Versions

If you need to install a different version or use a custom configuration, please see [this script](https://github.com/codeship/scripts/blob/master/packages/mongodb.sh). This script supports [MongoDB 3.0.0 and above](https://docs.mongodb.com/manual/release-notes).

For example if you want to install **4.0.6**, set that version and port number as [environment variables]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_:

```
export MONGODB_VERSION=4.0.6
export MONGODB_PORT=27017
```

Next, add these commands to shutdown the default MongoDB instance and [install the new version](https://github.com/codeship/scripts/blob/master/packages/mongodb.sh#L10).

```
sudo mongod --dbpath /var/lib/mongodb --shutdown

\curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/packages/mongodb.sh | bash -s
```
