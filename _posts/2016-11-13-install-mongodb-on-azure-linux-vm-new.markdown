---
layout: post
title: Install mongodb on Azure Linux VM
date: '2016-11-13 04:45:36'
previewimg: '/content/images/2016/11/mongodb.jpeg'
tags:
- mongodb
---

Please Follow steps listed in my previous blog 
[Hosting MySQL on Azure Linux VM](/hosting-mysql-on-azure-linux-vm/) to create a Linux VM and attach data disk to it.

* Complete steps till **Initialize Data Disk on Linux VM**  at above blog link

####Installing Mongodb
* Import the public key used by the package management system.


```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```

* Create a list file for MongoDB.

```
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
```
* Reload local package database.
```
sudo apt-get update
```
* Install the MongoDB packages
```
sudo apt-get install -y mongodb-org
```


* To start mongodb service run `sudo systemctl start mongodb`
* To Check status run `sudo systemctl status mongodb`

####Troubleshoot
If you receive below error
```
Failed to start mongod.service: Unit mongod.service not found.
```
try `sudo apt-get install --reinstall mongodb`

Reference: 
https://docs.mongodb.com/v3.0/tutorial/install-mongodb-on-ubuntu/#install-mongodb

