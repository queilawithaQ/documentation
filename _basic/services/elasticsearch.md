---
title: Using Elasticsearch In CI/CD with Codeship Basic
shortTitle: Elasticsearch
tags:
  - services
  - elastic
  - elasticsearch
  - es
menus:
  basic/services:
    title: Elasticsearch
    weight: 1
redirect_from:
  - /services/elasticsearch/
  - /classic/getting-started/elasticsearch/
categories:
  - Services
---

* include a table of contents
{:toc}

[Elasticsearch](https://www.elastic.co) **6.6.1** is installed on the default port **9200** and doesn't require any credentials. However, it is not running by default. To use this version of Elasticsearch during your builds, start the service with this command:

```shell
sudo /etc/init.d/elasticsearch start
```

## Other Versions

If you need to install a different version or use a custom configuration, please see [this script](https://github.com/codeship/scripts/blob/master/packages/elasticsearch.sh).

For example if you want to install **6.7.0**, set that version and port number as [environment variables]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_:

```
export ELASTICSEARCH_VERSION=6.7.0
export ELASTICSEARCH_PORT=9200
```

Java 8 is set by default, but if the Elasticsearch version being used needs a specific [Java version]({{ site.baseurl }}{% link _basic/languages-frameworks/java-and-jvm-based-languages.md %}#versions-and-setup) be sure to set it in your _Setup Commands_. 

Finally add [this command](https://github.com/codeship/scripts/blob/master/packages/elasticsearch.sh#L6) to your _Setup Commands_ and the script will automatically be called at build time. Note, this script automatically starts the Elasticsearch service. Do not call the sudo command mentioned above, otherwise there will be two instances of Elasticsearch running in the build.

```
\curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/packages/elasticsearch.sh | bash -s
```
