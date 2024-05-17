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

## Troubleshooting: Common Errors

### Error: `AccessDeniedException`

![image](https://github.com/chhayasingh0112/blogs/assets/72135131/80e016ac-e9cb-44f9-b511-9853d28ddd57)

If you encounter an error like the following:

```plaintext
ResourceInitializationError: unable to pull secrets or registry auth: execution resource retrieval failed: unable to retrieve secret from asm: service call has been retried 1 time(s): failed to fetch secret arn:aws:secretsmanager:ap-south-1:221192224682:secret:awsExampleSecret-7qFlRJ from secrets manager: AccessDeniedException: User: arn:aws:sts::221192224682:assumed-role/ecsTaskExecutionRole/26e17af95b5e431893308026b892584f is not authorized to perform: secretsmanager:GetSecretValue on resource: arn:aws:secretsmanager:ap-south-1:221192224682:secret:awsExampleSecret-7qFlRJ because no identity-based policy allows the secretsmanager:GetSecretValue action status code: 400, request id: 359958d1-e041-4547-9bfa-1e289cd3a745
```

This error indicates that the ECS task execution role does not have the necessary permissions to access the secret in AWS Secrets Manager. Specifically, the role `ecsTaskExecutionRole` is not authorized to perform the `secretsmanager:GetSecretValue` action on the specified secret.

#### Solution

To resolve this issue, update the IAM policy attached to the `ecsTaskExecutionRole` to allow it to perform the `secretsmanager:GetSecretValue` action on the specified secret.

1. **Identify the ECS Task Execution Role**:
   - Confirm the IAM role used by your ECS task. Based on the error message, it appears to be `ecsTaskExecutionRole`.

2. **Modify the IAM Policy**:
   - Go to the AWS Management Console.
   - Navigate to the IAM service.
   - Find and select the `ecsTaskExecutionRole`.

3. **Update the Policy to Allow Secrets Manager Access**:
   - If the role already has an inline policy, you can edit it. Otherwise, you will need to attach a new policy.
   - Add a new policy or update the existing policy to include permissions for `secretsmanager:GetSecretValue`.

Here’s an example of an IAM policy that grants the necessary permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "secretsmanager:GetSecretValue"
      ],
      "Resource": "arn:aws:secretsmanager:ap-south-1:221192224682:secret:awsExampleSecret-7qFlRJ"
    }
  ]
}
```

4. **Attach the Policy to the Role**:
   - If creating a new policy, attach it to the `ecsTaskExecutionRole`.
   - If updating an existing policy, ensure the updated policy is saved and associated with the `ecsTaskExecutionRole`.

5. **Verify the Changes**:
   - Once the policy is updated, re-run your ECS task.
   - Verify that the task can now retrieve the secret without encountering the `AccessDeniedException`.

By ensuring that the `ecsTaskExecutionRole` has the correct permissions to access the secrets in Secrets Manager, your ECS tasks should be able to retrieve the required secrets without any issues.


![image](https://github.com/chhayasingh0112/blogs/assets/72135131/ec87d3dd-44b7-43d7-92c6-1fb10415d802)

## Force New Deployment

If secrets are updated or rotated, you must launch a new task to receive the updated value.

### Using Amazon ECS Console

1. Open the Amazon ECS console.
2. Choose Clusters, select the cluster with your service.
3. Select the Force New Deployment check box, and then choose Update Service.




### Using AWS CLI

```sh
aws ecs update-service --cluster yourClusterName --service yourService
