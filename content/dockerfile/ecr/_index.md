---
title: 'Setting up ECR'
chapter: true
weight: 30
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Setting up an Amazon Elastic Container Registry (ECR)

In order to deploy Dockerfile based services on AWS App Runner, a Docker image must be pushed to ECR.

Start by visiting the ECR console: https://console.aws.amazon.com/ecr/repositories

![Create Repository](/images/ecr1.png)

Select "Create Repository" to proceed.

![Create Repository](/images/ecr2.png)

Enter `simple-express-repository` as your Repository name, and select “Private” in order to limit access to your repository. Click on “Create repository” in order to finalize creation. One the repository is created, you'll need to note the URI listed as you'll need to refer to it later.

You will need to replace REGION and AWS_ACCOUNT_ID with the region you are using the AWS console from, and with your AWS account ID for the follow commands:

```aws ecr get-login-password --region REGION | docker login --username AWS --password-stdin AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com
docker build -t simple-express-container .
docker push AWS_ACCOUNT_ID.dkr.ecr.REGION.amazonaws.com/simple-express-container:latest```

Return to the AWS App Runner console at: https://console.aws-dev.amazon.com/fusion/home#/create

Select a repository type of "Container registry" and a provider of "Amazon ECR". Enter the URI listed previously when creating the `simple-express-repository` repository as the container image URI.

You'll need a role which gives the AWS App Runner service access a Trust Relationship with ECR, and has access to required ECR resources. TEMPORARY NOTE: This will presumably change soon, for now the following trust relationship should work:

```{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": "us-east-1.gamma.cells.build.bullet.aws.internal"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}```

TODO
