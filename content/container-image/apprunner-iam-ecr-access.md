---
title: 'Configure App Runner ECR access'
chapter: true
weight: 23
---

# Configure App Runner ECR Access

Before we create our App Runner service, we need to setup permissions so that App Runner can read
from our ECR repository.

## Create IAM role

Let's start by creating an IAM role that App Runner will use, and the roles corresponding trust
policy.

```shell
$ export TP_FILE=$(mktemp)
$ export ROLE_NAME=AppRunnerWorkshopAccessRole
$ cat <<EOF | tee $TP_FILE
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "build.apprunner.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
EOF
$ aws iam create-role --role-name $ROLE_NAME --assume-role-policy-document file://$TP_FILE
$ rm $TP_FILE
```

Now we need to attach a policy to the IAM role which grants access to ECR. We will be using a
_managed policy_ which will grant the appropriate access. Let's first inspect the policy:

```shell
$ aws iam get-policy --policy-arn arn:aws:iam::aws:policy/service-role/AWSAppRunnerServicePolicyForECRAccess --query 'Policy.DefaultVersionId' --output text | \
  xargs -I{} aws iam get-policy-version --policy-arn arn:aws:iam::aws:policy/service-role/AWSAppRunnerServicePolicyForECRAccess --version-id {}

{
    "PolicyVersion": {
        "CreateDate": "2021-05-14T19:17:21Z", 
        "VersionId": "v1", 
        "Document": {
            "Version": "2012-10-17", 
            "Statement": [
                {
                    "Action": [
                        "ecr:GetDownloadUrlForLayer", 
                        "ecr:BatchGetImage", 
                        "ecr:DescribeImages", 
                        "ecr:GetAuthorizationToken", 
                        "ecr:BatchCheckLayerAvailability"
                    ], 
                    "Resource": "*", 
                    "Effect": "Allow"
                }
            ]
        }, 
        "IsDefaultVersion": true
    }
}
```

Let's attach the policy to our role:

```shell
$ aws iam attach-role-policy --role-name $ROLE_NAME --policy-arn arn:aws:iam::aws:policy/service-role/AWSAppRunnerServicePolicyForECRAccess
```

Now that we have configured our IAM role and policy, let's go to App Runner and create our service.
