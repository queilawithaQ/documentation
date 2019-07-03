---
title: Setting an SSH Private Key
shortTitle: Setting an SSH Private Key
menus:
  pro/builds:
    title: Setting an SSH Private Key
    weight: 11
tags:
  - ssh
  - private
  - key
  - rsa
  - clone
  - git
  - ftp
  - sftp
  - deployment
  - rsync
  - encryption

categories:
  - Builds and Configuration

redirect_from:
  - /docker/ssh-key-authentication/
  - /pro/getting-started/ssh-key-authentication/
---

{% csnote info %}
This task requires the following:
- Local machine install of our [CLI tool]({{ site.baseurl }}{% link _pro/jet-cli/usage-overview.md %})
{% endcsnote %}

Many operations require the configuration of an SSH private key within your container(s) (e.g, git clone, rsync, ssh, etc).

While the task _seems_ as simple as copying a private key right into your Docker image, this is considered [highly inadvisable](https://medium.com/@mccode/dont-embed-configuration-or-secrets-in-docker-images-7b2e0f916fdd).

{% csnote warning %}
If you must have the private SSH key available during the image build (e.g., pulling dependencies) then please remove the private key before the end of the Dockerfile instruction (see the 'SSH Key Option' on [this page]({{ site.baseurl }}{% link _pro/builds-and-configuration/cloning-repos.md %}) before continuing with the information below).
{% endcsnote %}

---
<br>

**The suggested practice is to:**

#### 1. Generate & Store SSH Private Key to the Designated Encrypted Env Vars File

Run the following set of commands in the root of your project folder:

```
# Generate codeship_deploy_key and codeship_deploy_key.pub, configured to not require passphrase
docker run -it --rm -v $(pwd):/keys/ codeship/ssh-helper generate "<YOUR_EMAIL>" && \

# Store codeship_deploy_key as a one line entry in codeship.env file under `PRIVATE_SSH_KEY`
docker run -it --rm -v $(pwd):/keys/ codeship/ssh-helper prepare && \

# Remove original private key file
rm codeship_deploy_key && \

# Encrypt file
jet encrypt codeship.env codeship.env.encrypted && \

# Ensure that `.gitignore` includes all sensitive files/directories
docker run -it --rm -v $(pwd):/app -w /app ubuntu:16.04 \
/bin/bash -c 'echo -e "codeship.aes\ncodeship_deploy_key\ncodeship_deploy_key.pub\ncodeship.env\n.ssh" >> .gitignore'
```

{% csnote info %}
Check out the [README page](https://github.com/codeship-library/docker-utilities/tree/master/ssh-helper) for more information on our SSH Helper tool.
{% endcsnote %}

#### 2. Configure your CodeShip config files with the following as guidance

```
# Dockerfile

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y ssh
```

```
# codeship-services.yml

app:
  build:
    image: codeship/setting-ssh-key-test
    dockerfile: Dockerfile
  encrypted_env_file:
    - codeship.env.encrypted
  volumes:
  # mapping to `.ssh` directory ensures that `id_rsa` file persists to subsequent steps
  # replace container pathing if $HOME is not `/root`
    - ./.ssh:/root/.ssh
```

```
# codeship-steps.yml

- name: reinstate SSH Private Key File
  service: app
  command: /bin/bash -c "echo -e $PRIVATE_SSH_KEY >> /root/.ssh/id_rsa"

- name: chmod id_rsa
  service: app
  command: chmod 600 /root/.ssh/id_rsa

- name: add server to list of known hosts
  service: app
  command: /bin/bash -c "ssh-keyscan -H github.com >> /root/.ssh/known_hosts"

# https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
- name: confirm ssh connection to server, authenticating with generated public ssh key
  service: app
  command: /bin/bash -c "ssh -T git@github.com 2>&1 | grep 'successfully authenticated'"
```

{% csnote info %}
If you're unfamiliar with CodeShip Pro, then check out our step-by-step walk-through on [setting up a private SSH key](https://github.com/codeship-library/setting-ssh-private-key-in-pro).
{% endcsnote %}

<br>
