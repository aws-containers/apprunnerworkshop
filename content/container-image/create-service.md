---
title: 'Create App Runner service'
chapter: true
weight: 24
---

# Create App Runner Service

Now it's time to create our App Runner service, we have already built our image and configured IAM
access.

Go to the [AWS App Runner console](https://console.aws.amazon.com/apprunner/home) and click
_Create an App Runner service_.

![Create Service](/images/service-create-service.png)

## Configure source and deployment

For _Repository type_, select _Container registry_, and for _Provider_, select _Amazon ECR_, as we
will be using the image we have previously built and pushed to our private ECR repository.

![Configure Service](/images/container-image/configure-source-deployment.png)

In the _Container image URI_ input, enter the full URI for our image, you can get it by typing the
following command in your terminal:

```shell
$ echo $ECR_REPOSITORY_URI:demo
1234567891012.dkr.ecr.eu-west-1.amazonaws.com/apprunnerworkshop-app:demo
```

In the _Deployment settings_ section, select _Automatic_ as the deployment trigger. And for ECR
access role, select the role name we've previously created

![Configure Deployment Settings](/images/container-image/configure-deployment-settings.png)

Then, click _Next_.

## Configure Service

On the next page, we will configure our service, first, select a name for your service, enter
`apprunnerworkshop-app`, and leave the rest with default values

![Configure Service](/images/container-image/configure-service.png)

n the _Security_ section, we are going to configure an _Instance role_ to use, this will allow
AWS App Runner to access the DynamoDB table we created in the pre-requisities section.

The value in the drop-down should match the output from the following command:

```shell
$ aws cloudformation describe-stacks --stack-name repostatus-gh-demo-infra --query 'Stacks[*].Outputs[?OutputKey==`RoleName`].OutputValue' --output text
repostatus-gh-demo-infra-Role-1T58V5WPCQH6S
```

![Configure Service](/images/container-image/configure-service-security.png)

Go ahead and click _Next_.

## Review & Deploy

Review our settings, and if everything looks good, click _Create & Deploy_. This step will take
a few minutes.

![Github Link](/images/container-image/service-deploying.png)

## Test the app

Once status has moved to “Complete", you can click on the url listed below "Default domain" in order
to view the actual web application you have just deployed. The app will fetch general repository
info from the GitHub API for a slug you provide,
browse to `https://[DOMAIN_HERE]/repo/[YOUR_GITHUB_USERNAME]/repostatus-gh-demo`.

Congratulations, you have just deployed our demo application from a built container image using
App Runner!
