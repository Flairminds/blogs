---
title: Enforcing Mandatory Tags for Azure Resources using Azure Policy
date: 2024-03-26
authors: [atharvab]
slug: Enforcing-Mandatory-Tags-for-Azure-Resources-using-Azure-Policy
description: >
  Enforcing Mandatory Tags for Azure Resources using Azure Policy
categories:
  - DevOps
tags:
  - DevOps
  - Azure
  - Policy
comments: true
---

### Introduction

As organizations expand their operations in the cloud, managing resources efficiently becomes crucial. One effective strategy is enforcing the use of mandatory tags for Azure resources. Tags provide metadata that can be used for resource organization, cost tracking, and access control. This blog post will guide you through implementing a policy in Azure Resource Manager to enforce mandatory tags for resource groups.

<!-- more -->

### Prerequisites

Before you begin, ensure you have:

- An Azure subscription
- Permission to create and assign policies in Azure Policy

### Creating Policy

To enforce mandatory tags for Azure resources, follow these steps:

1. **Sign in to the Azure portal:** Go to [portal.azure.com](https://portal.azure.com) and sign in to your Azure account.

2. **Navigate to Azure Policy:** In the Azure portal, search for and select "Policy" from the services list.

3. **Create a new policy definition:** Click on "Definitions" under the "Authoring" section and then click on "Add definition".

4. **Enter the policy definition:** Copy and paste the following policy definition JSON into the policy definition editor:

    ```json
    {
      "mode": "All",
      "policyRule": {
        "if": {
          "allOf": [
            {
              "field": "type",
              "equals": "Microsoft.Resources/subscriptions/resourceGroups"
            },
            {
              "allOf": [
                {
                  "field": "[concat('tags[', 'business-criticality', ']')]",
                  "exists": "false"
                },
                {
                  "field": "[concat('tags[', 'environment-type', ']')]",
                  "exists": "false"
                },
                {
                  "field": "[concat('tags[', 'managedby', ']')]",
                  "exists": "false"
                },
                {
                  "field": "[concat('tags[', 'product', ']')]",
                  "exists": "false"
                },
                {
                  "field": "[concat('tags[', 'start-date', ']')]",
                  "exists": "false"
                },
                {
                  "field": "[concat('tags[', 'team', ']')]",
                  "exists": "false"
                }
              ]
            }
          ]
        },
        "then": {
          "effect": "deny"
        }
      },
      "parameters": {}
    }
    ```

5. **Review and create the policy definition:** Review the policy definition to ensure it meets your requirements and then click on "Review + create" to create the policy definition.

6. **Assign the policy definition:** After creating the policy definition, assign it to the desired scope (e.g., subscription, resource group).

7. **Verify the policy:** Once the policy is assigned, Azure Policy will enforce the tag requirements. Any resources that do not comply with the policy will be denied.

## Understanding the Policy Definition
The policy definition provided is a JSON object that defines the conditions under which resources are allowed or denied. Let's break down the key components:

- Mode: The mode specifies whether the policy is applied to all resources (All) or only new resources (Indexed).

- Policy Rule: The if section defines the conditions that must be met for the policy to apply. In this case, it checks if the resource type is a subscription or a resource group and if certain tags are missing.

- Parameters: This section allows you to define parameters that can be used in the policy rule. In this example, there are no parameters defined.

### Conclusion

Enforcing mandatory tags for Azure resources using Azure Policy helps organizations maintain consistency, improve resource management, and streamline operations. By implementing this policy, you can ensure that all resources in your Azure environment have the necessary tags, enabling better organization and governance.

### References

- [Azure Policy documentation](https://docs.microsoft.com/en-us/azure/governance/policy/overview)
- [Azure Resource Manager documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
- [Azure Tags documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)