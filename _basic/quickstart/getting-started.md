---
title: Getting Started With Codeship Basic
menus:
  basic/quickstart:
    title: Getting Started
    weight: 1
tags:
  - getting started
  - codeship basic
categories:
  - Quickstart  
  - Guide
  - Configuration
redirect_from:
  - /basic/getting-started/getting-started/
---

* include a table of contents
{:toc}

## Introducing Codeship Basic

Codeship Basic makes it easy and simple to get a working CI/CD process running through an easy-to-configure web UI and turnkey deployments.

This article will walk you through setting up a Codeship Basic project. For a video introduction to Codeship Basic, you can view our [overview video](https://codeship.com/features/basic).

## Setting up Continuous Integration with Codeship

### Prerequisites

Codeship requires that you set up a Codeship Account and connect to a Source Content Management (SCM).
See [Setting Up A New Codeship Account Guide ]({{ site.baseurl }}{% link _general/account/new-user-signup.md %}) for more information.


### Setting up tests for your deployments

Setup commands are the commands you need to be able to run your tests and deployments. Examples of setup commands include fetching dependencies and seeding database.

To configure your setup commands:

1. Select Tests in the dashboard.

2. Click the dropdown arrow on the right to select the technology to prepopulate basic commands

3. Either enter a new setup command or select existing Setup command.

4. Either click _Save and go to dashboard_ or _Save Changes_.

![Setup Commands on Codeship Basic]({{ site.baseurl }}/images/basic-guide/setup-commands.png)

**Note** that Codeship provides a list of popular setup commands for many common languages in the dropdown, but you can enter in your own commands as needed.

### Configuring tests for your deployment

Next, you will enter in your test commands. These are all tests you want to have run in your CI/CD pipeline, and all deployments you configure will be contingent on these tests passing.

![Setup Commands on Codeship Basic]({{ site.baseurl }}/images/basic-guide/test-commands.png)

## Defining Your Deployment Pipeline with Codeship

Now that you've defined your setup and test commands, you'll want to define your deployment pipelines. Deployment pipelines run only when a build's setup and tests commands have completed successful _and_ only when the branch defined for the deployment is matched. We call them deployment pipelines rather than deployments because you can have different deployment destinations - perhaps staging and master environments - triggered by different branches.

To configure your deployment pipelines:

1. Select _Deploy_ in the dashboard. 

2. Select either _Branch is exactly_ to match a specific branch or select _Branch starts with_ to match any branch that starts with a specific string.

3. Enter branch name with the drop down window.

4. Click the _Save Pipeline Settings_ button.

See [deployment pipeline]({{ site.baseurl }}{% link _basic/builds-and-configuration/deployment-pipelines.md %}) for more information.

![Add New Deployment Pipeline on Codeship Basic]({{ site.baseurl }}/images/basic-guide/add-new-deployment.png)

### Using preconfigured deployments to deploy to cloud services 

After specifying which branch triggers your new deployment pipeline, you can choose to use one of Codeship's turnkey deployment integrations or to use your own custom script deployment.

If you want to use one of Codeship's turnkey deployment integrations, just click on your host provider and provide the necessary account credentials as requested.

![Add New Deployment Pipeline on Codeship Basic]({{ site.baseurl }}/images/basic-guide/turnkey-deployments.png)

### Using your own custom deployment scripts to deploy to cloud services


If you don't want to use one of the turnkey deployment integrations, you can instead use your own custom script deployment. From the list of deployment targets, just select the last option - Custom Script.

![Custom Script Deployment on Codeship Basic]({{ site.baseurl }}/images/basic-guide/custom-script-deployment.png)

From there you will be presented with a command window, just like when you entered your setup and test commands, in which you can define what deployment scripts or commands you would like to run.

![Custom Script Deployment on Codeship Basic]({{ site.baseurl }}/images/basic-guide/custom-script-deployment-bash.png)

### Adding Multiple Deployment Steps

It's worth noting that for each deployment pipeline, you can add multiple deployments or multiple deployment steps. For instance, you can have one deployment on a `master` pipeline that runs your deployment scripts followed by another pipeline that runs notification scripts.

To add multiple steps or deployments to a pipeline, just click on an additional deployment target and specify as needed. You can then use the simple drag-and-drop interface to arrange the deployment commands in the order you need them to run in.

![Custom Script Deployment on Codeship Basic]({{ site.baseurl }}/images/basic-guide/multiple-deployments.png)

## Running a build

### Skipping a build

By using the string `--skip-ci` in your commit message, you can instruct Codeship not to run a build for a particular commit. You can learn more about this via our article on [skipping builds]({{ site.baseurl }}{% link _general/projects/skipping-builds.md %})

## Speeding up a build

### Using the cache to speed up a build

Codeship Basic has an automatic, built-in dependency cache, meaning we cache the packages directory for the most common dependency management systems, like NPM and Rubygems. You can clear your dependency cache at any time via the sidebar.

![Reset Dependency Cache]({{ site.baseurl }}/images/basic-guide/reset-dependency-cache.png)

### Creating parallel test tests to speed up a build 

Codeship offers the option to upgrade your Basic account with additional parallel test pipelines, allowing you to run multiple test commands simultaneously as a way to speed up your builds.

![Parallel test pipelines on Codeship Basic]({{ site.baseurl }}/images/basic-guide/two-pipelines.png)

You can sign up for a free ParallelCI trial from the sidebar or [get in touch with us](mailto:codeship-solutions@cloudbees.com) to discuss configuration options.

## Troubleshooting 

### Clearing the Cache

### Opening a SSH debug session

### Discrepancy between local machine runs and Codeship basic runs

### System Timeouts

If a command runs for longer than 10 minutes without printing any log output, the command and build will be automatically failed. Additionally, if a build runs for longer than 3 hours, it will be automatically failed.
## Additional Information 

### Accessing Codeship using the API

If you're looking to automate more of your processes, you can access your projects and builds via the Codeship API. See the [Codeship API Documentation]({{ site.baseurl }}{% link _general/integrations/api.md %}) for more details and examples.

### Scripts Library

We maintain a [scripts library](https://github.com/codeship/scripts) with scripts for common packages, deployments and other useful workflow improvements on Codeship Basic.

If you're looking for a specific tool or version, the scripts library is a great first place to check.



### Codeship Infrastructure

Codeship Basic builds run on fresh VMs provisioned on Ubuntu Trusty. You can learn more about our infrastructure setup [here]({{ site.baseurl }}{% link _general/about/vm-and-infrastructure.md %})

