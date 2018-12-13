---
title: Integrating Codeship With Gosec for Go Security Analysis
shortTitle: Using Gosec For Go Security Analysis
description: Technical documentation for the how to integrate Codeship with Gosec to automatically run a security analysis for Go code
tags:
  - go
  - security
menus:
  general/integrations:
    title: Using Gosec
    weight: 26
categories:
  - Integrations
---

* include a table of contents
{:toc}

## About Gosec

Gosec exists to help spot problems right in your Go source code, such as hard coded passwords, personal access tokens,  insecure random number seeds and more.

[Their documentation](https://github.com/securego/gosec) does a great job of providing more information, in addition to the setup instructions below.

## CodeShip Basic

## Project Configuration

To use Gosec with your CodeShip Basic project, you'll need to build Go in your project's [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}). You can do this by selecting Go from the list of languages, or including a command similar to the below in your instructions:

```
export GO_VERSION="1.8.1"
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/go.sh)"
go get -t -v ./...
go build -v
```

From there, simply install Gosec and [specify the rules you need](https://github.com/securego/gosec) via your project's [test or deployment commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}), as seen below:

```
curl -sfL https://raw.githubusercontent.com/securego/gosec/master/install.sh | sh -s -- -b $GOPATH/bin latest
gosec ${HOME}/src/github.com/michaelneale/mikerowecode.com
```

**Note** that this example uses a repo provided by a CloudBees team member, but you can develop your own repo for long-term use.

## CodeShip Pro

To use Gosec with your CodeShip Pro project, you'll need to have Go accessible either via an image you're using or a Dockerfile you're building in your [codeship-services.yml file]({{ site.baseurl }}{% link _pro/builds-and-configuration/services.md %}).

An example set of instructions to customize and include in your Dockerfile is below, if you're not already including Go:

```
RUN export GO_VERSION="1.8.1"
RUN source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/go.sh)"
RUN go get -t -v ./...
RUN go build -v
```

From there, simply install Gosec and [specify the rules you need](https://github.com/securego/gosec) via a script you call in your project's [codeship-steps.yml file]({{ site.baseurl }}{% link _pro/builds-and-configuration/steps.md %}).

For instance, you can take the below code and store it as a script in your repository as `gosec.sh`:

```
curl -sfL https://raw.githubusercontent.com/securego/gosec/master/install.sh | sh -s -- -b $GOPATH/bin latest
gosec ${HOME}/src/github.com/michaelneale/mikerowecode.com
```

**Note** that this example uses a repo provided by a CloudBees team member, but you can develop your own repo for long-term use.

Next, you can call this script as a step via your [codeship-steps.yml file]({{ site.baseurl }}{% link _pro/builds-and-configuration/steps.md %}):

```yaml
- name: gosec
  service: app
  command: gosec.sh
```
