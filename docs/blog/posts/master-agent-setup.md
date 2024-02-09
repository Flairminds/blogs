---
title: Setup of Jenkins Master and Slave Agent on AWS EC2
date: 2024-02-01
authors: [suraj]
slug: Setup-of-Jenkins-Master-and-Slave-Agent-on-AWS-EC2
description: >
  Guide to creation and setup of jenkins master and slave agent on aws ec2 instance
categories:
  - DevOps
tags:
  - DevOps
  - CI/CD
  - Jenkins
  - Agents
---
# **Setup of jenkins master agent and slave agent on AWS ec2 instance**

## Introduction
In the realm of continuous integration and deployment, Jenkins stands as a powerful automation tool that streamlines the software development process. By leveraging Jenkins Master and Slave agents, you can distribute workloads across multiple nodes, optimizing performance and scalability. This step-by-step guide is designed to walk you through the process of setting up Jenkins Master and Slave agents on AWS EC2 instances.

<!-- more -->

## Problem Statement
Many software development teams face challenges in optimizing their continuous integration and deployment workflows. This guide aims to address the complexities involved in setting up Jenkins Master and Slave agents on AWS EC2 instances, providing solutions for efficient and scalable automation in cloud-based environments.

## Prerequisites
- Launch 2 AWS ec2 instances for jenkins master and slave agent.
- Create a security group that allows inbound traffic from ssh, http, https, and custom tcp from port 8080 and apply this to both ec2 instances.

## **Jenkins Master-Agent Creation**

### Step 1: Installation of Jenkins

1. Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:
   ```bash
   sudo yum update –y
   ```
2. Add the Jenkins repo using the following command:
   ```bash
   sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/redhat-stable/jenkins.repo
   ```
3. Import a key file from Jenkins-CI to enable installation from the package:
   ```bash
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
   sudo yum upgrade
   ```
4. Install Java (Amazon Linux 2023):
   ```bash
   sudo dnf install java-17-amazon-corretto -y
   ```
5. Install Jenkins:
   ```bash
   sudo yum install jenkins -y
   ```
6. Enable the Jenkins service to start at boot:
   ```bash
   sudo systemctl enable jenkins
   ```
7. Start Jenkins as a service:
   ```bash
   sudo systemctl start jenkins
   ```
8. You can check the status of the Jenkins service using the command:
   ```bash
   sudo systemctl status Jenkins
   ```
![image](https://github.com/Flairminds/blogs/assets/135031436/f56a8209-c87e-4db4-bfb6-d5fd10ce628e)


### Step 2: Configuring Jenkins to create a master agent on ec2

1. Connect to http://<your_server_public_or_private_address\>:8080 from your browser. You will be able to access Jenkins through its management interface:![image](https://github.com/Flairminds/blogs/assets/135031436/4101ebd6-eefa-4c7c-824b-a487cefab52f)
2. As prompted, enter the password found in **/var/lib/jenkins/secrets/initialAdminPassword**.![image](https://github.com/Flairminds/blogs/assets/135031436/3635e206-f86a-4adf-aae0-84f8e4bd1732)
3. Once the installation is complete, the **Create First Admin User** will open. Enter your information, and then select **Save and Continue**.![image](https://github.com/Flairminds/blogs/assets/135031436/62ff5a7c-e391-4ab1-8b95-5eae03a6d611)
4. On the left-hand side, select **Manage Jenkins**, and then select **Manage Plugins**.
5. Select the **Available** tab, and then enter **Amazon EC2 plugin** at the top right.
6. Select the checkbox next to **Amazon EC2 plugin**, and then select **Install without restart**.

![image](https://github.com/Flairminds/blogs/assets/135031436/06be932e-b0e9-475d-be76-9701c25f5fdd)

### Step 3: Verify your master agent as build-in-node and it is in synched

![image](https://github.com/Flairminds/blogs/assets/135031436/2810a64b-5e39-4cd3-99a4-743ae01afcb5)

## **Jenkins Slave-Agent Creation**

### Step 1: [Refer this step in order to install jenkins](#step-1-installation-of-jenkins)

### Step 2: Create a Node.

- Go under manage Jenkins section from dashboard -> Select Nodes -> Create a new node and give it a name and choose as Permanent Type.

![image](https://github.com/Flairminds/blogs/assets/135031436/5bbd6f78-13cd-41c0-99f0-928a259e092b)

![image](https://github.com/Flairminds/blogs/assets/135031436/9db58f00-62ac-4bc7-ab23-3b2d902ac8cc)

### Step 3: Configuring Node

1. Give host as Public ip of your slave ec2 instance and in credentials click on Add.![image](https://github.com/Flairminds/blogs/assets/135031436/0f620c53-f091-4c9f-9d8e-be546229d444)![image](https://github.com/Flairminds/blogs/assets/135031436/584b9e18-5bd4-4a07-a193-1df0f68429eb)
2. Enter private key of slave-agent ec2.![image](https://github.com/Flairminds/blogs/assets/135031436/5e00d5d0-a390-4fac-afa7-59477ecd5d12)
3. In host key verification strategy select non verifying.
4. Save.

### Step 4: You will see that your agent will be in sync .

![image](https://github.com/Flairminds/blogs/assets/135031436/1890227e-bbc7-4c97-b45b-b63ea865aea4)

## Conclusion:
In wrapping up, you've successfully established a robust Jenkins infrastructure on AWS EC2, empowering your team with efficient and scalable CI/CD capabilities. With Master and Slave agents configured, you're poised to accelerate development cycles and enhance overall software delivery. Cheers to a streamlined and automated workflow!

