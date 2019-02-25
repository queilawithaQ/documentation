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

We are starting to run Ubuntu Bionic build containers for CodeShip Basic. In general, the overall environment is setup and configured in the same way you are familiar with. Most existing build commands should continue to work the same. The underlying OS version is just getting upgraded, specifically to **Ubuntu 18.04.2 LTS (Bionic Beaver)**.

### Rollout Plan

Starting February 18th we will start automatically opting in projects and running them on Bionic. This will be a gradual rollout, meaning we will start with a very small number of projects and steadily increase over the next several weeks. Your projects might get opted in on the first day or it could happen at a later time.

If the build is running on Bionic, step 6 of the build will say `Preparing Bionic Build Container`.

If you would like your projects switched to Bionic sooner, please [let us know](https://helpdesk.codeship.com/hc/en-us/requests/new).

### Key Changes

* MySQL 5.7 running by default
* Python 3.7 installed by default
* PHP 5.3, 5.4 and 5.5 removed due to [end of life](http://php.net/supported-versions.php)

### Common Issues

Many underlying package and dependency versions changed in Bionic so it is possible you will encounter issues depending on your build configuration. If you get unexpected errors the first step is to [clear your project's dependency cache]({{ site.baseurl }}{% link _basic/builds-and-configuration/dependency-cache.md %}#clearing-the-cache). You can also add the `cs clear-cache` command to the start of the build to ensure the cache is not used while you are configuring the new environment.

If the build issues persist, then take a look at your build in a [debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) which allows you to look closer and experiment with other build commands. If you did any special customizations to make your projects run in the current environment, those customizations may need to either be updated for Bionic, or in some cases you may no longer need them.

Keep in mind that you have [root permissions]({{ site.baseurl }}{% link _basic/builds-and-configuration/root-level-access.md %}) in the build environment so you are free to use tools like `apt-get` to further customize the environment.

Finally, if you are using any [CodeShip scripts](https://github.com/codeship/scripts) they should work on Bionic, but if you encounter any problems let us know. Also consider that with newer versions of many packages in Bionic, you may not need a particular script any longer.

### Opting Out

If you have a project that is failing on Bionic and there is not a clear solution, you can opt that project out. Under _Project Settings > General_ is a button to switch back to the old environment.

### Support

If the above steps do not help to get your projects running, [reach out to us](https://helpdesk.codeship.com/hc/en-us/requests/new). We will help you work through any migration challenges. Your feedback is also helpful to us and other customers as we work on resolving issues in the new environment.
