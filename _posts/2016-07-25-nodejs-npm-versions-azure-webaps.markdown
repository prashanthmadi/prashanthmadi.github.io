---
layout: post
title: NodeJs and NPM versions on Azure App Services
date: '2016-07-25 01:44:40'
tags:
- azure
- nodejs
- webapps
---

**NodeJs** is a JavaScript runtime built on Chrome's V8 JavaScript engine. NodeJs uses an event-driven, non-blocking I/O model that makes it lightweight and efficient 

**NPM** is the package manager for JavaScript. 

How to find the nodejs version's that azure web app supports

*   Navigate to kudu console (`https://<sitename>.scm.azurewebsites.net`) and click cmd in Debug Console
*   Click on disk image and navigate to D:\Program Files (x86)\nodejs
*   You would see all the available versions

**NodeJs Version on Azure Apps** 

There are two ways of setting NodeJs version in azure web Apps

*   Using iisnode.yml (this wont change node version on kudu cli or during deployment)
*   Using App Setting in Azure portal

Note : iisnode.yml would overwrite App Setting if it exists. 

**NPM Version** 

NPM version corresponds to the NodeJs version you have set in web app as above.  You do not need to worry about setting the npm version as the version of node you selected (see below) will use the correct npm version.

*   Node 0.12.2  would use npm 2.7.4
*   Node 0.10.32 would use npm 1.4.28

**Changing NodeJs Version :** 

1\. Using App Setting

*   Navigate to your web app in azure portal
*   Click on Application settings in Settings blade.
*   You can include WEBSITE\_NODE\_DEFAULT\_VERSION as key and  version of nodejs you want as value in app settings.

[![Screen Shot 2016-04-20 at 10.32.35 AM](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.32.35-AM-1024x600.png)](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.32.35-AM.png)

*   Navigate to kudu console (`https://<sitename>.scm.azurewebsites.net`) and you can check the nodejs version using below command
    *   node -v

[![Screen Shot 2016-04-20 at 10.33.56 AM](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.33.56-AM-300x82.png)](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.33.56-AM.png) [![Screen Shot 2016-04-20 at 10.37.16 AM](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.37.16-AM-300x100.png)](https://msdnshared.blob.core.windows.net/media/2016/04/Screen-Shot-2016-04-20-at-10.37.16-AM.png) 

2\. Using iisnode.yml file 

As i have mentioned earlier, changing nodejs version in iisnode.yml file would only set the run-time environment which iisnode uses. your kudu cmd and others would still use nodejs version set at app settings. 

-Setting iisnode.yml file manually

*   Create a iisnode.yml file in your app root folder and include below line

[![iisnode](https://msdnshared.blob.core.windows.net/media/2016/04/iisnode-300x258.png)](https://msdnshared.blob.core.windows.net/media/2016/04/iisnode.png)

    nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"


-Setting iisnode.yml file using package.json during source control deployment 
Azure Source Control deployment process would involve below steps

1.  Moves content to azure web app
2.  Creates default deployment script, if there isn’t one(deploy.cmd, .deployment files) in web app root folder
3.  Run’s deployment script where it creates iisnode.yml file if we mention nodejs version in package.json file > engine
```
"engines": {
"node": "5.9.1",
"npm": "3.7.3"
}
```

iisnode.yml would have below line of code

    nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"

**Changing NPM Version**

*   Changing NodeJs version would automatically change NPM version
*   If you include npm version in package.json file, that would be used during deployment with source control

```
"engines": {
"node": "5.9.1",
"npm": "3.7.3"
}
```

**Using Custom Nodejs Version**

Azure App services already has most of the NodeJs versions and the list is constantly updated. If you want to use custom NodeJs version follow below steps

* Download your choice of NodeJs version from https://nodejs.org/en/download/releases/
* While writing this blog, App service doesn't has NodeJs v4.5
* I have clicked download option at above mentioned link and downloaded "node-v4.5.0-win-x86.zip" from
https://nodejs.org/download/release/v4.5.0/
* Move unzipped content to Azure App service
![Custom NodeJs Version to App service](/content/images/2016/09/Screen-Shot-2016-09-09-at-3-28-33-PM.png)
* Create iisnode.yml file and add below line
```
nodeProcessCommandLine: "D:\home\site\wwwroot\node-v4.5.0-win-x86\node.exe"
```
Above folder name may change depending on your custom NodeJs version

Output:
![App service using custom NodeJs version](/content/images/2016/09/Screen-Shot-2016-09-09-at-3-32-49-PM.png)


####WebApps on Linux

* Changing nodejs version with  engines in package.json or `WEBSITE_NODE_DEFAULT_VERSION` would change nodejs version during git deployment.
* kudu cli would still stay at node v4.5 after above changes
* To change nodejs version in app container, we need to use dropdown available in portal
