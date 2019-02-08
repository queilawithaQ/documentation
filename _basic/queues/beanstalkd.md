---
title: Using Beanstalkd In CI/CD with Codeship Basic
shortTitle: Beanstalkd
tags:
  - services
  - queues
  - beanstalkd
menus:
  basic/queues:
    title: Beanstalkd
    weight: 2
categories:
  - Queues    
redirect_from:
  - /queues/beanstalkd/
  - /classic/getting-started/beanstalkd/
---

* include a table of contents
{:toc}

[Beanstalkd](https://beanstalkd.github.io) `1.9` can be installed and started by adding the following commands to your _Setup Commands_:

```
sudo apt-get update
sudo apt-get install -y beanstalkd
```
