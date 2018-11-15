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

[RabbitMQ](https://www.rabbitmq.com) `3.2.4` runs with the default configuration on top of [Erlang](https://www.erlang.org) `17.4`.

The `rabbitmq_management` plugin is also enabled, which allows for changing various server related settings. Please look at the [plugin documentation](https://www.rabbitmq.com/management.html) for more information.

## Other Versions

If you need to install a different version or use a custom configuration, please see [this script](https://github.com/codeship/scripts/blob/master/packages/rabbitmq.sh).

For example if you want to install **3.7.8**, set that version as an [environment variable]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_. RabbitMQ requires Erlang as well so you should also configure the necessary Erlang version here:

```
export ERLANG_VERSION=21.1
export RABBITMQ_VERSION=3.7.8
```

Next, add [these commands](https://github.com/codeship/scripts/blob/master/packages/rabbitmq.sh#L6) to your _Setup Commands_ and the script will automatically be called at build time. Note, this script will automatically start the RabbitMQ service with its default configuration.

```
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/erlang.sh)"
\curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/packages/rabbitmq.sh | bash -s
```
