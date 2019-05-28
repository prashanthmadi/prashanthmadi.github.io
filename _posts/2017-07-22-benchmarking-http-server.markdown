---
layout: post
title: Benchmarking HTTP Server
date: '2017-07-22 21:16:41'
tags:
- apache-benchmarking
- tools
- http-benchmarking
---

Most engineers rarely perform HTTP Server Benchmarking before moving app to production and realize that their app is performing very slow after few months(under heavy load).
![surprise](/content/images/2017/07/surprise.gif)

In this blog, i would like to provide ways to do Benchmarking so that you can find bottlenecks in early stages and reduce the impact.  

My Web App uses an api that has dependency on redis cache which returns very big string 293566 chars( > 270kb)

![](/content/images/2017/07/app.png)

I have setup a repro @ https://prwebapptest.azurewebsites.net/ to test these tools. If i hit my url in normal scenario it returns in 500ms even with big string but takes longer when there is heavy load.

#### Apache Benchmarking : 
Details about it can be found @ [url](https://httpd.apache.org/docs/2.4/programs/ab.html)

_Test: 1000 concurrent requests for 20,000 requests_

- When my endpoint returns this big string, below are the stats using apache benchmark tool with mean of 7 seconds
![](/content/images/2017/07/1.jpg)

- Here is another test with request making redis call with large data but return only "hello world" from webapp. This decreased mean time to 4 seconds
![](/content/images/2017/07/2.jpg)

- Later, I changed content in my redis cache to small string(17 chars) and mean response is 724ms .
![](/content/images/2017/07/3.jpg)

So, definitely issue is due to the fact that it returns too much of data and its taking this extra time to write content to socket.

Later in the day, I had a chance to work with Azure Redis Team.
They have provided me below link which has best practices for azure redis.
https://gist.github.com/JonCole/925630df72be1351b21440625ff2671f#best-practices-for-azure-redis 

Check for point 6 in Configuration and Concepts
-	Redis works best with smaller values, so consider chopping up bigger data into multiple keys. In this Redis discussion, 100kb is considered "large". Read this article for an example problem that can be caused by large values

Solution : I had to reduce data transferred per url request and use pagination concept in my android app. 

#### Load test with the Azure portal :

If you have a azure subscription, [Link](https://www.visualstudio.com/en-us/docs/test/performance-testing/app-service-web-app-performance-test) has detailed steps to perform load testing in Azure.

#### loadtest nodejs module :
Details about it can be found at [url](https://www.npmjs.com/package/loadtest)

I have tried running this tool from my Azure Linux VM and also Desktop. I felt that your internet connection and others would cause unnecessary noise.   
![](/content/images/2017/07/4.jpg)