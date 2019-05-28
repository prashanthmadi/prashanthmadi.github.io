---
layout: post
title: Installing native nodejs modules on Azure App Services during Git Deployment
date: '2017-02-10 19:01:13'
previewimg: '/content/images/2017/02/npm.png'
tags:
- npm
- nodejs
- azure
- webapps
- app-services
---

Azure Source Control deployment process would involve below steps
* Moves content to azure web app
* Creates default deployment script, if there is no .deployment file in web app root folder
* Run’s deployment script. In case of a nodejs app it would do npm install here

During `npm install` step, Most of the node modules mentioned in package.json are plain-text JavaScript files but few may require platform-specific binary images. These modules are compiled at install time, usually by using Python and node-gyp.

At this time, App Service has limited support for building native Node modules and you might end-up with an msbuild error.

There were some known issues with node-gyp and that have been fixed lately. Thanks to the Azure Customers feedback
https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6573329-support-for-node-gyp-in-nodejs-applications

In This blog, I would like to provide a workaround if you are still experiencing issues installing native modules

#### Manually copy content:

Run npm install on a Windows machine that has all the native module's prerequisites installed. Then, deploy the created node_modules folder as part of the application to Azure App Service.

Before compiling, check that your local Node.js installation has matching architecture and the version is as close as possible to the one used in Azure 

#### Automated Git Deployment:
Azure App Service can be configured to execute custom bash or shell scripts during deployment, giving you the opportunity to execute custom commands and precisely configure the way npm install is being run. I have provided documentation on this @ [Custom Deployment Script in Azure App Services](/azure-custom-deployment)

Instead of ignoring all the `node_modules` and pushing total content in node_modules, we would bundle the node modules which are failing and unzip them during Git Deployment using Custom Deployment Script.

Ex:
My Project's package.json file has bcrypt modules which is failing with below error
```
remote: gyp ERR! build error 
remote: gyp ERR! stack Error: `msbuild` failed with exit code: 1
remote: gyp ERR! stack     at ChildProcess.onExit (D:\\Program Files (x86)\\npm\\3.10.8\\node_modules\\npm\\node_modules\\node-gyp\\lib\\build.js:276:23)
remote: gyp ERR! stack     at emitTwo (events.js:106:13)
remote: gyp ERR! stack     at ChildProcess.emit (events.js:191:7)
remote: gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:215:12)
remote: gyp ERR! System Windows_NT 6.2.9200
remote: gyp ERR! command 'D:\\\\Program Files (x86)\\\\nodejs\\\\6.9.1\\\\node.exe' 'D:\\\\Program Files (x86)\\\\npm\\\\3.10.8\\\\node_modules\\\\npm\\\\node_modules\\\\node-gyp\\\\bin\\\\node-gyp.js' 'rebuild'
```

To resolve this issue,

* Remove bcrypt from package.json file
* In your Local computer, Create a new folder<br>
 `cd .. && mkdir failedpackages && cd failedpackages `
* Run below command to install bcrypt. <br>
 `npm install --arch=ia32 bcrypt@1.0.2`
```
Make sure that you have same version of nodejs in local as Azure web apps. I would recommend to use NVM - https://github.com/coreybutler/nvm-windows to quickly change nodejs versions on Local computer to match with that of Azure Web Apps.
```
* Above command would have created a `node_modules` folder with bcrypt and all other dependencies of it inside `node_modules` folder
* Zip Content inside `node_modules` folder and name it as `failedmodules.zip`
* Add `failedmodules.zip` to your app root folder
* Create [Custom Deployment Script]([link](/azure-custom-deployment) and add below content to unzip `failedmodules.zip` content into `node_modules` folder during deployment.
```
#4. Unzip failed node modules
if [ -e "$DEPLOYMENT_TARGET/failedmodules.zip" ]; then
  cd "$DEPLOYMENT_TARGET"
  eval unzip -o failedmodules.zip -d node_modules
  cd - > /dev/null
fi
```

Sample of deploy.sh with above content can be found at https://gist.github.com/prashanthmadi/c207ee03397b3d2195d721794e6eef6b

#### Troubleshoot

*How do I find which version of nodejs I'm using in Azure App Services*
https://prmadi.com/nodejs-npm-versions-azure-webaps/