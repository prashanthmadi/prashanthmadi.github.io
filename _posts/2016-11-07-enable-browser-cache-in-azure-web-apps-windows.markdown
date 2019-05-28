---
layout: post
title: Enable Browser Cache in Azure App Services(windows)
date: '2016-11-07 01:00:10'
tags:
- nodejs
- iis
---

The **browser cache** is a temporary storage location on your computer for files downloaded by your browser to display websites. Files that are cached locally include any documents that make up a website, such as html files, CSS style sheets, JavaScript scripts, as well as graphic images and other multimedia content.

Azure web apps use IIS as server and you can Add below content in `web.config` file to set the cache-control for static files in any app.
```
<staticContent>
 <!-- Set expire headers to 30 days for static content-->
 <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="30.00:00:00" />
</staticContent>
```
**web.config screenshot :**
![web.config sample](/content/images/2016/11/webconfig.jpg)

**Browser screenshot With above Config:**
![Browser Cache Output](/content/images/2016/11/browser_screenshot.jpg)



####Node.js
If you still insist in setting **max-age** at express app level, below details may help you

* Make sure to remove static content rule in web.config file
* Make sure that your static url's are hitting node.exe and remove any static content rewrite rule in web.config
```
<rule name="StaticContent">
  <action type="Rewrite" url="public{REQUEST_URI}"/>
</rule>
```
* Use below code
```
var cacheTime = 86400000*7; 
app.use(express.static(path.join(__dirname, 'public'),{ maxAge: cacheTime }));
```
**Browser Screenshot with above Config :**
![Browser Cache Output](/content/images/2016/11/browser_screenshot2.jpg)
