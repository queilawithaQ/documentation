---
title: Step Log Not Appearing
shortTitle: Step Log Not Appearing
menus:
  pro/common-issues:
    title: Step Log Not Appearing
    weight: 6
tags:
  - docker
  - steps
  - log
  - pro

categories:
  - Common Issues
  - Command Steps

---

If the step's corresponding log is not appearing at all for the build, it is possible that you have run up against the 16mb step log limit. [Reducing the log output of dependent containers]({{ site.baseurl }}{% link _pro/common-issues/silencing-dependent-containers.md %}) is a good starting point for keeping under the log limit threshold.

If the logs must be viewed for this particular build, one additional workaround is to run the CodeShip Pro build from your local machine via `jet steps` (see our [Jet tool]({{ site.baseurl }}{% link _pro/jet-cli/installation.md %}) doc page for more information).

<br />
