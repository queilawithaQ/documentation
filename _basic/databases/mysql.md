---
title: Using MySQL In CI/CD with CodeShip Basic
shortTitle: MySQL
tags:
  - services
  - databases
  - mysql
  - db
menus:
  basic/db:
    title: MySQL
    weight: 1
redirect_from:
  - /databases/mysql/
  - /classic/getting-started/mysql/
categories:
  - Databases  
---

* include a table of contents
{:toc}

MySQL **5.7** runs on the default port and the credentials are stored in the `MYSQL_USER` and `MYSQL_PASSWORD` environment variables.

A **development** and **test** database are setup by default for you in addition to the system databases.

## Ruby on Rails

We replace the values in your `config/database.yml` automatically.

If you have your Rails application in a subdirectory or want to change
it from our default values you can add the following to a codeship.database.yml
(or any other filename) in your repository:

```yaml
development:
  adapter: mysql2
  host: localhost
  encoding: utf8
  pool: 10
  username: <%= ENV['MYSQL_USER'] %>
  password: <%= ENV['MYSQL_PASSWORD'] %>
  database: development<%= ENV['TEST_ENV_NUMBER'] %>
  socket: /var/run/mysqld/mysqld.sock
test:
  adapter: mysql2
  host: localhost
  encoding: utf8
  pool: 10
  username: <%= ENV['MYSQL_USER'] %>
  password: <%= ENV['MYSQL_PASSWORD'] %>
  database: test<%= ENV['TEST_ENV_NUMBER'] %>
  socket: /var/run/mysqld/mysqld.sock
```

Then in your setup commands run

```shell
cp codeship.database.yml YOUR_DATABASE_YAML_PATH
```

to copy the file wherever you need it.

If you don't use Rails and load `database.yml` yourself you might see an error like the following instead of the value of the environment variable:

```
MYSQL2::Error: Access denied for user '<%= ENV['MYSQL_USER'] %>'@'localhost'
```

This is because the `database.yml` example includes ERB syntax. You need to load `database.yml` and run it through ERB before you can use it:

```ruby
require "erb"
require "yaml"

DATABASE_CONFIG = YAML.load(ERB.new(File.read("config/database.yml")).result)
```

## Django

```python
DATABASES = {
  'default': {
    'ENGINE': 'django.db.backends.mysql',
    'NAME': 'test',
    'USER': os.environ.get('MYSQL_USER'),
    'PASSWORD': os.environ.get('MYSQL_PASSWORD'),
    'HOST': '127.0.0.1',
  }
}
```

## Other Versions

If you need to install [MySQL 8.0](https://dev.mysql.com/doc/relnotes/mysql/8.0/en), please see [this script](https://github.com/codeship/scripts/blob/master/packages/mysql-8.0.sh).

To configure a specific version or port number, set them as [environment variables]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}) in your project or add this in the _Setup Commands_:

```
export MYSQL_VERSION=8.0.17
export MYSQL_PORT=3308
```

Next add [this command](https://github.com/codeship/scripts/blob/master/packages/mysql-8.0.sh#L6) to your _Setup Commands_ and the script will automatically be called at build time. Note, this script automatically starts MySQL, but does not automatically setup any databases. You can run additional MySQL commands as needed to configure your databases.

For example, you can call `mysql` as follows:

```
"$HOME/mysql-8.0.17/bin/mysql" --defaults-file="$HOME/mysql-8.0.17/my.cnf" --version
```
