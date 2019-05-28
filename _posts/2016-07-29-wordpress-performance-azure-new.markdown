---
layout: post
title: Improving Wordpress Performance on Azure Web Apps
featured: true
previewimg: '/content/images/2016/07/fimg2.jpg'
date: '2016-07-29 19:22:09'
tags:
- wordpress
- azure
---

**WordPress** is web software you can use to create a beautiful website, blog, or app. It is a [free and open-source](https://en.wikipedia.org/wiki/Free_and_open-source_software "Free and open-source software") [content management system](https://en.wikipedia.org/wiki/Content_management_system "Content management system") (CMS) based on [PHP](https://en.wikipedia.org/wiki/PHP "PHP") and [MySQL](https://en.wikipedia.org/wiki/MySQL "MySQL") 

The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives. You can find more info on how to create WordPress app @ [Link](https://azure.microsoft.com/en-us/documentation/articles/app-service-web-create-web-app-from-marketplace/ "WordPress on Azure") 

Whether you run a high traffic WordPress installation or a small blog on a low cost shared host, you should optimize WordPress and your server to run as efficiently as possible. Although there are different blogs available online, this article would provide step-by-step procedure on how to fix WordPress performance issues in Azure specifically.   

**How a WordPress installation on Azure web apps is different from other providers/ why is it slow ?** - Azure web apps use a remote storage disk to store all the deployed code. When a request comes in, it would hit your web app machine which in-turn has to bring the code from remote storage into web app machine for execution. These remote storage calls add some network latency causing app to be slower than expected. Below diagram may help you understand this scenario [![3](https://msdnshared.blob.core.windows.net/media/2016/05/311.jpg)](https://msdnshared.blob.core.windows.net/media/2016/05/311.jpg) As you can see in above picture, Deployed code would be stored in a remote storage and required files are accessed from it on-demand basis by web app machines. 

**Is there a workaround for reducing network latency between storage and web app machine ?** Yes, Using local cache but it changes how you operate web app. More info can be found @ [https://azure.microsoft.com/en-us/documentation/articles/app-service-local-cache/](https://azure.microsoft.com/en-us/documentation/articles/app-service-local-cache/ "Local cache")

**Troubleshoot :** First look at the Browser developer tools and check where its spending the time

1.  First Request (or)
2.  Static files

[![1](https://msdnshared.blob.core.windows.net/media/2016/05/134-1024x339.png)](https://msdnshared.blob.core.windows.net/media/2016/05/134.png) 

If it is on **First Request** (where it brings html content). Follow below list of steps 

**Enable super cache**

*   Navigate to your WordPress admin portal ex : http://Your_WebApp_Name.azurewebsites.net/wp-admin
*   Click on Add New in plugins at the left nav

[![Screen Shot 2016-05-13 at 8.32.36 PM](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.32.36-PM-1024x516.png)](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.32.36-PM.png)

*   Search for super cache and click on install
*   Activate the plugin

![Screen Shot 2016-05-13 at 8.35.33 PM](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.35.33-PM-1024x405.png)

*   Click on Wp super cache settings in plugins tab

[![Screen Shot 2016-05-13 at 8.41.47 PM](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.41.47-PM-1024x845.png)](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.41.47-PM.png)

*   Check if Caching is turned-on and update status accordingly

[![Screen Shot 2016-05-13 at 8.42.38 PM](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.42.38-PM-1024x458.png)](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.42.38-PM.png)

*   Navigate to your web app in browser and you should see decrease in TTFB from second request. As you can see in below screenshot, same app took minute amount of time after enabling super cache.

[![2](https://msdnshared.blob.core.windows.net/media/2016/05/226-1024x321.png)](https://msdnshared.blob.core.windows.net/media/2016/05/226.png) 

**Disable Plugins**

*   If your app is still slow after enabling super cache, Try disabling all the existing plugins and check if there is any fault plugin affecting overall app performance
*   We have seen few plugins which are having negative affect on app performance. These plugins mostly rely on database operations to store/retrieve data.
* Add wincache.reroute_enable=1 to the .user.ini   

If the slowness is due to **Static files**, 

* Try to reduce number of requests made by your app for static files. When you navigate to a url on browser, it makes >1 requests internally for getting dependent content(it could be images, JavaScript or other files). Ex: Below is an app which makes 145 static url requests for loading index page. As you can see, It took almost 9 sec to load its page while a minimal amount of time spent in retrieving html content after enabling super cache. [![5](https://msdnshared.blob.core.windows.net/media/2016/05/513-1024x465.png)](https://msdnshared.blob.core.windows.net/media/2016/05/513.png) 

In case of Azure web apps, It uses IIS Server which receives request and forwards to PHP process for response. If IIS is busy processing other requests/cannot create a new process it would build a queue and a new request would wait in queue to get processed. For a WordPress app, we generally see number of static file requests ranging(100-140). It's quite natural that response time would increase as requests would wait in queue to get processed over the time. [![6](https://msdnshared.blob.core.windows.net/media/2016/05/615-1024x433.png)](https://msdnshared.blob.core.windows.net/media/2016/05/615.png) 
Above is a request stack of an app in normal condition vs under load. As you can see in above screenshot, queue size has increased and it took 113sec to just assign a PHP process.   

**High Traffic Apps** - Enable CDN (making it someone else problem)

*   Below url has details on how to create a CDN Profile and an end point.
    *   More Info : [https://azure.microsoft.com/en-us/documentation/articles/cdn-create-new-endpoint/](https://azure.microsoft.com/en-us/documentation/articles/cdn-create-new-endpoint/ "Azure CDN")
*   At the end of above step you would receive a CDN url : `https://<Your_CDN_NAME>.azureedge.net/`
*   Wait for 30-40 sec for web app content to get propagated into CDN servers
*   There are different plugins to enable CDN. Since we have already installed super cache in earlier step, Lets use that
*   Super Cache has in-built functionality to enable CDN, navigate to admin portal
*   Click on WP super cache settings in plugins tab

[![Screen Shot 2016-05-13 at 8.41.47 PM](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.41.47-PM-1024x845.png)](https://msdnshared.blob.core.windows.net/media/2016/05/Screen-Shot-2016-05-13-at-8.41.47-PM.png)

*   Click on CDN
*   Enter CDN url

**Low Traffic Apps** 

Although using CDN is a good way to solve static files latency issue. Many of small vendors are less likely to utilize this feature due to added cost. Below tips may help you -  Process static files at IIS level, All static files follow below mapping _url hits IIS ->  forwards request to PHP/wordpress -> response is fetched_

*   IIS uses web.config file to configure server settings. This would be available at web app root folder in kudu console(https://Your_APP_Name.scm.azurewebsites.net)
*   Enter Below rewrite rule and all the url's are served at IIS level instead of forwarding it to PHP process
*   This would help reduce fight for PHP processes.

     <!-- consider whether the incoming URL matches a physical file in the /public folder -->
     <rule name="StaticContent">
       <action type="Rewrite" url="public{REQUEST_URI}"/>
     </rule>

- Enable Browser cache Browser cache, sometimes also referred to as the temporary Internet files folder, contains files from web sites you've visited. All modern web browsers maintain a cache of files for one important reason - faster display of web pages the next time you open those web sites. Thus, instead of being retrieved from the online web server (the computer that hosts the web site) each time, the files are picked from the browser cache (on your computer) which, as you can understand, speeds up the display of the web page. Adding below content in web.config file would set the cache-control for static files . 

<!-- Set expire headers to 30 days for static content--> 

<clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="30.00:00:00" /> 


 Browser screenshot : [![7](https://msdnshared.blob.core.windows.net/media/2016/05/73.jpg)](https://msdnshared.blob.core.windows.net/media/2016/05/73.jpg) 

######Use Local cache

*   As i have mentioned earlier, Azure web apps use remote storage.
*   Every file access would add this network latency between web app machine and storage.
*   You can turn-on local cache by adding below app setting in azure portal.

`WEBSITE_LOCAL_CACHE_OPTION` = `Always` 

[![app-service-local-cache-configure-portal](https://msdnshared.blob.core.windows.net/media/2016/05/app-service-local-cache-configure-portal.png)](https://msdnshared.blob.core.windows.net/media/2016/05/app-service-local-cache-configure-portal.png)

*   A **one-way sync process** is established and all the content in storage for that web app is copied to web app machine.
*   Using Local cache would reduce response time as files are stored in web app machine itself.

**The local cache is read-write. However, any modifications will be discarded when the web app moves virtual machines or gets restarted. You should not use Local Cache for apps that store mission-critical data in the content store.** **More Info : [https://azure.microsoft.com/en-us/documentation/articles/app-service-local-cache/](https://azure.microsoft.com/en-us/documentation/articles/app-service-local-cache/)**   


**Useful Links:** 10 ways to speed up WordPress - [https://sunithamk.wordpress.com/2014/08/01/10-ways-to-speed-up-your-wordpress-site-on-azure-websites/](https://sunithamk.wordpress.com/2014/08/01/10-ways-to-speed-up-your-wordpress-site-on-azure-websites/ "wordpress speed-up")

