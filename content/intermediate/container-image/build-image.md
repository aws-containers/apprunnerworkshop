---
title: 'Building the image'
chapter: true
weight: 23
---

# Building the image

It's time to build our image, but before we can do that, we need to retrieve login credentials for
our local container engine, so that we can push the image

```shell
$ export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query 'Account' --output text)
$ export AWS_REGION=[AWS_REGION]  # Change this to the region you are using, for example eu-west-1

$ aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
Login Succeeded
```

The `Dockerfile` contains the instructions for assembling our container image. Ours is relatively
straight forward, and contains only a few directives for adding our source code to the image,
instructions for how to install dependencies, and finally what command to use for running the app.
Let's have a look:

```shell
$ cat ~/environment/repostatus-gh-demo/Dockerfile
```

Let's go ahead and build our app.

```shell
$ cd ~/environment/repostatus-gh-demo
$ docker build -t apprunnerworkshop-app:demo .
[build output omitted]

$ docker tag apprunnerworkshop-app:demo $ECR_REPOSITORY_URI:demo
$ docker push $ECR_REPOSITORY_URI:demo
```

We have now built our application image and pushed it to ECR. Let's move on to setting up AWS App
Runner.
