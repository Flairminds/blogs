---
title: Mount S3 Bucket On Linux EC2 Instance using S3FS
date: 2024-01-16
authors: [akashv]
slug: Mount-S3-Bucket-On-Linux-EC2-Instance-using-S3FS
description: >
  Guide to Mount S3 Bucket On Linux EC2 Instance using S3FS
categories:
  - DevOps
tags:
  - DevOps
  - S3
  - FSTAB
  - S3FS
---

# **Mount S3 Bucket On Linux EC2 Instance using S3FS**

## **Introduction**


S3fs is a FUSE file system that allows you to mount an Amazon S3 bucket as a local file system. It behaves like a network-attached drive, as it does not store anything on the Amazon EC2, but a user can access the data on S3 from the EC2 instance.

<!-- more -->

## **Prerequisites**

- S3 bucket (Private)
- EC2 Instance (Amazon Linux 2023 (AL2023))
- IAM User
- AWS CLI

## **Installation**

Connect to your EC2 Instance and then run below cmd to install all required tools to work with S2FS.
```bash
sudo yum update -y

sudo yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel -y

git clone https://github.com/s3fs-fuse/s3fs-fuse.git

cd s3fs-fuse
./autogen.sh
./configure --prefix=/usr --with-openssl
make
sudo make install
sudo yum install awscli -y
```

## **IAM (Identity and Access Management)**

Create an IAM user for s3fs with permission access to AmazonS3FullAccess.

Get the access key and secret key.

## **Configuration**

On your EC2 Instance, create a file named .passwd-s3fs and append your IAM Access Key and Secret Key to it.

```bash
echo <your access key ID>:<your secret key> > ${HOME}/.passwd-s3fs

chmod 0600 $HOME/.passwd-s3fs

mkdir /data/mongodb_backup

s3fs my-bucket-abdcefs /data/mongodb_backup
```

Use the following command to validate that the S3 Bucket has been mounted:

```bash
df -Th
```

Go to your S3 bucket, and upload a new file. Then, go to your EC2 and do `ls` in the same directory. The file that you just uploaded in your S3 bucket appears in your FileSystem.

## **Conclusion**

S3fs provides a convenient way to access and manage data stored in Amazon S3 by mounting it as a local file system. By following the steps outlined in this guide, you can easily install S3fs on your Amazon Linux 2023 system and mount an S3 bucket for optimal data management. This solution can streamline your data backup and archiving processes, as well as make it easier to share data between different systems. Give S3fs a try and take advantage of the benefits it provides for managing your data stored in Amazon S3.
