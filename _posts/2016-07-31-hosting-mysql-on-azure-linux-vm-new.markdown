---
layout: post
title: Hosting MySQL on Azure Linux VM
date: '2016-07-31 17:15:08'
previewimg: '/content/images/2016/07/mysql.png'
tags:
- azure
- mysql
---

**MySQL** is the world’s most popular open source database, enabling the cost-effective delivery of reliable, high-performance and scalable Web-based and embedded database applications

There are different options to run MySQL on Azure

- ClearDB is a MySQL hosting service and manages the MySQL infrastructure for you.
- When you run your own MySQL cluster or database on an Azure Virtual Machine you have to set up the MySQL server and keep it updated with patches.

In this Blog, I would provide details on how to Setup Virtual Machine with MySQL installed on it. 

**Virtual Machine Setup :**

*   Navigate to Azure portal and create a new ubuntu virtual machine.

[![mysql1](https://msdnshared.blob.core.windows.net/media/2016/07/mysql1.png)](https://msdnshared.blob.core.windows.net/media/2016/07/mysql1.png)

*   If you are planning to use replication Next Blog, Create a new/Add to existing Availability set while creating VM.
*   After creating Virtual Machine, attach data disk to it

[![mysql2](https://msdnshared.blob.core.windows.net/media/2016/07/mysql2.png)](https://msdnshared.blob.core.windows.net/media/2016/07/mysql2.png) 
**Why i need to use data disk ?** 

To increase IOPS  

*   Login to your virtual machine via Putty/other tools using public IP address/DNS and username/password specified during creation of Virtual Machine

**Initialize Data Disk on Linux VM :**

*   Below link has details for how to initialize new data disk on VM
    *   [https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-classic-attach-disk/#initialize-a-new-data-disk-in-linux ](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-classic-attach-disk/#initialize-a-new-data-disk-in-linux)
*   After using the points provided in above link, you would end-up with a /datadrive which can use to store data in Data Disk

**Install MySQL Server on Data Disk :**

*   To give a proper directory structure, i have planned to install mysql in /datadrive/app/mysql
*   Create /datadrive/app  and /datadrive/app/mysql folder
*   Create a soft link between /datadrive/app/mysql and /var/lib/mysql. so that mysql would get installed in data disk

   `sudo ln -s /datadrive/app/mysql /var/lib/mysql`

*   Install Mysql server using below command

   `sudo apt-get install mysql-server`

**Testing :**

*   You should be able to login into mysql using below command

    `mysql -u root -p`
*   Enter password and mysql shell would be available

[![mysql3](https://msdnshared.blob.core.windows.net/media/2016/07/mysql3.png)](https://msdnshared.blob.core.windows.net/media/2016/07/mysql3.png)   