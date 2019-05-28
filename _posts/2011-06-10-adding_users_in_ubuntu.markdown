---
layout: post
title: adding users in ubuntu
date: '2011-06-10 06:06:00'
tags:
- linux
- ubuntu
---

sudo useradd -d /home/testuser -m testuser 

sudo passwd testuser 

make him sudoer my tweaking the following file 

/etc/sudoers 

when auto filling doesnt work using tab..... 

It is likely your default shell for adding users is Bourne shell, not bash. 

Look at /etc/defaults/useradd, and change: 

SHELL=/bin/sh 

to 

SHELL=/bin/bash 

So that future user adds will default to bash. 

For your current user, you should change their login shell to bash. 

chsh -s /bin/bash user_name