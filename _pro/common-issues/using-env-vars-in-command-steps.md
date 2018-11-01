---
title: Using Environment Variables in Command Steps
shortTitle: Using Environment Variables in Command Steps
menus:
  pro/common-issues:
    title: Using Env Vars in Command Steps
    weight: 2
tags:
  - docker
  - steps
  - environment variables
  - pro

categories:
  - Common Issues
  - Environment Variables
  - Command Steps

---

In order to interpolate [environment variables]({{ site.baseurl }}{% link _pro/builds-and-configuration/environment-variables.md %}) into `codeship-steps.yml` command steps, the entire step must be wrapped in a shell command.

For example, the command without a shell wrapper...

```yaml
- service: app
  command: echo The branch name is: $CI_BRANCH
```

...results in:

```
The branch name is: $CI_BRANCH
```

---
<br />

Whereas a command _with_ a shell wrapper...

```yaml
- service: app
  command: /bin/sh -c 'echo The branch name is: $CI_BRANCH'
```

...results in:

```
The branch name is: master
```
