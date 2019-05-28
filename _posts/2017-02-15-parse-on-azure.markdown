---
layout: post
title: Parse on Azure
date: '2017-02-15 02:34:45'
tags:
- parse
- azure
---

**Parse** is a Mobile Backend as a Service. On 28 January 2016, Facebook announced that it will close down Parse. Microsoft announced a Parse Server on Azure Managed Services, as an easy way for developers to migrate from the soon-to-be-defunct Facebook service.

Below link has details on how to create a Parse server on Azure.
https://azure.microsoft.com/en-us/blog/announcing-the-publication-of-parse-server-with-azure-managed-services/

In this Blog, I would provide an overview of Developing Web and Mobile Applications using parse server while developing a sample application.

After creating the app following instructions at above link

* To access Parse Dashboard, Navigate to below link and enter `username/password` from app service app settings `APP_ID/MASTER_KEY`
https://`<Your_APP_Name>`.azurewebsites.net/parse-dashboard

When you install a parse server from marketplace, It pulls the code from github and runs it on Azure App Services 

`Azure/parse-server-example` @ https://github.com/Azure/parse-server-example

Azure version of Parse Server would utilize below modules

* **parse-server-azure-push** :  To use Azure Notification Hub(send Push Notifications)
* **parse-server-azure-storage** : To use Azure Storage (Stores Images and other)
* **parse-server-azure-config** : Simplifies configuration of Parse Server on Azure Managed Services

I would create android/iOS app using react-native which uses parse-server hosted on Azure in below links.

1. Create React-Native Application and Connect Parse Server - [Link](/getting-started-with-react-native-app-and-parse) 
2. Send Push Notifications from Parse Server - (Coming soon)
