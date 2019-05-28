---
layout: post
title: Ghost v1.x on Azure App Service Linux
featured: true
date: '2017-08-29 03:03:04'
tags:
- ghost-tag
- azure
- app-services
- linux
- docker
- dockerhub
---

Ghost v1.0 was announced in July 2017. You can find more info about it @ https://blog.ghost.org/1-0/. In this blog, I would like to provide steps for running Ghost v1.x blog on App Service Linux.

*Check my previous blog for using older version of Ghost on Azure App Services(windows). https://prmadi.com/ghost-blog-on-azure-app-services/*

Azure App Service is a PAAS solution to run Enterprise-grade Web Applications. Azure has recently announced [App Services on Linux](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-intro). It supports running web apps natively on Linux using Docker Technology.

Below is an Architecture of how a request flows through

![Ghost Blog Architecture](/content/images/2017/08/Ghost_blog_architecture-1.png)

As you can see in above screenshot, each app would have two different containers and a persistent storage between them
* App Container  (Your Application runs in this)
* Kudu Container (Used mainly for tooling purpose like Continuous Deployment)

We would store all our Ghost_Content and log files inside /home folder as anything else would be lost after app restart

You can find Ghost Docker Image details used in this blog at below links
Github Link : https://github.com/prashanthmadi/azure-ghost
Docker Hub : https://hub.docker.com/r/prashanthmadi/azure-ghost/

Feel free to open issues @ https://github.com/prashanthmadi/azure-ghost/issues or Fork the repo to fit your needs.

## Installation Steps
* Click on below button and it would navigate you to azure portal
[![Azure Deploy](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fprashanthmadi%2fazure-ghost%2fmaster%2fazuredeploy.json)

* Enter required details in form. It would create **Azure Database for MySQL** and **Web App** with Ghost blog installed in it.
* Navigate to your newly created webapp in portal and click on Browse
* First request would take little longer and might fail if it takes > 240 sec. Subsequent requests should be faster.

### Why is my first request slow ?
During first request, we would run `docker run` command that would pull image from Dockerhub and executes [init-container.sh](https://github.com/prashanthmadi/azure-ghost/blob/master/init-container.sh) script
* init-container.sh would copy ghost_content folder to /home/site/wwwroot and runs database migration using knex. This part happens only once and for subsequent app restart it would spend time only for `docker run` command. Check [migrate_util.sh](https://github.com/prashanthmadi/azure-ghost/blob/master/migrate_util.sh) to understand logic involved.


### Configuration
There are mutliple ways to configure Ghost application but recommended approach is to use ghost-cli. At the end, All approaches would boil down to `config.production.json` file in `/var/lib/ghost` folder. We are setting common config values using app settings provided in webapp via ghost-cli. Below is my blog config file
```
{
  "url": "http://ourwayoflyf.com/",
  "server": {
    "port": 2368,
    "host": "0.0.0.0"
  },
  "database": {
    "client": "mysql",
    "connection": {
      "host": "XXXXXXX.mysql.database.azure.com",
      "user": "XXXXXXX@XXXXXXX",
      "password": "XXXXXXX",
      "database": "XXXXXXX"
    }
  },
  "mail": {
      "transport": "Direct"
  },
  "logging": {
    "transports": [
      "file",
      "stdout"
    ]
  },
  "process": "systemd",
  "paths": {
    "contentPath": "/home/site/wwwroot"
  }
}
```
If you want to add extra config, create a `config.production.json` folder in `/home/site` folder. I have added logic in [migrate_util.sh](https://github.com/prashanthmadi/azure-ghost/blob/master/migrate_util.sh) to copy `config.production.json` in `/home/site` to `/var/lib/ghost` if it exists before runing the app.

**Note:** You might have to use ftp clients like filezilla to modify `config.production.json` file in `/home/site` folder

### Mail Config
There are multiple mail services. You can find related doucmentation at below link
https://docs.ghost.org/docs/mail-config

Here is how i have added Sendgrid for my blog
* Create a sendgrid account in Azure Portal
* Make a note of username and password
* You can use web-ssh available in kudu container to access app container and copy `config.production.json` file in /var/lib/ghost to /home/site folder
* Replace mail config in `/home/site/config.production.json` with below content to use Sendgrid.
* Change from, user and pass details as per your requirement.
```
  "mail": {
    "transport": "SMTP",
    "options": {
      "from": "XXXXXXX@gmail.com",
      "service": "SendGrid",
      "auth": {
        "user": "azure_XXXXXXX@azure.com",
        "pass": "XXXXXXX"
      }
    }
  },
```


### Migrating from older Version of Ghost to 1.X
Below link has required info on it
https://docs.ghost.org/v1.0.0/docs/migrating-to-ghost-1-0-0#section-4-copy-your-images

### Backup web app and MySQL Database
https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-backup

### Map an existing custom DNS name to Azure Web Apps
https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-domain

After mapping custom domain, make sure to update your app setting to use new custom domain else all url's inside app would redirect to old url.
![domainchange](/content/images/2017/09/domainchange.PNG)

### Upgrade Ghost

You can find available Ghost versions at below link
https://hub.docker.com/r/prashanthmadi/azure-ghost/tags/

I have seen many users complaining about knex-migrator issue while upgrading their ghost version.

Navigate to `/var/lib/ghost` folder via webssh in App Container
https://`Your_APP_Name`.scm.azurewebsites.net/webssh/host

Run below command
```
ghost update
```

Even though you have updated your container for now.. An app restart might take it back to older version of ghost.So make sure to change tag of your docker image in Azure portal as below to upgrade after running `ghost update`

Example: I changed below highlighted content from 1.7 to 1.8
![upgradeghost](/content/images/2017/09/upgradeghost.PNG)

### Troubleshoot
* `/home/LogFiles/xxx_docker.log` files has docker run command and init_script output
* `/home/site/wwwroot/logs/*` contains ghost application standard out/err logs




Special Thanks to [Srikanth Sureddy](https://github.com/sureddy1) for his contributions to Ghost image and helping me with Linux queries.