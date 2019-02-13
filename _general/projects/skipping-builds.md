---
title: Skipping Individual Builds
menus:
  general/projects:
    title: Skipping Individual Builds
    weight: 3
tags:
  - docker
  - basic
  - pro
  - jet
  - git
  - builds
  - testing
  - skipping
  - skip
  - triggers
  - triggering
  - trigger
categories:
  - Projects
  - Testing
  - Configuration
redirect_from:
  - /docker/skipping-builds/
  - /pro/getting-started/skipping-builds/
  - /basic/getting-started/skipping-builds/
  - /continuous-integration/skipping-builds/
---

* include a table of contents
{:toc}

## Configuring Build Triggers

### Triggering Builds On Commits, Merges, And Tags

You can trigger a build when committing, merging, and pushing tags to your project.  This is the default behavior. See [working with tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) for more information on pushing tags.   


To trigger a build on commit, builds and tags:

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Build on commit, merge, and tags_ button.

4. Click Save Configuration.


### Triggering Builds Only On Pull Requests

You can trigger a build when opening, merging, and updating a Pull Requests (PR).

To trigger a build only on PRs:

1. Go to Project Settings.

2. Select the _Build Triggers_ tab.

3. Select the _Build only on PR events_ button.
![Build only on PRs]({{ site.baseurl }}/images/general/build_only_PR.png)
4. Click Save Configuration.

Note:
The following environment variables are populated after the _Build only on PR events_ configuration is saved:
PR_NUMBER is populated with the PR number.
CI_PULL_REQUEST is populated with the URL of the pull request. 

See link for more information on environment variables.

### Triggering Builds on Commits versus on Pull Requests

The following table shows when a build is triggered.
           

|                       	| Trigger a Build on Commit, Merge, Tags         |      | Trigger A Build On Pull Requests        	|
|-----------------------	|:----------------------------------------------:|:----:|:--------------------------------------------:	|
| Push a Commit                	|                       Yes                      |	|			No			|
| Push a Tag                  	|                       Yes                      |	|                      No                      	|
| Open a Pull Request   	|                       No                       |	|                      Yes                     	|
| Update a Pull Request 	|                       Yes                      |	|                      Yes                     	|
| Merge a Pull Request  	|                       Yes                      |	|                      Yes                     	|


## Configuring Branches

You can run builds for all branch, exclude branches from triggering builds, and run builds only for certain branches. 
The default behavior is to run builds for all branches.
 
### Excluding Branches From Triggering Builds

To exclude branches from triggering a build:

1. Go to Project Settings

2. Select the _Build Triggers_ tab

3. Select the _Don't run builds for these branches_ button

4. Enter either full branch names like "master" or a regular expressions like "^release.*$".
![Exclude branches from running builds]({{ site.baseurl }}/images/general/exclude_branches.png)
5. Click Save Configuration

### Running Builds Only For These Branches

To run builds only on certain branches: 

1. Go to Project Settings

2. Select the _Build Triggers_ tab

3. Select the _Run build for these branches only_ button

4. Enter either full branch names like "master" or a regular expressions like "^release.*$".

5. Click Save Configuration

## Skipping Individual Builds

You can skip builds on both [Codeship Basic](https://codeship.com/features/basic) and [Codeship Pro](https://codeship.com/features/pro) by using a special commit directive.

### Skipping Builds Using The Commit Message

You can add either of the following skip directives to the commit message of the last commit before you push and that push will be ignored:

* `--skip-ci`
* `--ci-skip`
* `[skip ci]`
* `[ci skip]`

Skipped builds do not have a build record and will not show up in the Codeship UI. They will also not count towards the concurrent builds or monthly build limits for users.


### Skipping Builds Using A Step Tag on Pro

On [Codeship Pro](https://codeship.com/features/pro), in addition to using a commit message, you can also de-facto skip builds by making sure that every step in your `codeship-steps.yml` file has a `tag`, which limits that step to a certain branch. You can learn more about limiting your steps to a certain branch [codeship-steps.yml documentation]({{ site.baseurl }}{% link _pro/builds-and-configuration/steps.md %}).
