---
layout: post
title: Creating SSH public key on OSX for Azure VM
date: '2016-11-12 23:18:24'
previewimg: '/content/images/2016/11/password-less-ssh-login-to-your-linux-server-from-mac-osx_1474856410-b.jpg'
tags:
- linux
- ssh
---

open terminal and enter below command
```
ssh-keygen -t rsa
```
Follow prompt to provide passphrase and destination to store private, public keys.

It creates two files

* ssh_key
* ssh_key.pub

Use public key(*.pub content) to create Virtual Machine as in below link..

https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-quick-create-portal/

Login to machine using ssh_key file
```
ssh -i ssh_key prashanthmadi@104.210.151.66
```
Enter passphrase to finish login process...