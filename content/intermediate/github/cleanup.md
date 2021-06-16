---
title: 'Cleanup'
chapter: true
weight: 15
---

# Clean up

Let's remove our App Runner service using the AWS CLI

Find our App Runner service ARN and delete it in one step.

```shell
$ aws apprunner list-services --query 'ServiceSummaryList[?ServiceName==`apprunnerworkshop-app`].ServiceArn' --output text | \
  xargs -I{} aws apprunner delete-service --service-arn {}
```

## [Optional] Delete DynamoDB table and IAM role

In the pre-requisities for this section, we created a DynamoDB table and an IAM role using
CloudFormation. If you are **NOT** proceeding with the next section of the workshop, you can delete
those now, otherwise, clean them up after the final section:

```shell
$ aws cloudformation delete-stack --stack-name repostatus-gh-demo-infra
```
