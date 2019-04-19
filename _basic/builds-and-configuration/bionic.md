---
title: Ubuntu Bionic
shortTitle: Ubuntu Bionic
menus:
  basic/builds:
    title: Ubuntu Bionic
    weight: 14
tags:
  - sudo
  - root
  - admin
  - apt-get
  - install
  - packages
  - ubuntu
  - bionic
categories:
  - Builds and Configuration
  - Configuration
---

* include a table of contents
{:toc}

## Ubuntu Bionic On CodeShip Basic

We are now running Ubuntu Bionic build containers for CodeShip Basic. In general, the overall environment is setup and configured in the same way you are familiar with. Most existing build commands should continue to work the same. The underlying OS version is now **Ubuntu 18.04.2 LTS (Bionic Beaver)**.

### Rollout Plan

On February 18th we started automatically opting in projects and running them on Bionic. At this time all projects are running on Bionic unless you manually opted a project out. All projects need to be migrated to Bionic by **April 15th**. If you are unable to migrate by **April 15th**, your projects will be manually changed over for you which may result in failing builds.

If the build is running on Bionic, step 6 of the build will say `Preparing Bionic Build Container`.

### Key Changes

* MySQL 5.7 running by default
* Python 3.7 installed by default
* PHP 5.3, 5.4 and 5.5 removed due to [end of life](http://php.net/supported-versions.php)

### Common Issues

Many underlying package and dependency versions changed in Bionic so it is possible you will encounter issues depending on your build configuration. If you get unexpected errors the first step is to [clear your project's dependency cache]({{ site.baseurl }}{% link _basic/builds-and-configuration/dependency-cache.md %}#clearing-the-cache). You can also add the `cs clear-cache` command to the start of the build to ensure the cache is not used while you are configuring the new environment.

If the build issues persist, then take a look at your build in a [debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) which allows you to look closer and experiment with other build commands. If you did any special customizations to make your projects run in the current environment, those customizations may need to either be updated for Bionic, or in some cases you may no longer need them.

Keep in mind that you have [root permissions]({{ site.baseurl }}{% link _basic/builds-and-configuration/root-level-access.md %}) in the build environment so you are free to use tools like `apt-get` to further customize the environment.

Finally, if you are using any [CodeShip scripts](https://github.com/codeship/scripts) they should work on Bionic, but if you encounter any problems let us know. Also consider that with newer versions of many packages in Bionic, you may not need a particular script any longer.

### Support

If the above steps do not help to get your projects running, [reach out to us](https://helpdesk.codeship.com/hc/en-us/requests/new). We will help you work through any migration challenges.
