[CodeShip](http://addons.heroku.com/codeship) is an easy to use hosted [continuous integration and delivery](http://en.wikipedia.org/wiki/Continuous_delivery) service provided by [CloudBees](https://www.cloudbees.com).

CodeShip automated the CI/CD process, letting you specify test and deployment commands that will run on all Git commits and PRs inside your Github, Gitlab or Bitbucket repos.

CodeShip offers two products:

- CodeShip Basic, focused on simplicity and quick Setup
- CodeShip Pro, focused on Docker and advanced configurations

## Installing the add-on

The free CodeShip add-on can be installed to a Heroku application via the CLI by running the following command:

```shell
$ heroku addons:add codeship:free
-----> Adding codeship to sharp-mountain-4005... done, v18 (free)
```

<div class="callout">
A list of all plans available can be found
<a href="http://addons.heroku.com/codeship">here</a>.
</div>

Once installed,y ou can open CodeShip by running:

```shell
$ heroku addons:open codeship
```

If you haven't already configured a project inside CodeShip, you will be taken to the new project screen. You can always access your Codeship dashboard using the above command. Alternatively, you can sign in through GitHub / BitBucket or with your email and password at [https://www.codeship.com](https://www.codeship.com).

## Configuration

When adding a new project, the first step is to choose your SCM provider.

![SCM Selection](https://documentation.codeship.com/images/new-user-setup/authenticate-scm.png)

From there, you'll select either CodeShip Basic or CodeShip Pro.

- If you're not using Docker, or you don't want to use configuration files to set up your CI/CD process, choose CodeShip Basic
- If you are using Docker, or want to configure your CI/CD with configuration files, choose CodeShip Pro

![Basic Or Pro](https://documentation.codeship.com/images/new-user-setup/select-infra.png)

Once you've selected which CodeShip product is right for you, we recommend [reading our setup guides](https://documentation.codeship.com/getting-started/) or [reviewing our code](https://documentation.codeship.com/getting-started/) samples to get started configuring your projects.

### Additional Settings

#### Backup

A backup through the standard Heroku [PostgreSQL backups](https://devcenter.heroku.com/articles/heroku-postgres-backups) will be done.

#### Force

Push via `git push --force` to Heroku to overwrite whatever was in the repository before. This is handy for deploying to your staging application as you may have pushed something to give it a try but haven't reverted. **You should never enable this for your production application**.

#### Migrate

Runs Rails migrations for your application.

#### Restore From

Copies the PostgreSQL database from another app into this applications database. For example you are pushing to staging and want to run the migrations with production data. You can restore the production db into your staging application to have it accessible for your migrations.

#### URL

The URL that will be called to check that a *HTTP/2xx* Status is returned. By default this will be `https://APP_NAME.herokuapp.com/`, but you can change that to anything you want. If you use *HTTP Basic Authentication*  add your credentials to the URL like  `https://USER:PASSWORD@APP_NAME.herokuapp.com`.

## Removing the add-on

If some strange outlandish circumstances should force you to remove the add-on (remember, you don't want to remove the add-on!) Codeship can be removed via the CLI. **This will destroy all associated data and cannot be undone!**

Before removing the add-on please have a little [chat with Marko](mailto:marko@codeship.com) from the Codeship crew and tell him what made you remove it so we can improve our service for future users.

```shell
$ heroku addons:remove codeship
-----> Removing codeship from sharp-mountain-4005... done, v20
(free)
```

All your keys are named with the project name, so you can easily see which keys are in there from Codeship.

```term
$ heroku keys
ssh-rsa AAAAB3FcbR.../uX8kI4rsL codeship/owner/name
```

## Support

Heroku provides support requests for all add-ons through [https://support.heroku.com](https://support.heroku.com).
If you have any questions or need anything you can create a ticket there and they will let us know.

If you use our app the best & fastest way to contact is via our in-app support system. Additionally you can also contact us via email at [support@codeship.com](mailto:support@codeship.com) or on [twitter.com/codeship](https://twitter.com/codeship).

## The Codeship Blog

You should frequently take a look at our blog on [blog.codeship.com](https://blog.codeship.com/?utm_source=heroku&utm_medium=link&utm_campaign=herokuadd-onprogram). Our crew works hard to bring you awesome content. A lot of interesting articles about using Codeship with Heroku, automated testing, continuous integration and delivery can be found there.

Should you have any other questions, [just let us know](mailto:support@codeship.com)! And ***always keep shipping!***
