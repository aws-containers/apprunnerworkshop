---
title: "Create pre-requisites for the app"
chapter: false
weight: 17
---

The app uses DynamoDB as a storage backend for the caching, to reduce the number of calls to the
GitHub API. Before we deploy our application, we need to create a DynamoDB table, and ensure that
our application is granted permissions to read and write to the table.

## Examine and deploy the CloudFormation stack

To simplify the steps for creating the required IAM role an DynamoDB table, a CloudFormation
template is part of the repository we have forked.

### Let's take a look at the CloudFormation template

In the provided CloudFormation template, two resources are provided, a DynamoDB table, and an
IAM Role.

```shell
$ cat ~/environment/repostatus-gh-demo/hack/apprunner-prereqs-cfn.yaml
```

### Deploy the CloudFormation stack

Execute the following command to deploy the CloudFormation stack

```shell
$ cd ~/environment/repostatus-gh-demo && aws cloudformation deploy \
  --stack-name repostatus-gh-demo-infra \
  --template-file hack/apprunner-prereqs-cfn.yaml \
  --capabilities CAPABILITY_IAM
```

The output should look similar to this:

```text
Waiting for changeset to be created..
Waiting for stack create/update to complete
Successfully created/updated stack - repostatus-gh-demo-infra
```

Use the following command to inspect what resources have been created by the CloudFormation stack

```shell
$ aws cloudformation describe-stack-resources --stack-name repostatus-gh-demo-infra --output text
STACKRESOURCES  Role    repostatus-gh-demo-infra-Role-1T58V5WPCQH6S     CREATE_COMPLETE AWS::IAM::Role  arn:aws:cloudformation:eu-west-1:1234567891012:stack/repostatus-gh-demo-infra/3e9d5060-c917-11eb-9cd7-0610fe338635       repostatus-gh-demo-infra        2021-06-09T11:39:44.638000+00:00
DRIFTINFORMATION        NOT_CHECKED
STACKRESOURCES  Table   repostatus_cache        CREATE_COMPLETE AWS::DynamoDB::Table    arn:aws:cloudformation:eu-west-1:1234567891012:stack/repostatus-gh-demo-infra/3e9d5060-c917-11eb-9cd7-0610fe338635       repostatus-gh-demo-infra        2021-06-09T11:39:24.537000+00:00
DRIFTINFORMATION        NOT_CHECKED
```

That's it for pre-prequisities, now we are ready to move on to AWS App Runner.
