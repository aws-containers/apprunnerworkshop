---
title: 'Configure build & deployment settings'
chapter: true
weight: 13
---


# Configure build settings

In this section, we will configure a few settings for your AWS App Runner service.

## Configure Deployment Settings

![Github Link](/images/intermediate/service-deployment1.png)

In the _Deployment Settings -> Deployment trigger_, select _"Automatic"_, so that AWS App Runner
automatically newly introduced code changes from your `main` branch as defined above.

Click next.

## Configure Build Settings

![Github Link](/images/intermediate/service-deployment2.png)

In this example, we are going to specify all the settings for our service manually. This is in order
to show the control that AWS App Runner gives you. Later we will demonstrate giving these settings
through a configuration file contained within your code repository.

Select “Configure all settings here”, then underneath Runtime select _“Python 3”_ from the dropdown.

Under Build commend, enter `pip install pipenv && pipenv install`.

Under Start command, enter `pipenv run flask run -h 0.0.0.0 -p 8080`.

Under Port, enter `8080`.

Select ‘Next’ to continue.

## Configure service

![Github Link](/images/intermediate/service-deployment3.png)

In this step we will give our new service a name - `apprunnerworkshop-app`.

![Configure Service Role](/images/intermediate/service-deployment-role.png)

In the _Security_ section, we are going to configure an _Instance role_ to use, this will allow
AWS App Runner to access the DynamoDB table we created in the pre-requisities section.

The value in the drop-down should match the output from the following command:

```shell
$ aws cloudformation describe-stacks --stack-name repostatus-gh-demo-infra --query 'Stacks[*].Outputs[?OutputKey==`RoleName`].OutputValue' --output text
repostatus-gh-demo-infra-Role-1T58V5WPCQH6S
```

Leave the rest of these settings as defaults. Select “Next” to continue.

![Github Link](/images/intermediate/service-deployment4.png)

Finally, review your settings and select “Create & deploy”. This will take a few minutes.

![Github Link](/images/intermediate/service-creating.png)

## Test the app

Once status has moved to “Complete", you can click on the url listed below "Default domain" in order
to view the actual web application you have just deployed. The app will fetch general repository
info from the GitHub API for a slug you provide,
browse to `https://[DOMAIN_HERE]/repo/[YOUR_GITHUB_USERNAME]/repostatus-gh-demo`.

Congratulations, you have just deployed a simple web service using App Runner!
