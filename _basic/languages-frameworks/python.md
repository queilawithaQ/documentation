---
title: Using Python In CI/CD with CodeShip Basic
shortTitle: Python
menus:
  basic/languages:
    title: Python
    weight: 4
tags:
  - python
  - languages
  - flask
  - django
  - pyenv
  - pip
categories:
  - Languages And Frameworks
redirect_from:
  - /languages/python/
---

* include a table of contents
{:toc}

## Versions And Setup

We use [pyenv](https://github.com/pyenv/pyenv) to manage Python environments for you.

By default, Python `{{ site.data.basic.defaults.python }}` is set, but versions `2.7`, `3.4`, `3.5`, and `3.6` are preinstalled as well. These are aliases that are pointing to the specific versions installed.

The following Python versions are preinstalled:

{% include basic/ami/{{ site.data.basic.ami_id }}/python.md %}

### Specifying Version

You have several options to specify which Python version you would like to use.

In your [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}) you can use **pyenv** commands. For instance:

```shell
pyenv local $version
```

You can also use the environment variable `PYENV_VERSION` to choose from one of the installed Python versions.

Alternatively, you can specify a version to use by committing a file named `.python-version` into your code repository with a version specification.

To install a specific Python version that is not already preinstalled, add these commands:

```shell
pyenv install $version
pyenv local $version
```

## Dependencies

You can use **pip** to install any dependencies in your [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}).

For example:

```shell
pip install -r requirements.txt
```

### Dependency Cache

CodeShip automatically caches all dependencies installed through `pip`. You can [read this article to learn more]({{ site.baseurl }}{% link _basic/builds-and-configuration/dependency-cache.md %}) about the dependency cache and how to clear it.

## Frameworks And Testing

All Python frameworks, including Django, Flask and Pyramid, should work without issue.

All test frameworks and tools, including pytest and unittest, should also work without issue.

## Parallel Testing

If you are running [parallel test pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), you will want separate your tests into groups and call a group specifically in each pipeline. For instance:

**Pipeline 1**
```shell
py.test tests_1.py
```

**Pipeline 2**
```shell
py.test tests_2.py
```

### Parallelization Modules

In addition to parallelizing your tests explicitly [via parallel pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), you may find that there are packages available for parallelizing different types of testing, such as [nose-parallel](https://pypi.python.org/pypi/nose-parallel), to speed your tests up.

While we do not officially support or integrate with these modules, many CodeShip users find success speeding their tests up by using them. Note that it is possible for these modules to cause resource and build failure issues, as well.

## Notes And Known Issues

Due to Python version issues, you may find it helpful to tests your commands with different versions via an [SSH debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) if tests are running differently on CodeShip compared to your local machine.

### Executable Not Available

As we use **pyenv**, if an executable is not available after installation you may need to run the command `pyenv rehash` after installing the package. [You can read pyenv's documentation](https://github.com/pyenv/pyenv) for more information.

### Cannot Rehash

You may encounter a rehash error like this:

```
pyenv: cannot rehash: /home/rof/.pyenv/shims/.pyenv-shim exists
```

If this occurs try adding this command to the start of your _Setup Steps_:

```
rm -rf $HOME/.pyenv/plugins/pyenv-codeship-rehash
```
