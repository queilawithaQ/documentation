---
title: Managing Multiple Environments For a Service
shortTitle: Managing Multiple Environments For a Service
menus:
  pro/common-issues:
    title: Managing Multiple Environments For a Service
    weight: 7
tags:
  - docker
  - pro
  - service

categories:
  - Common Issues

---

For services that have multiple environments (e.g., production, staging, development) and require these contexts to be present within the CodeShip Pro build, our recommendation is to create a service for every environmental variant, reference the same Dockerfile in each service and provide the custom environment variables as needed:

```yaml
# codeship-services.yml

app-prod:
  build:
    dockerfile: Dockerfile.app
  encrypted_env_file:
    - shared_env_vars.encrypted
    - prod_env_vars.encrypted

app-staging:
  build:
    dockerfile: Dockerfile.app
  encrypted_env_file:
    - shared_env_vars.encrypted
    - staging_env_vars.encrypted

app-dev:
  build:
    dockerfile: Dockerfile.app
  encrypted_env_file:
    - shared_env_vars.encrypted
    - dev_env_vars.encrypted
```

<br />
