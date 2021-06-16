---
title: 'Clean Up'
weight: 100
---

## App Runner Service

```shell
$ aws apprunner list-services --query 'ServiceSummaryList[?ServiceName==`apprunnerworkshop-app`].ServiceArn' --output text | \
  xargs -I{} aws apprunner delete-service --service-arn {}
```

## Resources provisioned via CloudFormation


```shell
$ aws cloudformation delete-stack --stack-name repostatus-gh-demo-infra

```

## IAM role for ECR access

```shell
$ aws iam delete-role --role-name $ROLE_NAME
```

## Cloud 9 Environment

Go to the Cloud 9 console, select the _apprunnerworkshop_ Cloud 9 environment, and finally click
_Delete_.

![Delete Cloud9](/images/delete-cloud9.png)
