---
layout: post
title: installing mysql
date: '2011-06-10 03:27:00'
tags:
- sql
---

sudo apt-get install mysql-server 

sudo netstat -tap | grep mysql 
When you run this command, you should see the following line or something similar: 

tcp 0 0 localhost.localdomain:mysql *:* LISTEN - 
If the server is not running correctly, you can type the following command to start it: 

sudo /etc/init.d/mysql restart