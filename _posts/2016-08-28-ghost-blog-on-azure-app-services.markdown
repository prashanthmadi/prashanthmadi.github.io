---
layout: post
title: Ghost Blog on Azure App Services
date: '2016-08-28 05:40:15'
tags:
- nodejs
- ghost-tag
---

_Check my New blog for using Newer version of Ghost on Azure App Services(Linux). https://ourwayoflyf.com/ghost-v1-0-on-app-service-linux/_

**Ghost** is an open source publishing platform which is beautifully designed, easy to use, and free for everyone. It is written in `Javascript`, designed to simplify the process of online publishing for individual bloggers as well as online publications. 

Why Ghost ?

* You care about a well designed interface
* Your content needs to work well for social and search
* Speed and performance are important to you

You can find a comparison between Ghost vs Wordpress @ [link](https://ghost.org/vs/wordpress/)

#####Install Ghost on Azure App Services
* Navigate to azure portal - [portal.azure.com](https://portal.azure.com)
* Search for ghost in marketplace
![Ghost in Marketplace](/content/images/2016/08/Screen-Shot-2016-08-27-at-6-00-51-PM.png)
* Choose the option with **Web+Mobile** as Category.
* Click on Create option and provide required details to finish Install.
* Above step would download content from [Ghost-Azure Github](https://github.com/AzureWebApps/Ghost-Azure) and install it in Azure App services Web App

#####Ready for first use
* After install process, Navigate to your web app using `http://<Your_App_Name>.azurewebsites.net/`
* It may fail on the first attempt due to cold start but a refresh should bring the blog up and running.

#####Setup Ghost Admin
* Navigate to `https://<Your_App_Name>.azurewebsites.net/ghost/` for initial setup process.
* During the first visit, it would ask you to create a new account and the same would be marked as owner of existing Blog installation.
* You might try creating a sample post from admin dashboard and check if its available @  `http://<Your_App_Name>.azurewebsites.net/`

#####Change Theme
* We can find many pre-built themes available online with steps to use that particular theme.
* In my case, I have forked existing theme  and made changes to fit my needs [My Personal Blog Theme](https://github.com/prashanthmadi/Bastard)
* To use this, Copy theme folder inside `/content/themes` of Ghost Blog using FTP/drag-drop feature in Kudu Console.
* Restart Ghost and then go to Ghost's Settings `http://<Your_App_Name>.azurewebsites.net/ghost/settings/general/`. 
* Choose your new theme from the theme dropdown menu and save your changes.

#####Setup SMTP for sending Email's
Ghost Blog needs a SMTP server to send emails like any other web app. Azure Web App by default doesn't has a local smtp server in it. 

How do we send emails ?
We can use third-party service called **send-grid**. 

Using Send-grid :

* Navigate to azure portal - [portal.azure.com](https://portal.azure.com)
* Search for send grid in marketplace
![Ghost in Marketplace](/content/images/2016/08/Screen-Shot-2016-08-27-at-9-50-47-PM.png)
* Click on Create option and provide required details to finish Install. Make a note of `password` you have used.
* Navigate to send-grid account which you have just created and copy `username` from it.
* Add your send-grid config in Ghost Blog Web App App Settings.
```
emailService  -> SendGrid
emailUsername -> username from above step
emailPassword -> password from above step
```
Ex:
![Send Grid Details](/content/images/2016/08/Screen-Shot-2016-08-27-at-10-00-19-PM.png)


##### Use MySQL In-App/ClearDb instead of SqlLite
Ghost Blog by default would use SqlLite as database. If you prefer using MySQL database, follow below steps

I don't want to get into detail about MySQL offerings from azure in this blog. Below Link has details on how to create MySQL database in Azure.

* For MySQL In-App Feature refer - [Link](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/)
* For a database from ClearDb refer - [Link](https://azure.microsoft.com/en-us/documentation/articles/store-php-create-mysql-database/)

Add below lines of code in config.js file available @ `D:\home\site\wwwroot` for production/development based on your requirement.
```
database: {
    client: 'mysql',
    connection: {
        host: 'database_host_name',
        user: 'database_username',
        password: 'database_password',
        database: 'database_name',
        charset: 'utf8',
        // use below option for MySQL in-app
        // port: process.env.WEBSITE_MYSQL_PORT
    }
},
```
##### Create Backups
You can find info on how to set-up backups for Azure Web Apps at [link](https://azure.microsoft.com/en-us/documentation/articles/web-sites-backup/).


##### Upgrade Ghost Blog
You might find different guides on updating ghost blog online but the easiest way would be to use sync feature available in Azure portal - [portal.azure.com](https://portal.azure.com)
![Ghost Blog Update](/content/images/2016/08/Screen-Shot-2016-08-27-at-7-13-02-PM.png)

If your app doesn't work after update process. Check for Useful logs section in https://blogs.msdn.microsoft.com/azureossds/2015/08/19/debug-node-js-web-apps-on-azure/. It might help you debug the issue.

Recently i upgraded my ghost blog from 0.8 to 0.9 resulting in below error

    Cannot find module 'lodash/object/assign'
To fix above issue, i have navigated to `D:\home\site\wwwroot` in Kudu Console and entered below command to update node modules which fixed the issue

    >npm update

##### Using Custom Domain
Refer Below link to add custom Domain
https://azure.microsoft.com/en-us/documentation/articles/web-sites-custom-domain-name/