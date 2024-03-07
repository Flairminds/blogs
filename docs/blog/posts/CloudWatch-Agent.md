---
title: Monitor Memory, Disk  Utilization of EC2 Instance with CloudWatch
date: 2024-03-06
authors: [akashv]
slug: Monitor-Memory-Disk-Utilization-of-EC2-Instance-with-CloudWatch
description: >
  Steps To Monitor Memory Utilization of EC2 Instance with CloudWatch
categories:
  - DevOps
tags:
  - DevOps
  - Monitoring
  - Memory-Disk-Utilization
  - CloudWatch
---

# Steps To Monitor Memory Utilization of EC2 Instance with CloudWatch

Monitoring system performance is crucial for maintaining optimal performance. Amazon Web Services (AWS) provides a powerful monitoring service called CloudWatch, which allows you to monitor various metrics of your EC2 instances, including CPU, memory, and disk utilization. In this blog post, we'll discuss how to set up monitoring for these metrics using CloudWatch.

<!-- more -->

## Prerequisites:

1. **IAM Role with “CloudWatchFullAccess”**
2. **Assign IAM Role to EC2 Instance**

## Installing CloudWatch Agent

First, log in to the EC2 instance, and download and install the CloudWatch agent.

```bash
sudo yum install amazon-cloudwatch-agent
```

After installing CloudWatch Agent, create `config.json` file at `/opt/aws/amazon-cloudwatch-agent/bin/config.json`

Enter the below text in the `config.json` file.

![Material Metrics  cloudwatch-Config][Material Metrics  cloudwatch-Config]

```json
{
	"metrics": {
		"append_dimensions": {
			"InstanceId": "${aws:InstanceId}"
		},
		"metrics_collected": {
			"mem": {
				"measurement": [
					"mem_used_percent"
				],
				"metrics_collection_interval": 60
			},
            "disk": {
				"measurement": [
                     "disk_used_percent"
				],
				"metrics_collection_interval": 60
			}
		}
	}
}
```

With the below command, we can start the CloudWatch Agent.

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

The above command output should be like below.

![Material Metrics  cloudwatch-stoped][Material Metrics  cloudwatch-stoped]

Then execute below command to run the CloudWatch Agent.

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a start
```

With the below command, we can check status of the CloudWatch Agent.

![Material Metrics  CWA-Status][Material Metrics  CWA-Status]

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
```

Verifying that the Amazon CloudWatch Agent is working involves checking if it's successfully collecting and sending metrics to CloudWatch.

1. Navigate to the CloudWatch service.
2. Go to the Metrics section.
3. You will get metrics of your instance.


## Conclusion:
Monitoring CPU, memory, and disk utilization is essential for maintaining the performance and health of your AWS infrastructure. By leveraging AWS CloudWatch, you can easily collect, visualize, and analyze these metrics, enabling you to make informed decisions and ensure optimal resource utilization. Follow the steps outlined in this blog post to configure monitoring for your EC2 instances and start harnessing the power of CloudWatch today!

## References:
- AWS CloudWatch Documentation: [https://docs.aws.amazon.com/cloudwatch/index.html](https://docs.aws.amazon.com/cloudwatch/index.html)
- AWS CloudWatch Agent Setup Guide: [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-first-instance.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-first-instance.html)
- AWS CloudWatch Alarms Guide: [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)



[Material Metrics  cloudwatch-Config]: cloudWatch-Agent/cloudwatch-Config.png
[Material Metrics  cloudwatch-stoped]: cloudWatch-Agent/cloudwatch-stoped.png
[Material Metrics  CWA-Status]: cloudWatch-Agent/CWA-Status.png
