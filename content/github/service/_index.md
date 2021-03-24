---
title: "Amazon AWS App Runner Workshop - Deploying from Github"
chapter: true
weight: 15
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Setting up the AWS App Runner Service

Open the AWS console, and browse to the AWS App Runner service, or https://console.aws.amazon.com/fusion/home (https://console.aws.amazon.com/console/home):

![Create Service](/images/service-create-service.png)

Select “Create a service”.

![Source Service](/images/service-source.png)

For your Repository type, select “Source code repository”. This will require you to add a connection to Github in order for Fusion to deploy your new service. Select “Add new”.

![Github Link](/images/service-link-github1.png)

Give your connection name a suitable name - for example “fusion-example-connection”. Install a GitHub app with access to the repository you have just created by choosing the organization in which you created your new repository. Select your own account name.

![Github Link](/images/service-link-github2.png)

Confirm your password

![Github Link](/images/service-link-github3.png)

![Github Link](/images/service-link-github4.png)

Select the repository you created earlier within “Only select repositories”, and click “Save”. You’ll now be taken back to Step 1 within Fusion service creation.

![Github Link](/images/service-deployment1.png)


