---
title: Creating an AWS WAF IP Set and Associating it with an ALB
date: 2024-01-11
authors: [amanw]
slug: Creating-an-AWS-WAF-IP-Set-and-Associating-it-with-an-ALB
description: >
  Guide to Creating an AWS WAF IP Set and Associating it with an ALB
categories:
  - DevOps
tags:
  - DevOps
  - WAF
  - Security
  - ALB
  - WEB ACL
  - API Gateway
comments: true
---

## Feature and Cost for API gateway and ALB with Web ACL

This document offers a brief yet insightful overview of two critical AWS services: Amazon API Gateway and ALB with Web ACL. We'll explore the key features that enhance API management and web traffic control, coupled with a concise cost analysis for informed decision-making.

<!-- more -->

**API Gateway:**

*Feature:*

1. **Fully Managed Operations:**
   - Simplifies API publishing, maintenance, and scaling.
   - Pay-as-you-go model for secure and reliable API operations.

2. **Versatile API Creation:**
   - Quick creation and deployment of custom APIs linked to AWS services or external HTTP endpoints.
   - User-friendly console for resource, method, and SDK management.

3. **Efficient Monitoring and Resiliency:**
   - Real-time API performance monitoring through integrated dashboard and CloudWatch.
   - Traffic management features like throttling rules and caching for backend system efficiency.

4. **Rate Limiting for Traffic Control:**
   - Implement rate limiting rules to control requests per second for each API method.
   - Ensures optimal traffic management and prevents abuse.

*Cost:*

- **Number of Requests (per month):**
  - First 300 million: $1.05 per million
  - 300+ million: $0.95 per million

<br>

**ALB with Web ACL:**

*Feature:*

1. **Precise Control with Scope-Down Statements:**
   - AWS WAF allows scope-down statements for rate-based rules.
   - Enables precise control over requests for aggregation, counting, and rate limiting.

2. **Dynamic Rate Limiting Criteria:**
   - Rate-based rule actions based on criteria like scope-down statements and exceeding specified request counts.
   - Ensures effective rate limiting.

3. **Efficient Algorithm for Request Rates:**
   - AWS WAF uses an efficient algorithm for estimating request rates, refreshing approximately every 30 seconds.
   - Effectively controls high request rates with a focus on recent requests.

4. **Versatile Rule Actions:**
   - Rate-based rules offer versatile actions like blocking, counting, CAPTCHA, or Challenge responses.
   - Provides flexibility in handling requests exceeding defined rate limits.

*Cost:*

- **Resource Type:**
  - Web ACL: $5.00 per month (prorated hourly)
  - Rule: $1.00 per month (prorated hourly)
  - Request: $0.60 per 1 million requests (for inspection up to 1500 WCUs and default body size*)
  
- **Bot Control and Fraud Control:**
  - Additional cost as per tabs above.