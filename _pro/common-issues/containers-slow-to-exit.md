---
title: Container is Slow to Exit
shortTitle: Container is Slow to Exit after Completion of Command Step
menus:
  pro/common-issues:
    title: Container is Slow to Exit
    weight: 1
tags:
  - docker
  - container
  - slow
  - hangs
  - pro

categories:
  - Common Issues

---

For steps that appear to hang for a bit of time after the step's command has completed, consider investigating how the `CMD` and `ENTRYPOINT` instructions are provided to dependent containers.

At issue here is whether these instructions are provided in the 'exec' or 'shell' form (see [Stack Overflow post](https://stackoverflow.com/questions/42805750/dockerfile-cmd-shell-versus-exec-form) for explanation of forms).

If a container's instructions were provided in the shell form, a container may not exit gracefully upon completion of the step command and (as a result) would effectively hang until system timeouts take effect. Our recommendation is to use the exec form instead.

For an in depth discussion on why the shell form can be problematic, please check out [this blog post](https://www.ctl.io/developers/blog/post/gracefully-stopping-docker-containers/). We've also [prepared a demonstration of the differing behavior between shell and exec](https://github.com/codeship-library/shell-vs-exec-form). You can `git clone` the repository and run it on your local machine via `jet steps`.
