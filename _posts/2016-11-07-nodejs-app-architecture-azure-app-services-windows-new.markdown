---
layout: post
title: Nodejs App Architecture - Azure App Services
date: '2016-11-07 02:23:33'
previewimg: '/content/images/2016/11/iisnode.png'
tags:
- nodejs
- iisnode
---

**What is Nodejs ?**

* Server-side JavaScript environment
* Run’s on google V8 JS engine + libraries

**Why Nodejs ?**

* Never blocked on database/IO
* Rapid development
* Wealth of 3rd party packages(300,000+ on 11/6/16)
* When you need high levels of concurrency but little dedicated CPU time

Great for Streaming or event-based real-time app

* Web sockets(socket.io for chat apps)
* Editing documents online

**Node.js Books, Websites, Tutorials - [Link](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-node-js)**

####Web Apps (Windows)

In just a few steps you can build and deploy your Node.js app to Azure. I have blogged about it earlier at [link](https://blogs.msdn.microsoft.com/azureossds/2016/04/18/sample-nodejs-app-on-azure-app-services/)

In case of Azure App services(Windows), Below are list of steps it follows

1. As you can see in below screenshot, request hits one of the front-end server that navigates it to appropriate app instance(worker role).
2. After reaching Worker Role, it would use IIS server
3. IIS uses iisnode module to make named pipe connection with node.exe

![Nodejs Request Azure App Services Windows](/content/images/2016/11/node_arch.png)

#### Useful Links
* Deploy Sample Web APP [Link](https://blogs.msdn.microsoft.com/azureossds/2016/04/18/sample-nodejs-app-on-azure-app-services/)
* IISnode Configurration [Link](https://azure.microsoft.com/en-us/documentation/articles/app-service-web-nodejs-best-practices-and-troubleshoot-guide/#iisnode-configuration)
* Custom Deployment Script  [Link](/azure-custom-deployment)
* Nodejs/NPM Versions [Link](/nodejs-npm-versions-azure-webaps/)
* Debug Nodejs App  [Link](/debug-nodejs-app-in-azure-app-services-windows-2/)
* CPU Usage and Memory Leaks  [Link](             https://blogs.msdn.microsoft.com/azureossds/2015/08/23/finding-memory-leaks-and-cpu-usage-in-azure-node-js-web-app/)
* Best Practices   [Link](                              https://azure.microsoft.com/en-us/documentation/articles/app-service-web-nodejs-best-practices-and-troubleshoot-guide/ )
* Nodejs app performance tweaks [Link](/nodejs-app-performance-tweaks-azure-app-services-windows/ )
* Enable Browser Cache [Link](/enable-browser-cache-in-azure-web-apps-windows/)
* Installing Native Nodejs Modules [Link](/installing-native-nodejs-moduleson-azure-app-services-during-git-deployment)

#### Web Apps (Linux)

Azure has recently announced [Web Apps on Linux](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-intro). You can quickly create an app following [Link](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-how-to-create-a-web-app) and setup continuous deployment to publish the app.

In case of Azure App services(Linux), Below are list of steps it follows

![Nodejs Request Azure App Services Linux](/content/images/2017/12/appservice_linux_nodejs_arch.png)

1. As you can see in above screenshot, request hits one of the front-end server that navigates it to appropriate app instance(worker role).
2. Web Apps on Linux is built on top of Docker technology. So, you would be given two different containers(App and Kudu Container) per app sharing same storage volume.
3. Request would navigate to App container which uses PM2 to manager node.exe processes.
4. while Git deployment would utilize kudu container.

#### Related Links
* PM2 [Link](http://pm2.keymetrics.io/)
* Nodejs Docker Container [Link](https://hub.docker.com/r/appsvc/node/)