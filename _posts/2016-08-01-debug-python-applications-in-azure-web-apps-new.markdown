---
layout: post
title: Debug Python Applications in Azure Web Apps
date: '2016-08-01 20:22:20'
previewimg: '/content/images/2016/08/windows-azure-cloud.png'
tags:
- azure
- python
---

After creating a Azure Web app using Python, you may end-up getting below 500 error at some point of your application development process.This Blog describes how to enable  logs for a Python Web APP on Azure.

> The page cannot be displayed because an internal server error has occurred.

If you have worked earlier on Azure Web app, General tendency would be to look at LogFiles folder in kudu console https://`Your_Website`.scm.azurewebsites.net but that won't provide you much info about python application issue.

To overcome this, Please follow below set of instructions to receive application logs

* Navigate to your new azure portal and click on settings in your Web app.
* Click on Application Settings in Settings Tab
* Enter Below Key/Value pair under App Settings in Application Settings Tab.</span>
```
Key : WSGI_LOG
Value : D:\home\site\wwwroot\logs.txt    (Enter your choice of file name here)
```
![Azure App Setting](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/8171.new3.JPG)

* Now you should be able to see logs.txt file in wwwroot folder as mentioned in above step

![Python Output Logs](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/0601.end_result.JPG)

**Troubleshoot :**

If you still haven't found that logs.txt file, check if `ptvs_virtualenv_proxy.py` file is similar to below link content. [https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/#virtual-environment-proxy](https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/#virtual-environment-proxy)





Find more details on using Python in Azure Web Apps at below links : 

* Python Developer Center - [http://azure.microsoft.com/en-us/develop/python/](http://azure.microsoft.com/en-us/develop/python/)
* Configuring Python in Azure Web Apps - [https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/](https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/)