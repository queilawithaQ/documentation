---
title: Differing Results between Jet CLI and CodeShip Pro
shortTitle: Differing Results between Jet CLI and CodeShip Pro
menus:
  pro/common-issues:
    title: Differing Results with Jet CLI
    weight: 3
tags:
  - docker
  - pro
  - jet

categories:
  - Common Issues

---

Running a build on your local machine with the [Jet CLI tool]({{ site.baseurl }}{% link _pro/jet-cli/installation.md %}) may have differing results from a build on CodeShip Pro. Let's explore why this might be the case.

### Jet CLI Disjoints

- Jet tool can be out of date (and therefore out of alignment with CodeShip Pro environment).
  > Run `jet update` to ensure latest version of CLI tool.

- Jet may be reliant on outdated Docker/service image(s).
  > Identify the current image with `docker image ls`, then remove via `docker rmi IMAGE_ID` (you can also `docker rmi` the image name directly if you have an `image` attribute set in the services file). Running `jet steps` will now trigger an image rebuild.

- `jet steps` could run with additional files present that would otherwise not be expected in the CodeShip Pro build.
  > We recommend running `jet steps` on a freshly git cloned version of your project OR running a `git reset` and `git clean` operation on your project prior to `jet steps`.

- Jet will overlook volume mappings to absolute paths on the host.
  > This may work just fine on one's local machine, but can be problematic with an ephemeral Docker Host (i.e., the CodeShip Pro build). Please ensure that volumes are mapped relative to the project folder on the Docker Host.

- Unless explicitly passed along to `jet steps` as a flag, most [CI environment variables]({{ site.baseurl }}{% link _pro/builds-and-configuration/environment-variables.md %}) will not be present in a `jet steps` build.
  > See `jet steps --help` for flag options.

- Outdated Docker Engine version
  > Ensure that your local machine is utilizing an [up-to-date version of Docker Engine](https://docs.docker.com/release-notes/). CodeShip Pro currently runs with {{ site.data.docker.version }}

- AES key may have been recently reset from CodeShip project page, preventing decryption of environment variables with the outdated AES key on local machine.
  > The AES key for your project can be located on the `Project Settings > General` page.

### CodeShip Pro Disjoints

- Application level resource constraints may be imposed on CodeShip Pro builds. Usually resulting in an explicit "out of memory" error in the stack trace.
  > Consult your library's documentation on increasing the memory allocation limit (e.g., [Composer](https://getcomposer.org/doc/articles/troubleshooting.md#memory-limit-errors), [Node.js](https://stackoverflow.com/questions/38558989/node-js-heap-out-of-memory)) and [Java](https://stackoverflow.com/a/14763095/9041368)).

- CodeShip Pro may be reliant on outdated Docker image(s).
  > To clear the project's Docker image cache, click the drop down arrow of any build status icon and select 'Reset Cache'.

- Resource constraints for the allotted CodeShip Pro instance size could force background processes to be killed on CodeShip Pro builds, while the same build runs without issue via `jet steps`. The error stack trace can be a bit more cryptic than with resource constraints imposed on the application level.
  > If you suspect your build is failing on account of resource constraints, then please [reach out to our support team](https://helpdesk.codeship.com/hc/en-us/requests/new) with the CodeShip Pro build url in question.

<br />
