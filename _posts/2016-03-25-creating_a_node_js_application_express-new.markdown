---
layout: post
title: Creating a NodeJs application (Express)
date: '2016-03-25 04:37:00'
previewimg: '/content/images/2017/04/express.jpg'
tags:
- nodejs
- express
---

In this blog i would like to explain how to create a sample NodeJs application. 

* Open command prompt and create a directory 
```
mkdir workspace
```
* Install express-generator module at global level, we would use this to create express(Node js web framework) templates. 
```
 npm install -g express-generator
```
* Use express cli to create template app. This would create all the required files for a sample app in existing folder. 
```
express .
```
* Install required Nodejs modules using following command. By doing this, it will install all the required modules present in package.json file. 
```
npm install
```
Use the below command to start app on local server and also make sure if template app is working on local environment. 
```
npm start
```
Navigate to http://localhost:3000 in your Browser. 

![Sample Express App](https://2.bp.blogspot.com/-H2lOZ5ErD-s/VvS_8Amn-ZI/AAAAAAAAABo/7WjCkj9FRGIVaDerMikfQGDf9mls4KuUQ/s320/Screen%2BShot%2B2016-03-24%2Bat%2B11.34.04%2BPM.png)