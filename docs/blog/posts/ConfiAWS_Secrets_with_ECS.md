## README.md

# Securely Passing Secrets to Containers in Amazon ECS Tasks

## Introduction

This guide outlines the steps to securely pass secrets or sensitive information to containers within an Amazon ECS task. Passing sensitive data in plaintext can lead to security vulnerabilities, so it's essential to follow best practices for secure data handling.

## Prerequisites

Before proceeding, ensure you have the following:

* Sensitive information stored in AWS Systems Manager Parameter Store or AWS Secrets Manager.
* Necessary IAM permissions to access Parameter Store or Secrets Manager.
* A task execution IAM role granting permissions for fetching secrets.

## Steps

### 1. Store Sensitive Information

* **For Parameter Store:**

```bash
aws ssm put-parameter --type SecureString --name awsExampleParameter --value awsExampleValue
```

* **For Secrets Manager:**

```bash
aws secretsmanager create-secret --name awsExampleParameter --secret-string awsExampleValue
```

### 2. Set up IAM Roles

* Create an IAM role with trust relation for `ecs-tasks.amazonaws.com`.
* Attach inline policy with permissions for `ssm:GetParameters` and `secretsmanager:GetSecretValue`.

### 3. Reference Secrets in Task Definition

**A. From AWS Management Console:**

* Create a new Task Definition in the Amazon ECS console.
* Choose your launch type and specify the task execution IAM role.
* Add a container and define environment variables referencing Parameter Store or Secrets Manager ARN.

**B. From AWS CLI:**

* Reference Parameter Store or Secrets Manager resources in the task definition JSON file.
* Register the task definition using AWS CLI.

### 4. Handling Updates

* Note that sensitive data is injected into containers when initially started.
* If secrets are updated or rotated, launch a new task or update the service with the "Force new deployment" option.

## Conclusion

By following these steps, you can securely pass secrets or sensitive information to containers within Amazon ECS tasks, reducing the risk of data exposure and enhancing overall security posture.
