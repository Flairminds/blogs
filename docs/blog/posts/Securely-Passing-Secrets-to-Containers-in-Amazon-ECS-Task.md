# Securely Passing Secrets to Containers in Amazon ECS

This repository provides guidance and code snippets for securely passing secrets or sensitive information to containers in an Amazon ECS task. Passing sensitive data in plaintext can pose security risks, as it might be exposed in the AWS Management Console or through AWS APIs. As a best practice, use AWS Systems Manager Parameter Store or AWS Secrets Manager to securely inject data into containers as environment variables or in log configurations.

## Table of Contents

- [Short Description](#short-description)
- [Prerequisites](#prerequisites)
- [Store Sensitive Information](#store-sensitive-information)
  - [Using AWS Systems Manager Parameter Store](#using-aws-systems-manager-parameter-store)
  - [Using AWS Secrets Manager](#using-aws-secrets-manager)
- [Create IAM Role and Policy](#create-iam-role-and-policy)
  - [Create a Role with a Trust Relation](#create-a-role-with-a-trust-relation)
  - [Create an Inline Policy](#create-an-inline-policy)
  - [(Optional) Attach Managed Policy](#optional-attach-managed-policy)
- [Reference Sensitive Information in ECS Task Definition](#reference-sensitive-information-in-ecs-task-definition)
  - [Using AWS Management Console](#using-aws-management-console)
  - [Using AWS CLI](#using-aws-cli)
- [Force New Deployment](#force-new-deployment)
  - [Using Amazon ECS Console](#using-amazon-ecs-console)
  - [Using AWS CLI](#using-aws-cli)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## Short Description

Pass sensitive information to containers securely by referencing values stored in AWS Systems Manager Parameter Store or AWS Secrets Manager in the container definition of an Amazon ECS task definition. This can be done for:
- Tasks using AWS Fargate platform version 1.3.0 or greater
- Container instances using amazon-ecs-agent version 1.22.0 or greater

## Prerequisites

1. Store your sensitive information in AWS Systems Manager Parameter Store or Secrets Manager.

## Store Sensitive Information

### Using AWS Systems Manager Parameter Store

```sh
aws ssm put-parameter --type SecureString --name awsExampleParameter --value awsExampleValue
```

### Using AWS Secrets Manager

```sh
aws secretsmanager create-secret --name awsExampleParameter --secret-string awsExampleValue
```

**Note:** Ensure that the task execution IAM role has permissions for `ssm:GetParameters`, `secretsmanager:GetSecretValue`, and `kms:Decrypt`.

## Create IAM Role and Policy

### Create a Role with a Trust Relation

1. Open the IAM console.
2. Create a role with the following trust relationship for `ecs-tasks.amazonaws.com`:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": "ecs-tasks.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

### Create an Inline Policy

1. Open the IAM console.
2. Choose Roles, select the created role, and then choose Add inline policy on the Permissions tab.
3. Choose the JSON tab and add the following policy, replacing the placeholders with your values:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ssm:GetParameters",
        "secretsmanager:GetSecretValue"
      ],
      "Resource": [
        "arn:aws:ssm:us-east-1:awsExampleAccountID:parameter/awsExampleParameter",
        "arn:aws:secretsmanager:us-east-1:awsExampleAccountID:secret:awsExampleParameter*"
      ]
    }
  ]
}
```

### (Optional) Attach Managed Policy

Attach the managed policy `AmazonECSTaskExecutionRolePolicy` for tasks that use Amazon ECR images or send logs to Amazon CloudWatch.

## Reference Sensitive Information in ECS Task Definition

### Using AWS Management Console

1. Open the Amazon ECS console.
2. Navigate to Task Definitions and choose Create new Task Definition.
3. Select your launch type and proceed to the next step.
4. Choose the task execution IAM role created earlier.
5. Add a container in the Container Definitions section.
6. In the Environment variables section, enter a key for your environment variable.
7. Choose `ValueFrom` for the value and enter the ARN of your Parameter Store or Secrets Manager resource.

### Using AWS CLI

1. Create a task definition JSON file with the following structure, replacing the placeholders with your values:

```json
{
  "requiresCompatibilities": ["EC2"],
  "networkMode": "awsvpc",
  "containerDefinitions": [
    {
      "name": "web",
      "image": "httpd",
      "memory": 128,
      "essential": true,
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp"
        }
      ],
      "logConfiguration": {
        "logDriver": "splunk",
        "options": {
          "splunk-url": "https://sample.splunk.com:8080"
        },
        "secretOptions": [
          {
            "name": "splunk-token",
            "valueFrom": "arn:aws:secretsmanager:us-east-1:awsExampleAccountID:secret:awsExampleParameter"
          }
        ]
      },
      "secrets": [
        {
          "name": "DATABASE_PASSWORD",
          "valueFrom": "arn:aws:ssm:us-east-1:awsExampleAccountID:parameter/awsExampleParameter"
        }
      ]
    }
  ],
  "executionRoleArn": "arn:aws:iam::awsExampleAccountID:role/awsExampleRoleName"
}
```

2. Register the task definition:

```sh
aws ecs register-task-definition --family-name yourTaskDefinitionFamily --cli-input-json file://pathToYourJsonFile
```
![image](https://github.com/chhayasingh0112/blogs/assets/72135131/d987a10c-7d37-4ba2-b179-55ecaa00dfb5)

## Force New Deployment

If secrets are updated or rotated, you must launch a new task to receive the updated value.

### Using Amazon ECS Console

1. Open the Amazon ECS console.
2. Choose Clusters, select the cluster with your service.
3. Select the Force New Deployment check box, and then choose Update Service.

### Using AWS CLI

```sh
aws ecs update-service --cluster yourClusterName --service yourServiceName --force-new-deployment
```

## Example Code

Refer to the code snippets provided in the [Store Sensitive Information](#store-sensitive-information), [Create IAM Role and Policy](#create-iam-role-and-policy), and [Reference Sensitive Information in ECS Task Definition](#reference-sensitive-information-in-ecs-task-definition) sections for implementation details.

## Conclusion

Following these steps helps ensure that sensitive data is securely injected into your Amazon ECS containers, maintaining best practices for security and data integrity.
