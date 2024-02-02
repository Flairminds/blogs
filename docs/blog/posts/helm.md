---
title: Helm:- A Complete Guide
date: 2024-02-02
authors: [suraj]
slug: Helm:-A-Complete-Guide
description: >
  A complete guide about helm, helm's component, architecture & how it works.
categories:
  - DevOps
tags:
  - DevOps
  - Helm
  - K8's
---
# <p align="center">Helm: A Complete Guide</p>

## What is Helm?

Helm is a tool that automates the creation, packaging, configuration, and deployment of Kubernetes applications by combining your configuration files into a single reusable package.
In a microservice architecture, you create more microservices as the application grows, making it increasingly difficult to manage. Kubernetes, an open source container orchestration technology, simplifies the process by grouping multiple microservices into a single deployment. Yet managing Kubernetes applications across the development lifecycle brings its own set of challenges, including version management, resource allocation, updating, and rollbacks.

Helm provides one of the most accessible solutions to this problem, making deployments more consistent, repeatable, and reliable. In this article, you’ll learn about Helm and its use cases, as well as how to decide if you should adopt it for your Kubernetes projects.
In the following sections, we will review the different components of Helm and how they help to simplify Kubernetes management.

<!-- more -->

## Helm Charts

A Helm chart is a package that contains all the necessary resources to deploy an application to a Kubernetes cluster. This includes YAML configuration files for deployments, services, secrets, and config maps that define the desired state of your application.
A Helm chart packages together YAML files and templates that can be used to generate additional configuration files based on parametrized values. This allows you to customize configuration files to suit different environments and to create reusable configurations for use across multiple deployments. Additionally, each Helm chart can be versioned and managed independently, making it easy to maintain multiple versions of an application with different configurations.

## Configs
The config contains application configurations that you usually store in a YAML file. Resources in the Kubernetes cluster are deployed based on these values.

## Releases
A running instance of a chart is known as a release. When you run the **helm install command**, it pulls the config and chart files and deploys all the Kubernetes resources.

## Repositories
The Helm repository is where you can upload Helm charts. You can also create a private repository to share charts within your organization. Artifact Hub is a global Helm repository that features searchable charts that you can install for numerous purposes. In short, Artifact Hub does for Helm charts what Docker Hub does for Docker images.

## Architecture
Now that you understand these Helm concepts, here is a look at Helm’s architecture. Helm’s architecture has two main components: client and library.

A Helm client is a command-line utility for end users to control local chart development and manage repositories and releases. Just like using the MySQL database client to run MySQL commands, you use the Helm client to run Helm commands.

The Helm library does all the heavy lifting. It contains the actual code to perform the operations specified in the Helm command. The combination of config and chart files to create any release is handled by the Helm library.

The Helm architecture has improved significantly between versions 2 and 3. Version 2 used a Tiller server to mediate between the Helm client and the Kubernetes API server. It kept track of all the resources created using Helm. In favor of a client-only architecture, version 3 removed the Tiller server, instead using a direct API connection to interact with the Kubernetes API server.

## How Helm works
The Helm application library uses charts to define, create, install, and upgrade Kubernetes applications. Helm charts allow you to manage Kubernetes manifests without using the Kubernetes command-line interface (CLI) or remembering complicated Kubernetes commands to control the cluster.

Consider a practical scenario where Helm is helpful. Suppose you want to deploy your application in a production environment with ten replicas. You specify this in the deployment YAML file for the application and run the deployment using the kubectl command.

Now, run the same application in a staging environment. Assume that you need three replicas in staging and that you will run an internal application build in the staging environment. To do this, update the replicas count and the Docker image tag in the deployment YAML file and then use it in the staging Kubernetes cluster.

As your application becomes more complex, the number of YAML files increases. Eventually, the configurable fields in the YAML file also increase. Soon, updating many YAML files to deploy the same app in different environments becomes hard to manage.

Using Helm, you can parameterize the fields depending on the environment. In the previous example, instead of using a static value for replicas and Docker images, you can take the value for these fields from another file. This file is called values.yaml.

![image](https://github.com/SurajJaiswal2002/blogs/assets/143254595/915b6aec-63c2-4277-b687-45eb56ccda03)

Now, you can maintain a values file for each environment with the proper values for each. Helm helps you decouple the configurable field values from the actual YAML configuration.

![image](https://github.com/SurajJaiswal2002/blogs/assets/143254595/2f07d04a-f13e-412d-b79b-ea2641ae304d)

## Conclusion
In this article, you learned about Helm and how it simplifies deployment in Kubernetes. You also learned about all the core concepts of Helm, like Helm charts, repositories, deployments, and more.

Helm is a valuable tool for managing the deployment of multiple containers as a single unit. Some key benefits of using Helm include the ability to easily manage the deployment of complex microservice-based applications, the ability to provide a consistent and organized approach to managing the deployment process, and the ability to manage the deployment of containers across multiple environments. These capabilities make it an essential tool for organizations that rely on container-based applications.
