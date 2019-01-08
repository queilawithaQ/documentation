---
title: VM And Infrastructure Specifics
shortTitle: VM And Infrastructure
menus:
  general/about:
    title: VM & Infrastructure Specifics
    weight: 4
tags:
  - security
  - infrastructure
  - linux
  - firewall
  - virtual machine
  - build machine
categories:
  - About Codeship
  - Security 
redirect_from:
  - /security/vm-and-infrastructure/
---

* include a table of contents
{:toc}

## Build Machines

### Codeship Basic

Codeship Basic runs [Ubuntu 14.04 (Trusty Tahr)](https://help.ubuntu.com/14.04/serverguide/index.html) on all build machines. To virtualize the build machines [Linux Containers (LXC)](https://linuxcontainers.org) are used. All Basic build machines run on AWS us-east-1. Basic is multi tenant meaning there are many Linux Containers running on a single AWS instance at a time.

**Every build gets a new completely clean container.** Changes done to the filesystem during the build are stored on a temporary filesystem in memory so your code never touches a harddrive and is completely removed as soon as the build ends.

### Codeship Pro

All Codeship Pro builds run on dedicated, single tenant build machines, on individual AWS EC2 instances, in the us-east-1 region. On Pro, builds run on infrastructure equipped with version {{ site.data.docker.version }} of Docker.

The Codeship Pro build environment is configurable depending on plan and available in the following configurations:

* **Small**: 2 CPUs, 3.75gb RAM
* **Medium**: 4 CPUs, 7.5gb RAM
* **Big**: 8 CPUs, 15gb RAM
* **Huge**: 16 CPUs, 30gb RAM
* **Massive**: 32 CPUs, 60gb RAM

## Firewall
All incoming ports are rejected by default except port 22, which is open to allow [SSH debug sessions]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}). Outgoing port 25 (SMTP) is closed by default so Codeship can't be used for spamming.

## Disk Space
All builds on both Codeship Basic and Codeship Pro have 10gb of disk space allocation for the build environment.

## System Timeouts

On **Codeship Basic**, a build can run for up to 3 hours, although builds will time out if there is no log activity for 10 minutes.

On **Codeship Pro**, a build can run for up to 5 hours, although builds will time out if there is no log activity for 15 minutes.
