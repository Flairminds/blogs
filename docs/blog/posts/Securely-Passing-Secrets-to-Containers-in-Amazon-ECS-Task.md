---
title: Securely Passing Secrets to Containers in Amazon ECS
date: 2024-05-17
authors: [Chhaya]
slug: Securely-Passing-Secrets-to-Containers-in-Amazon-ECS
description: >
  Guide to securely passing secrets or sensitive information to containers in an Amazon ECS task using AWS Systems Manager Parameter Store and AWS Secrets Manager.
categories:
  - DevOps
tags:
  - DevOps
  - AWS
  - ECS
  - Security
---

# Securely Passing Secrets to Containers in Amazon ECS

## Overview

Passing sensitive data in plaintext can cause security issues, as it's discoverable in the AWS Management Console or through AWS APIs such as DescribeTaskDefinition or DescribeTasks. This guide provides a step-by-step approach to securely inject data into containers by referencing values stored in AWS Systems Manager Parameter Store or AWS Secrets Manager in the container definition of an Amazon ECS task definition.

<!-- more -->

## Prerequisites

Before passing secrets to your ECS containers, ensure you have stored your sensitive information in either AWS Systems Manager Parameter Store or AWS Secrets Manager.

## Store Sensitive Information

### Using AWS Systems Manager Parameter Store

Run the following command, replacing `awsExampleParameter` with your parameter name and `awsExampleValue` with your secure value:

```sh
aws ssm put-parameter --type SecureString --name awsExampleParameter --value awsExampleValue
```

### Using AWS Secrets Manager

Run the following command, replacing `awsExampleParameter` with your parameter name and `awsExampleValue` with your secret value:

```sh
aws secretsmanager create-secret --name awsExampleParameter --secret-string awsExampleValue
```

**Note:** Ensure the task execution IAM role has permissions for `ssm:GetParameters`, `secretsmanager:GetSecretValue`, and `kms:Decrypt`.

## Create IAM Role and Policy

### Create a Role with a Trust Relationship

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

![image](https://github.com/chhayasingh0112/blogs/assets/72135131/240a3fca-09b1-4ac2-9b5d-34e81e0e544e)

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

## Conclusion

By following these steps, you can securely pass sensitive data to your Amazon ECS containers, ensuring best practices for security and data integrity.
