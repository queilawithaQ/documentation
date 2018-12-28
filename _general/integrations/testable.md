---
title: Using Testable And Codeship For Load Testing
shortTitle: Testable Load Testing
menus:
  general/integrations:
    title: Using Testable
    weight: 7
tags:
- jmeter
- gatling
- locust
- nodejs
- phantomjs
- slimerjs
- selenium
- webdriverio
- api testing
- load testing
- performance testing
- browser testing
- screenshots
- integrations
categories:
  - Integrations
---

* include a table of contents
{:toc}

## About Testable

[Testable](https://testable.io) is a distributed load testing platform. Define a test with a variety of open-source tools and let Testable handle the scale, reporting, and analytics. Define your tests with  JMeter, Gatling, Locust, Node.js, Webdriver.io, Selenium Java, Serenity BDD, PhantomJS, SlimerJS, record-and-replay, and HAR files.

Checkout the [Testable documentation](https://docs.testable.io) as a starting point or the instructions below on how to run load tests in your [Codeship](https://codeship.com) pipeline.

## Codeship Pro

### Setting Your API Key

You will need to add your Testable API key to your [environment variables]({{ site.baseurl }}{% link _pro/builds-and-configuration/environment-variables.md %}) that you include in your [codeship-services.yml file]({{ site.baseurl }}{% link _pro/builds-and-configuration/services.md %}). 

- `TESTABLE_KEY`

API Keys can be [found on Testable](https://a.testable.io/account/api-keys) after registering for an account.

### Running a load test

Your Docker container will need to include any required test artifacts like a Node.js script, JMeter test plan, Gatling files, etc. 

You will then add a step in your [codeship-steps.yml file]({{ site.baseurl }}{% link _pro/builds-and-configuration/steps.md %}) that downloads a Testable script for running a load test. That [script](https://raw.githubusercontent.com/testable/sample-scripts/master/testable-kpi-monitor.sh) runs the test on Testable, waits for it to finish, checks the success/failure status, prints the success rate and median response time, and downloads the raw results to a CSV file. You can also add this script to your repository and customize it as needed.

```yaml
- name: testable_load_test
  service: app
  command: >
    /bin/bash -c 'curl -sSL https://raw.githubusercontent.com/testable/sample-scripts/master/testable-kpi-monitor.sh > testable-kpi-monitor.sh
    && chmod +x testable-kpi-monitor.sh
    && ./testable-kpi-monitor.sh $(curl -sS
    -F "code=@/usr/src/app/test/test.js"
    -F "concurrent_users_per_region=5"
    -F "duration_mins=1"
    -F "rampup_mins=0"
    -F "conf_testrunners[0].regions=aws-us-east-1"
    -F "kpis[0].expr=Outcome[success] > 95%"
    -F "kpis[1].expr=Response Time[Median] < 300ms"
    -F "testcase_name=Api Test"
    https://api.testable.io/start?key=$TESTABLE_KEY)'
```

This will run a load test that simulates 5 concurrent users each running a Node.js script for 1 minute from a shared grid in AWS N. Virginia and check that the success rate is greater than 95% and that the median response time is less than 300ms.

Check Testable's [parameter documentation](https://docs.testable.io/api/simple.html) for a complete reference.

While the load test is running you can track the real-time results via the [Testable website](https://a.testable.io).

## Codeship Basic

### Setting Your API Key

You will need to add your Testable API key to your to your project's [environment variables]({{ site.baseurl }}{% link _basic/builds-and-configuration/set-environment-variables.md %}).

- `TESTABLE_KEY`

API Keys can be [found on Testable](https://a.testable.io/account/api-keys) after registering for an account.

### Adding Setup Commands

After adding the API Key you'll just need to add Setup and Test commands.

Add the following to your [project's setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}/#configuring-your-setup-commands) to install a script that executes tests on Testable, waits for the test to finish, checks the success/failure status, prints the success rate and median response time, and downloads the raw results to a CSV file. The commands to add are:

```bash
## install jq
sudo apt-get update && sudo apt-get install -y jq

## Download script
curl -sSL https://raw.githubusercontent.com/testable/sample-scripts/master/testable-kpi-monitor.sh > testable-kpi-monitor.sh

## Make it executable
chmod +x testable-kpi-monitor.sh
```

### Adding Test Commands

Add the following to your [project's test commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}/#configuring-your-test-commands) to run the load test.  Check Testable's [parameter documentation](https://docs.testable.io/api/simple.html) for a complete reference.  

The following example test command runs a load test that simulates 5 concurrent users each running a Node.js script for 1 minute from a shared grid in AWS N. Virginia and check that the success rate is greater than 95% and that the median response time is less than 300ms. It assumes that the base URL of the deployed environment is available in the $DEPLOYED_BASE_URL environment variable for [the Node.js test script to access](https://docs.testable.io/guides/scenario-params.html).

```bash
/bin/bash -c './testable-kpi-monitor.sh $(curl -sS -F "code=@test.js" -F "params[baseUrl]=${DEPLOYED_BASE_URL}" -F "concurrent_users_per_region=5" -F "duration_mins=1" -F "rampup_mins=0" -F "conf_testrunners[0].regions=aws-us-east-1" -F "kpis[0].expr=Outcome[success] > 95%" -F "kpis[1].expr=Response Time[Median] < 300ms" -F "testcase_name=Api Test" https://api.testable.io/start?key=${TESTABLE_KEY})'
```

Check the [documentation](https://docs.testable.io/api/simple.html) for similar examples with other tools like JMeter, Gatling, Locust, Node.js, Webdriver.io, Selenium Java, Serenity BDD, PhantomJS, and SlimerJS.
