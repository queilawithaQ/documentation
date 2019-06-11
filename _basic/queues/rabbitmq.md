---
title: Using RabbitMQ In CI/CD with Codeship Basic
shortTitle: RabbitMQ
tags:
  - services
  - queues
  - rabbitmq
menus:
  basic/queues:
    title: RabbitMQ
    weight: 2
categories:
  - Queues    
  - Configuration
redirect_from:
  - /queues/rabbitmq/
  - /classic/getting-started/rabbitmq/
---

* include a table of contents
{:toc}

[RabbitMQ](https://www.rabbitmq.com) `3.6.10` runs with the default configuration on top of [Erlang](https://www.erlang.org) `20.2.2`.

The `rabbitmq_management` plugin is also enabled, which allows for changing various server related settings. Please look at the [plugin documentation](https://www.rabbitmq.com/management.html) for more information.

## Other Versions

To install a different version or use a custom configuration, please see the following steps. The [RabbitMQ documentation](https://www.rabbitmq.com/install-debian.html) has additional details as well.

For example, to install the latest version of RabbitMQ running on the latest version of Erlang add the following to your _Setup Commands_:

```
sudo rabbitmqctl stop
sudo apt-get remove -y erlang rabbitmq-server
wget -O - "https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc" | sudo apt-key add -
echo "deb https://dl.bintray.com/rabbitmq-erlang/debian bionic erlang" | sudo tee /etc/apt/sources.list.d/bintray.erlang.list
echo "deb https://dl.bintray.com/rabbitmq/debian bionic main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
sudo apt-get update
sudo apt-get install -y erlang rabbitmq-server

# Add to confirm the service is running
sudo rabbitmqctl status
```
