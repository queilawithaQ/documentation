---
title: Using DynamoDB In CI/CD with CodeShip Basic
shortTitle: DynamoDB
tags:
  - services
  - databases
  - dynamodb
  - dynamo
  - db
menus:
  basic/db:
    title: DynamoDB
    weight: 8
categories:
  - Databases  
---

* include a table of contents
{:toc}

[Amazon DynamoDB](https://aws.amazon.com/dynamodb) is not installed on the build VMs by default, but it can be easily added with [this script](https://github.com/codeship/scripts/blob/master/packages/dynamodb.sh).

For example if you want to install the latest version on the default port of **8000**, add [this command](https://github.com/codeship/scripts/blob/master/packages/dynamodb.sh#L6) to your _Setup Commands_ and the script will automatically be called at build time.

```
\curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/packages/dynamodb.sh | bash -s
```
