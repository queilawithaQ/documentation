---
title: Support For Git LFS
shortTitle: Git LFS
menus:
  basic/builds:
    title: Git LFS
    weight: 13
tags:
  - git
  - lfs
categories:
  - Builds and Configuration
  - Configuration
---

* include a table of contents
{:toc}

[Git LFS](https://git-lfs.github.com) is not installed by default on CodeShip Basic, but can easily be added with [this script](https://github.com/codeship/scripts/blob/master/packages/git-lfs.sh).

For example if you want to install **2.7.0**, set that version as an [environment variable]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_:

```
export GIT_LFS_VERSION=2.7.0
```

Next, add [this command](https://github.com/codeship/scripts/blob/master/packages/git-lfs.sh#L6) to your _Setup Commands_ and the script will automatically be called at build time. Note, this script will automatically call `git lfs fetch` after installation.

```
\curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/packages/git-lfs.sh | bash -s
```
