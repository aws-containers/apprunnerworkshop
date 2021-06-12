---
title: 'Setting up ECR'
chapter: true
weight: 30
---

## Setting up an Amazon Elastic Container Registry (ECR)

In order to deploy Dockerfile based services on AWS App Runner, a Docker image must be pushed to ECR.

Start by visiting the ECR console: https://console.aws.amazon.com/ecr/repositories

![Create Repository](/images/getting-started/ecr1.png)

Select "Create Repository" to proceed.

![Create Repository](/images/getting-started/ecr2.png)

Enter `simple-express-repository` as your Repository name, and select “Private” in order to limit access to your repository. Click on “Create repository” in order to finalize creation. Once the repository is created, you'll need to note the URI listed as you'll need to refer to it later.

![View Push Commands](/images/getting-started/view-push-commands.png)

After the ECR repository is created, click the button to "View push commands" and copy the login command from step 1 (choosing your appropriate OS tab).

-----

You will need to replace REGION and AWS_ACCOUNT_ID with the region you are using the AWS console from, and with your AWS account ID for the follow commands:

```
aws ecr get-login-password --region REGION | docker login --username AWS --password-stdin AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com

docker build -t simple-express-repository .

docker tag simple-express-repository:latest AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com/simple-express-repository:latest

docker push AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com/simple-express-repository:latest
```

Return to the AWS App Runner console at: https://console.aws.amazon.com/apprunner/home#/create

Select a repository type of "Container registry" and a provider of "Amazon ECR". Enter the URI listed previously when creating the `simple-express-repository` repository as the container image URI.

You'll need a role which gives the AWS App Runner service access a Trust Relationship with ECR, and has access to required ECR resources. Create an IAM role which has the following trust relationship:

```
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": "build.apprunner.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Attach a policy to this role which allows access to the ECR repository in question:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ecr:*",
            "Resource": "*"
        }
    ]
}
```

Once your role is created with access to ECR, return to https://console.aws.amazon.com/apprunner/home#/create to create an App Runner service using a Dockerfile.

![Create Service](/images/getting-started/docker-build1.png)

Select "Container registry" from repository type, and "Amazon ECR" for provider. Under Container image URI, enter `AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com/simple-express-repository:latest` from above, substituting your AWS_ACCOUNT_ID in, along with your REGION.

Select the service role you created above, and proceed to Next.

![Create Service Part 2](/images/getting-started/docker-build2.png)

Name your service - for example: "simple-express-docker", and enter 3000 for your port, and proceed to Next, then click "Create & deploy" to initialise your service.

Wait for your service to be deployed. You can click on your newly created service and follow the URL to access your service.

![Create Service Part 3](/images/getting-started/docker-status1.png)
