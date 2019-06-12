---
title: Reducing Log Output from Dependent Containers
shortTitle: Reducing Log Output from Dependent Containers
menus:
  pro/common-issues:
    title: Reducing Log Output from Dependent Containers
    weight: 4
tags:
  - docker
  - pro
  - jet
  - logs

categories:
  - Common Issues

---

If the logs of the dependent containers are too verbose, a `commmand` instruction can be provided in the `codeship-services.yml` to add logging flags to suppress log output. 

{% csnote info %}
Command instructions to suppress log output will only work if the Docker image's entrypoint is configured to receive logging flags. We recommend that you read your dependent image's documentation for more information.
{% endcsnote %}

The following is a contrived example for suppressing the log output of both the `elasticsearch` and `mysql` service:

```yaml
# codeship-services.yml

app:
  image: busybox
  depends_on:
    - elasticsearch
    - mysql

elasticsearch:
  image: elasticsearch:2.4-alpine
  command: -Des.logger.level=ERROR

mysql:
  build:
    context: .
    dockerfile: Dockerfile.mysql
  cached: true
  command: --general-log=0 --log-error
```

<br />
