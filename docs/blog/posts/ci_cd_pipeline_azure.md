---
title: Building a CI/CD Pipeline for Azure Blob Storage with GitHub and Azure CLI
date: 2024-02-24
authors: [ShreeyashS]
slug: Building-a-CI/CD-Pipeline-for-Azure-Blob-Storage-with-GitHub-and-Azure-CLI
description: >
  Guide on setting up a CI/CD pipeline using GitHub, Azure DevOps, and Azure CLI for deploying static website files to Azure Blob Storage.
categories:
  - DevOps
tags:
  - DevOps
  - Azure
  - GitHub
  - Azure DevOps
  - Azure CLI
  - CI/CD
comments: true
---

### Title: Building a CI/CD Pipeline for Azure Blob Storage with GitHub and Azure CLI

#### Introduction
In today's fast-paced software development environment, Continuous Integration and Continuous Deployment (CI/CD) pipelines have become essential tools for delivering high-quality software with efficiency and reliability. Azure Blob Storage, a scalable object storage solution in the Azure cloud, offers a convenient way to host static website files, making it an excellent choice for deploying web applications. In this blog post, we will walk through the process of setting up a CI/CD pipeline using GitHub, Azure DevOps, and Azure CLI to automate the deployment of static website files to Azure Blob Storage.

<!-- more -->

#### Prerequisites
Before diving into the tutorial, ensure you have a basic understanding of Git, GitHub, Azure DevOps, and Azure CLI. Additionally, you'll need an active Azure subscription with access to Azure Blob Storage.

#### Step 1: Connecting GitHub to Azure DevOps Pipeline
To kickstart our CI/CD pipeline, we'll begin by creating an agent job in Azure DevOps to connect to our GitHub repository. This job will be responsible for fetching the latest code changes from GitHub whenever a trigger event occurs, such as a new commit or a pull request.

#### Step 2: Building Project Files with a CMD Script
With our source code fetched from GitHub, the next step is to build our project files. We'll accomplish this by writing a CMD script that automates the build process. This script will install necessary dependencies, create a new project structure (if applicable), and execute the build command to generate the required artifacts.

**Example CMD script:**
```cmd
pip install mkdocs-material
pip install mkdocs-minify-plugin
mkdocs new .
mkdocs build
cd site
```

#### Step 3: Writing a Shell Script for Building and Storing Files
In addition to the CMD script, we'll also create a shell script to further streamline the build process. This shell script will execute the necessary commands to build the project files and store them in the desired folder structure, preparing them for deployment to Azure Blob Storage.

#### Step 4: Deploying to Azure Blob Storage with Azure CLI
Once our project files are built and ready for deployment, we'll utilize Azure CLI to copy these files to Azure Blob Storage. By writing a custom Azure CLI script, we can automate the process of uploading the build artifacts to a specified Blob Storage container, making them accessible for hosting our static website.

**Example Azure CLI script:**
```bash
$Container = '$web'
az storage copy --source $(System.DefaultWorkingDirectory)/_Flairminds_blogs/site/* --destination-account-name 'mkdocsblog' --destination-container $Container --recursive
```

#### Step 5: Configuring Azure Blob Storage Container
Before deploying our website to Azure Blob Storage, we need to ensure that the Blob Storage container is properly configured to host a static website. This involves setting up access and permissions for the container, as well as configuring the necessary properties to enable static website hosting.

#### Step 6: Triggering the Pipeline and Monitoring
To complete our CI/CD pipeline setup, we'll configure triggers in Azure DevOps to automatically run the pipeline whenever changes are detected in the GitHub repository. Additionally, we'll set up monitoring to track the execution of our pipeline and troubleshoot any issues that may arise during the deployment process.

#### Conclusion
In this blog post, we've explored the process of building a CI/CD pipeline for deploying static website files to Azure Blob Storage using GitHub, Azure DevOps, and Azure CLI. By automating the deployment process, we can ensure that our website is always up-to-date with the latest changes, resulting in a seamless and efficient development workflow.

#### Additional Resources
For further reading on Azure DevOps, Azure Blob Storage, and CI/CD best practices, check out the following resources:
- [Azure DevOps Documentation](https://docs.microsoft.com/en-us/azure/devops/?view=azure-devops)
- [Azure Blob Storage Documentation](https://docs.microsoft.com/en-us/azure/storage/blobs/)
- [CI/CD Best Practices](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/pipelines-get-started?view=azure-devops)