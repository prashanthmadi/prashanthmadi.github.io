---
layout: post
title: Running Sails.js app in Azure App Service Linux with Continuous Deployment
date: '2018-07-22 06:23:01'
previewimg: 'https://prmadi.com/content/images/2018/07/installations.png'
---

Sails makes it easy to build custom, enterprise-grade Node.js apps. Sails is 100% javascript.

**Pre-Reqs**
- VS code
- Node.js installed on your machine

Create sample sails.js local app following below steps
```
npm -g install sails
sails new app
cd app
sails lift
```
![1](/content/images/2018/07/1.PNG)

If you open app folder in VS code. It should look like below

![3](/content/images/2018/07/3.PNG)

Output:

![2](/content/images/2018/07/2.PNG)

**Create Web App Linux in Azure portal**
****
 ![5](/content/images/2018/07/5.PNG)
 
 Push your code to github
 ```
 git init
 git remote add origin <git url>
 git add .
 git commit -m "some message"
 git push origin master
 ```
Enable Deployment options in portal. In this blog i did selected Github, choose the repo and save the changes.
 
 Check for Deployment logs if it fails.
 
 ![6](/content/images/2018/07/6.PNG)
 
 App published on Azure.
 
 ![4](/content/images/2018/07/4.PNG)
 
 **Few errors i faced after pushing code to Azure**
 ```
 SyntaxError: Unexpected token function - Async function
 ```
 As Async functions are not supported in Node versions older than 7.6
 I updated Node version to 10.1 in Application settings.
 
 ![7](/content/images/2018/07/7.PNG)
 
 Also include onlyAlloworigins in  config --> env --> production.js 
 
 ![8](/content/images/2018/07/8.PNG)
