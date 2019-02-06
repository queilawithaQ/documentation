---
title: Ubuntu Bionic
shortTitle: Ubuntu Bionic
menus:
  basic/builds:
    title: Ubuntu Bionic
    weight: 13
tags:
  - sudo
  - root
  - admin
  - apt-get
  - install
  - packages
  - ubuntu
  - trusty
  - bionic
categories:
  - Builds and Configuration
  - Configuration
---

* include a table of contents
{:toc}

## Ubuntu Bionic On CodeShip Basic

We are starting to test Ubuntu Bionic build containers for CodeShip Basic. If you are interested in running your builds on Ubuntu Bionic and helping us beta test, please [get in touch](https://helpdesk.codeship.com/hc/en-us/requests/new) and we can get you started.

In general, the overall environment is setup and configured in the same way you are familiar with. Most existing build commands should continue to work the same. The underlying OS version is just getting upgraded, specifically to **Ubuntu 18.04.1 LTS (Bionic Beaver)**.

If the build is running on Ubuntu Bionic, step 6 of the build will say `Preparing Bionic Build Container`.

### Common Issues

Many underlying package and dependency versions changed in Bionic so it is possible you will encounter issues depending on your build configuration. If you get unexpected errors the first step is to [clear your project's dependency cache]({{ site.baseurl }}{% link _basic/builds-and-configuration/dependency-cache.md %}#clearing-the-cache). You can also add the `cs clear-cache` command to the start of the build to ensure the cache is not used while you are testing the new environment.

If the build issues persist, then take a look at your build in a [debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) which allows you to look closer and experiment with other build commands. If you did any special customizations to make your builds run in the current environment, those customizations may need to either be updated for Bionic, or in some cases you may no longer need them.

### Support

If the above steps do not help to get your builds running, [reach out to us](https://helpdesk.codeship.com/hc/en-us/requests/new). We will help you get things running and your feedback will be helpful to us and other customers as we work on resolving issues in the new environment.
