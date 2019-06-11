---
title: Codeship Pro Image List
shortTitle: Codeship Pro Image List
description: Technical documentation listing all preinstalled Docker images of the Codeship Pro build environment
menus:
  pro/builds:
    title: Preinstalled Images
    weight: 12
tags:
- pro
- docker
- images
categories:
  - Builds and Configuration
---

{% csnote info %}
This page was last updated on 11/2/2018.
{% endcsnote %}

* include a table of contents
{:toc}

## Codeship Pro Preinstalled Images

The Codeship Pro build environment includes many common images from [Docker Hub](https://hub.docker.com) by default. In a best effort to list everything preinstalled on Codeship Pro, we offer the following list of installed images. While the list may not be fully complete at any given moment, we try our best to keep it comprehensive and up to date.

## Full List of Preinstalled Images

```
alpine:3.6
alpine:3.7
alpine:3.8

debian:jessie
debian:stretch

elasticsearch:2.4
elasticsearch:2.4-alpine
elasticsearch:5.6
elasticsearch:5.6-alpine

golang:1.10
golang:1.11

mdillon/postgis:9.4
mdillon/postgis:9.5
mdillon/postgis:9.6
mdillon/postgis:10
mdillon/postgis:11

mongo:3.4
mongo:3.6
mongo:4.0

mysql:5.6
mysql:5.7
mysql:8.0

postgres:9.4
postgres:9.4-alpine
postgres:9.5
postgres:9.5-alpine
postgres:9.6
postgres:9.6-alpine
postgres:10
postgres:10-alpine
postgres:11
postgres:11-alpine

redis:3.2
redis:4.0
redis:5.0

ruby:2.3
ruby:2.3-alpine
ruby:2.4
ruby:2.4-alpine
ruby:2.5
ruby:2.5-alpine

ubuntu:16.04
ubuntu:18.04
```
