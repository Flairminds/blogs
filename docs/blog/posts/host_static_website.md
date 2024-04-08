---
title: How to Host a Website on Azure Blob Storage A Simple Guide for You
date: 2024-02-08
authors: [shreeyashs]
slug: hosting-website-azure-blob-storage-guide
description: >
  Learn how to effortlessly host your static website on Azure Blob Storage with this step-by-step guide.
categories:
  - Azure
tags:
  - Azure
  - Azure Blob Storage
  - Static Website
  - Hosting
comments: true
---

# How to Host a Website on Azure Blob Storage: A Simple Guide for You

## Introduction:
So you've got a website and you're looking for a hassle-free way to host it without breaking the bank? Well, you're in luck! Azure Blob Storage offers a super easy and cost-effective solution for hosting static websites. This guide will walk you through the steps, making it a breeze.

<!-- more -->

## Step 1: Setting Up Your Storage Account:
1. Head over to the Azure portal (https://portal.azure.com) and log in.
2. Click on "Create a resource" in the top-left corner.
3. Search for "Storage account" and give it a click.
4. Hit "Create" and fill in the necessary details like your storage account name, location, and performance options.
5. Once done, give it a once-over and hit "Review + create" to set up your storage account.

## Step 2: Enabling Static Website Hosting:
1. Now that you've got your storage account set up, find it in the Azure portal and open it up.
2. Look for "Static website" in the left-hand menu under Settings and click on it.
3. Toggle the switch to "Enabled" - easy as pie!
4. Enter the name of your index document (like index.html) and any error document if you have one.
5. Click "Save" and you're good to go!

[Material Metrics Screenshot_18]:host_static_website/Screenshot_18.png
![Material Metrics Screenshot_18][Material Metrics Screenshot_18]


## Step 3: Uploading Your Website Content:
1. In your storage account overview, find and click on "Containers" in the menu.
2. You'll see a container named "$web" - click on that bad boy.
3. Now, all you gotta do is upload your website content. Just drag and drop your files or use the "Upload" button.
4. Make sure your website content includes the index document you mentioned earlier.

[Material Metrics Screenshot_1]:host_static_website/Screenshot_1.png
![Material Metrics Screenshot_1][Material Metrics Screenshot_1]

## Step 4: Configuring Front Door CDN (Optional):
1. Open the Azure portal (https://portal.azure.com) and navigate to your resource group.
2. Click on "Create a resource" in the top-left corner and search for "Front Door" in the marketplace.
3. Select "Front Door" from the search results and click on "Create."
4. Fill in the required details such as subscription, resource group, and Front Door name.
5. Choose your preferred pricing tier and click "Next" to configure routing rules and endpoints.
6. Follow the setup wizard to add your static website as an endpoint and configure caching rules for optimal performance.
7. Review your settings and click on "Review + create" to create your Front Door instance.
8. Once created, navigate to your Front Door instance and note the Front Door endpoint.
9. Update your DNS settings to point to the Front Door endpoint to direct traffic through the CDN.
10. Your static website is now configured to leverage the Front Door CDN for improved performance and scalability.

[Material Metrics Screenshot_2]:host_static_website/Screenshot_2.png
![Material Metrics Screenshot_2][Material Metrics Screenshot_2]

## Step 5: Checking Out Your Website:
1. Once everything's uploaded and configured, find the primary endpoint provided in the Azure portal.
2. If you set up a custom domain, you can use that too.
3. Give your website a visit and make sure everything's working as it should.

## Conclusion:
Hosting your static website on Azure Blob Storage is a piece of cake! With these simple steps, you can have your website up and running in no time, without the hassle of complicated setups. If you need a hand or have any questions, just give our support team a shout – we're here to help!
