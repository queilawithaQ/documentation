[CodeShip](http://addons.heroku.com/codeship) is an easy to use hosted [continuous integration and delivery](https://en.wikipedia.org/wiki/Continuous_delivery) service provided by [CloudBees](https://www.cloudbees.com).

CodeShip automated the CI/CD process, letting you specify test and deployment commands that will run on all Git commits and PRs inside your GitHub, GitLab or Bitbucket repos.

CodeShip offers two products:

- [CodeShip Basic](https://codeship.com/features/basic), focused on simplicity and quick setup
- [CodeShip Pro](https://codeship.com/features/pro), focused on Docker and advanced configurations

## Installing the add-on

The free CodeShip add-on can be installed to a Heroku application via the CLI by running the following command:

```shell
$ heroku addons:add codeship:free
-----> Adding codeship to sharp-mountain-4005... done, v18 (free)
```

<div class="callout">
A list of all plans available can be found
<a href="https://elements.heroku.com/addons/codeship#pricing">here</a>.
</div>

Once installed, you can open CodeShip by running:

```shell
$ heroku addons:open codeship
```

If you haven't already configured a project inside CodeShip, you will be taken to the new project screen. You can always access your CodeShip dashboard using the above command. Alternatively, you can sign in through GitHub/Bitbucket or with your email and password at [codeship.com](https://app.codeship.com/sessions/new).

## Configuration

When adding a new project, the first step is to choose your SCM provider.

![SCM Selection](https://documentation.codeship.com/images/new-user-setup/authenticate-scm.png)

From there, you'll select either CodeShip Basic or CodeShip Pro.

- If you're not using Docker, or you don't want to use configuration files to set up your CI/CD process, choose CodeShip Basic
- If you are using Docker, or want to configure your CI/CD with configuration files, choose CodeShip Pro

![Basic Or Pro](https://documentation.codeship.com/images/new-user-setup/select-infra.png)

Once you've selected which CodeShip product is right for you, we recommend [reading our setup guides](https://documentation.codeship.com/getting-started/) or [reviewing our code samples](https://documentation.codeship.com/pro/quickstart/quickstart-examples/#quickstart-example-repos) to get started configuring your projects.

## Removing the add-on

If you need to remove the add-on CodeShip can be removed via the CLI. **This will destroy all associated data and cannot be undone!**

Before removing the add-on please [reach out to us](mailto:support@codeship.com) and let us know what made you remove it so we can improve our service for future customers.

```shell
$ heroku addons:remove codeship
-----> Removing codeship from sharp-mountain-4005... done, v20
(free)
```

All your keys are named with the project name, so you can easily see which keys are in there from CodeShip.

```term
$ heroku keys
ssh-rsa AAAAB3FcbR.../uX8kI4rsL codeship/owner/name
```

## Support

Heroku provides support requests for all add-ons through [https://help.heroku.com](https://help.heroku.com/).
If you have any questions or need anything you can create a ticket there and they will let us know.

If you use our app the fastest way to contact us is through our [support system](https://helpdesk.codeship.com/hc/en-us/requests/new) or at [support@codeship.com](mailto:support@codeship.com).

## The CodeShip Blog

You should frequently look at our [blog](https://blog.codeship.com/?utm_source=heroku&utm_medium=link&utm_campaign=herokuadd-onprogram). Our crew works hard to bring you awesome content. A lot of interesting articles about using CodeShip with Heroku, automated testing, continuous integration and delivery can be found there.

Should you have any other questions, [just let us know](mailto:support@codeship.com)! And ***always keep shipping!***
