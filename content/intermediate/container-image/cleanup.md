---
title: 'Cleanup'
chapter: true
weight: 26
---

# Clean up

Let's remove our App Runner service using the AWS CLI

Find our App Runner service ARN and delete it in one step.

```shell
$ aws apprunner list-services --query 'ServiceSummaryList[?ServiceName==`apprunnerworkshop-app`].ServiceArn' --output text | \
  xargs -I{} aws apprunner delete-service --service-arn {}
```

## Delete DynamoDB table and IAM role

In the pre-requisities for this section, we created a DynamoDB table and an IAM role using
CloudFormation, let's clean those up as well:

```shell
$ aws cloudformation delete-stack --stack-name repostatus-gh-demo-infra
$ aws iam detach-role-policy --role-name $ROLE_NAME --policy-arn arn:aws:iam::aws:policy/service-role/AWSAppRunnerServicePolicyForECRAccess
$ aws iam delete-role --role-name $ROLE_NAME
```
