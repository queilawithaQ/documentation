---
title: Using Elixir In CI/CD with Codeship Basic
shortTitle: Elixir
tags:
  - elixir
  - erlang
  - languages
menus:
  basic/languages:
    title: Elixir
    weight: 5
categories:
  - Languages And Frameworks    
---

* include a table of contents
{:toc}

## Versions And Setup

[Elixir](https://elixir-lang.org) is not installed on the build VMs by default, but it can be easily added with [this script](https://github.com/codeship/scripts/blob/master/languages/elixir.sh).

For example if you want to install **1.8.1**, set that version as an [environment variable]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_. Elixir requires Erlang as well so you should also configure the necessary Erlang version here:

```
export ERLANG_VERSION=21.2
export ELIXIR_VERSION=1.8.1
```

Next, add [these commands](https://github.com/codeship/scripts/blob/master/languages/elixir.sh#L12) to your _Setup Commands_ and the scripts will automatically be called at build time.

```shell
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/erlang.sh)"
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/elixir.sh)"
```

## Dependencies

Installing dependencies via hex is supported once Elixir has been installed, as per the instructions above.

### Dependency Cache

We do not cache Elixir dependencies between builds.

## Frameworks And Testing

Elixir frameworks such as Phoenix, and test tools such as ExUnit, are all supported on Codeship. Note that you will need to manually install all tools needed, in your project's [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}).

## Parallel Testing

If you are running [parallel test pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), you will want separate your tests into groups and call a group specifically in each pipeline. For instance:

**Pipeline 1:**
```shell
mix test tests/tests_1.exs
```

**Pipeline 2:**
```shell
mix test tests/tests_2.exs
```

### Parallelization Modules

In addition to parallelizing your tests explicitly [via parallel pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), some customers have found using ExUnit's built-in test parallelization is a good way to speed up your tests.

Note that aggressive parallelization can cause resource and build failure issues, as well.

## Notes And Known Issues

Due to Elixir version and build issues, you may find it helpful to tests your commands with different versions via an [SSH debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) if tests are running differently on Codeship compared to your local machine.
