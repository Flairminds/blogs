---
title: AWS Control Tower Setup Guide
date: 2024-04-04
authors: [ShreeyashS]
slug: aws-control-tower-setup-guide
description: >
  Learn how to set up AWS Control Tower to manage your AWS environment effectively.
categories:
  - Cloud Computing
tags:
  - AWS
  - AWS Control Tower
comments: true
---

# AWS Control Tower Setup Guide

## Introduction:
AWS Control Tower is a comprehensive service offered by Amazon Web Services (AWS) that facilitates the setup and management of a multi-account AWS environment. It provides centralized management capabilities, simplifying the implementation of security and compliance controls across your AWS accounts. By leveraging AWS Control Tower, organizations can achieve governance and scale in their cloud infrastructure deployments.

In this guide, we will walk you through the process of setting up AWS Control Tower, creating a landing zone, and configuring organizational units (OUs) to structure your AWS accounts effectively. Whether you are managing a single AWS account or a complex multi-account environment, AWS Control Tower streamlines the administrative tasks and ensures adherence to organizational policies.

<!-- more -->

## Prerequisite
- **AWS Organizations**: Add an AWS account.
- **Audit Account**: This account is for your team of users that need access to the audit information made available by AWS Control Tower. You can also use this account as the access point for third-party tools that will perform programmatic auditing of your environment to help you audit for compliance purposes.
- **Log Archive Account**: This account is for your team of users that need access to all the logging information for all of your enrolled accounts within registered OUs in your landing zone. Create this account before setting up the landing zone.

[Material Metrics Image1]:Aws_Control_Tower_setup/Image1.png
![Material Metrics Image1][Material Metrics Image1]

[Material Metrics Image2]:Aws_Control_Tower_setup/Image2.png
![Material Metrics Image2][Material Metrics Image2]

## Steps to Setup Control Tower
1. **Create a Landing Zone**:
    - A landing zone in AWS Control Tower is like a starting point or foundation for setting up and managing your AWS environment. It is a pre-configured and secure AWS environment that includes multiple AWS accounts organized in a structured manner.
    - Link: [AWS Control Tower Console](https://console.aws.amazon.com/controltower).

[Material Metrics Image3]:Aws_Control_Tower_setup/Image3.png
![Material Metrics Image3][Material Metrics Image3]

[Material Metrics Image4]:Aws_Control_Tower_setup/Image4.png
![Material Metrics Image4][Material Metrics Image4]

2. **Pricing of AWS Control Tower**:
    - There is no extra cost for using AWS Control Tower; you only pay for the services which are enabled by Control Tower.
    
[Material Metrics Image5]:Aws_Control_Tower_setup/Image5.png
![Material Metrics Image5][Material Metrics Image5]

3. **Select Regions**:
    - Select the regions which you want to add under the governance of your landing zone. Click Next.

4. **Configure Organizational Units (OUs)**:
    - Name your organizational units (OUs). You can easily change the OU names or add more later on.
    - AWS Control Tower will create a security OU in which it will create two shared AWS accounts: log-archive and audit. By creating a foundational OU, AWS Control Tower helps establish a structured hierarchy for your AWS accounts, enabling better governance and management. You can also add additional OUs in this landing zone.

[Material Metrics Image6]:Aws_Control_Tower_setup/Image6.png
![Material Metrics Image6][Material Metrics Image6]

5. **Setting up Shared Accounts**:
    - After creating a foundational OU, set up the two shared accounts by adding account email and names for those accounts.
    - It is not mandatory to create new accounts; you can also include existing accounts as log-archive and audit accounts.

[Material Metrics Image7]:Aws_Control_Tower_setup/Image7.png
![Material Metrics Image7][Material Metrics Image7]

6. **Additional Configurations**:
    - In the final stage, you can add additional configurations like setting up IAM identity center to manage access of your team.
    - You can enable or disable CloudTrail to monitor all account activities in the form of logs at a central S3 bucket.

[Material Metrics Image8]:Aws_Control_Tower_setup/Image8.png
![Material Metrics Image8][Material Metrics Image8]

7. **Review and Setup Landing Zone**:
    - Review all your changes and click setup landing zone.

[Material Metrics Image9]:Aws_Control_Tower_setup/Image9.png
![Material Metrics Image9][Material Metrics Image9]

[Material Metrics Image10]:Aws_Control_Tower_setup/Image10.png
![Material Metrics Image10][Material Metrics Image10]

8. **Note**:
    - If user identity is already created, it will use the same.

## Summary:
- You can create different OUs and add domain-specific AWS accounts in those OUs. It will help you organize your accounts for faster account access and better management.
- Other things you can do with Control Tower:
    1. Create a new AWS account.
    2. Add existing AWS account (accounts outside of the landing zone) to the landing zone.
    3. Remove any added AWS account from the landing zone.
