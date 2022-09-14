<!--
title: 'AWS Python Scheduled Cron example in Python'
description: 'This is an example of creating a function that runs as a cron job using the serverless ''schedule'' event.'
layout: Doc
framework: v3
platform: AWS
language: Python
priority: 2
authorLink: 'https://github.com/rupakg'
authorName: 'Rupak Ganguly'
authorAvatar: 'https://avatars0.githubusercontent.com/u/8188?v=4&s=140'
-->

# ESPN Fantasy Football Discord Bot; Serverless Deployment

This bot posts messages to Discord on behalf of an ESPN Fantasy Football League. It is deployed to AWS as Lambda functions which are invoked via CRON events, resulting in no cost to operate.

## Usage

### Setup

This project relies on Serverless to package and deploy, so import the relevant packages via

```
$ npm install
```

### Local Testing

Copy `example-config.yaml`, replace relevant values (from the [forked bot's instructions](../README.md)), and set `test=true`. When _any_ function is invoked, all relevant bot functions will be run and printed out to your terminal.

To execute a function, execute via CLI:

```
$ sls invoke local --function functionName
```

where `functionName` is a function from `serverless.yaml.functions`, such as `sundayScore`.

### Deployment

This example is made to work with the Serverless Framework dashboard, which includes advanced features such as CI/CD, monitoring, metrics, etc.

In order to deploy with dashboard, you need to first login with:

```
serverless login
```

and then perform deployment with:

```
serverless deploy
```

After running deploy, you should see output similar to:

```bash
Deploying aws-python-scheduled-cron-project to stage dev (us-east-1)

✔ Service deployed to stack aws-python-scheduled-cron-project-dev (205s)

functions:
  rateHandler: aws-python-scheduled-cron-project-dev-rateHandler (2.9 kB)
  cronHandler: aws-python-scheduled-cron-project-dev-cronHandler (2.9 kB)
```

There is no additional step required. Your defined schedules becomes active right away after deployment.

### Bundling dependencies

In case you would like to include 3rd party dependencies, you will need to use a plugin called `serverless-python-requirements`. You can set it up by running the following command:

```bash
serverless plugin install -n serverless-python-requirements
```

Running the above will automatically add `serverless-python-requirements` to `plugins` section in your `serverless.yml` file and add it as a `devDependency` to `package.json` file. The `package.json` file will be automatically created if it doesn't exist beforehand. Now you will be able to add your dependencies to `requirements.txt` file (`Pipfile` and `pyproject.toml` is also supported but requires additional configuration) and they will be automatically injected to Lambda package during build process. For more details about the plugin's configuration, please refer to [official documentation](https://github.com/UnitedIncome/serverless-python-requirements).
