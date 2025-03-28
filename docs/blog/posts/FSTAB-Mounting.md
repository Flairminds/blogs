---
title: Use FSTAB To Auto-mount partition In Ubuntu 
date: 2024-02-23
authors: [akashv]
slug: Use-FSTAB-TO-Auto-mount-partition-In-Ubuntu 
description: >
  Guide Congiguration of FSTAB to Auto-mount partition at the time of boot.
categories:
  - DevOps
tags:
  - DevOps
  - S3
  - FSTAB
  - FSTAB-FILE
---

# **FSTAB Mounting**

[Material FSTAB lsblk]: FSTAB_Mounting/lsblk.png
[Material FSTAB fils-s-dev-nvm1]: FSTAB_Mounting/fils-s-dev-nvm1.png
[Material FSTAB vi_etc-fstab]: FSTAB_Mounting/vi_etc-fstab.png


When we connect an external drive, by default, Linux OS (or Ubuntu Server) doesn't automount the external drive at startup. We can mount it very easily using the mount command but we want to enable automount feature on startup. So, we don't need to mount the drive again after restarting or logging into Linux OS. 

<!-- more -->

The **fstab** stands for File System Table. It's a system configuration file on Unix and Unix-like operating systems, including Ubuntu, that maintains a table of filesystems and their associated mount points. This file is located at */etc/fstab*.

## **Using lsblk to Identify Filesystems:**

To find all filesystems that are mounted or free, you can use the `lsblk` command. It will give you a list of all filesystems. Identify your filesystem and copy the name of that filesystem.

```bash
lsblk
```
![Material FSTAB lsblk][Material FSTAB lsblk]


Additionally, you need to determine the type of filesystem, such as ext4, xfs, etc. To find the filesystem type, you can use either of the following commands:

```bash
lsblk -f
```

or

```bash
file -s /dev/your_filesystem_name
```
![Material FSTAB fils-s-dev-nvm1][Material FSTAB fils-s-dev-nvm1]

## **Editing the FSTAB File:**

Once you have gathered the necessary information, edit the FSTAB file using a text editor such as Vim:

```bash
vim /etc/fstab
```
![Material FSTAB vi_etc-fstab][Material FSTAB vi_etc-fstab]

Here's a typical line from an fstab file:

```bash
UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX    /mnt/mydisk      ext4    defaults    0    2
```

or

```bash
/dev/nvme1n1   /home/ubuntu/backups    xfs    defaults   0   2
```

- **UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX**: This specifies the UUID of the filesystem.
- **/mnt/mydisk** or **/home/ubuntu/backups**: This is the mount point, the directory where the filesystem will be attached.
- **ext4** or **xfs**: This is the filesystem type.
- **defaults**: This is a list of default mount options.
- **0**: This indicates the dump frequency. Usually, it's set to 0, which means it won't be backed up by the dump utility.
- **2**: This indicates the order in which fsck should check filesystems. 0 or 1 means it won't be checked, and 2 or 3 means it will.

## **Adding Entries to FSTAB:**

Add your filesystem, mountpoint, filetype, and other options in the fstab file and save the file.

## **Verifying Mount Success:**

To verify that the filesystem is mounted successfully, use the following command:

```bash
mount -a
```

If this command does not give any errors, then there are no errors in the fstab file.

You can also check if the filesystem is mounted successfully again using `lsblk`.

## **Restarting for Verification:**

To ensure the changes take effect, verify by restarting your machine.

## **Important Note:**

Modifying fstab requires root privileges, and any incorrect entries can potentially prevent the system from booting properly. Therefore, it's crucial to be careful when editing this file.