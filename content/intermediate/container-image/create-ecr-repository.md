---
title: 'Create ECR repository'
chapter: true
weight: 22
---

# Create ECR repository

Our first step will be to create a _repository_ in ECR, this is where we later will store our
container image once it's been built.

Let's create our repository:

```shell
$ aws ecr create-repository --repository-name apprunnerworkshop-app
{
    "repository": {
        "repositoryUri": "1234567891012.dkr.ecr.eu-west-1.amazonaws.com/apprunnerworkshop-app", 
        "imageScanningConfiguration": {
            "scanOnPush": false
        }, 
        "encryptionConfiguration": {
            "encryptionType": "AES256"
        }, 
        "registryId": "1234567891012", 
        "imageTagMutability": "MUTABLE", 
        "repositoryArn": "arn:aws:ecr:eu-west-1:1234567891012:repository/apprunnerworkshop-app", 
        "repositoryName": "apprunnerworkshop-app", 
        "createdAt": 1623314531.0
    }
}
```

We are interested in using the `repositoryUri` later, so that we can tag and push images to the
repository, let's go ahead and store that as an environment variable for easy access later on.

```shell
$ export ECR_REPOSITORY_URI=$(aws ecr describe-repositories --repository-names apprunnerworkshop-app --query 'repositories[?repositoryName==`apprunnerworkshop-app`].repositoryUri' --output text)
$ echo $ECR_REPOSITORY_URI
1234567891012.dkr.ecr.eu-west-1.amazonaws.com/apprunnerworkshop-app
```

Great, we have created our repository, let's move on to the next step, which is building our image
and pushing it to the registry.
