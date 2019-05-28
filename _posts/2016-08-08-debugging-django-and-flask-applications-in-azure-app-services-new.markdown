---
layout: post
title: Debugging Django and Flask Applications in Azure App services
date: '2016-08-08 01:02:01'
previewimg: '/content/images/2016/08/djangoflask.png'
tags:
- azure
- python
- django
- flask
---

After creating a Azure Web app using Django Framework in Python, you may end-up getting Application errors at some point of your Application Development Process. This Blog describes how to enable Application logs for a Azure Web APP which uses Django Framework.

Before starting debug process make sure that you have below two important files at Web APP Root folder. You can find them in wwwroot folder @ kudu console `https://Your_webApp_Name.scm.azurewebsites.net`

    web.config  
    ptvs_virtualenv_proxy.py

Please find more information on above files @ [https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/#webconfig](https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/#webconfig)

####Flask

Will update it soon


####Django
You can display Django Application errors using below three channels

######Display Application Errors on Web Browser
* Open settings.py file in your Django Web App

![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/7384.dj1.JPG)

* In Settings.py file change debug option to True as below

   DEBUG = True

Output :
![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/2451.dj2.JPG)

As you can see in above screen shot, Application error info is shown on web page with error Traceback.

It is highly recommended to Swtich **DEBUG** option to **False** when you move the site into **Production**.

######Log Errors in a Azure File System.

* In settings.py file add below content for LOGGING variable
```
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'filters': {
        'require_debug_false': {
            '()': 'django.utils.log.RequireDebugFalse'
        }
    },
    'handlers': {
        'logfile': {
            'class': 'logging.handlers.WatchedFileHandler',
            'filename': 'D:\home\site\wwwroot\myapp.log'
        }
    },
    'loggers': {
        'django': {
            'handlers': ['logfile'],
            'level': 'ERROR',
            'propagate': False,
        }
    }
}
```

* You can find more information on LOGGING module @ [https://docs.djangoproject.com/en/dev/topics/logging/](https://docs.djangoproject.com/en/dev/topics/logging/)

**Output :**

After making above changes, You would see `myapp.log` file in wwwroot folder as in Below screenshot.

![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/6253.dj3.JPG)

Below Screenshot has the error message in myapp.log file.

![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/4034.dj4.JPG)

This option is highly suitable for websites in production.

######Email Application Errors to Developers

* In settings.py file add below content for LOGGING variable. I have highlighted configuration which is required to send an Email in RED.
```
    LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'filters': {
        'require_debug_false': {
            '()': 'django.utils.log.RequireDebugFalse'
        }
    },
    'handlers': {
        'mail_admins': {
            'level': 'ERROR',
            'filters': ['require_debug_false'],
            'class': 'django.utils.log.AdminEmailHandler',
            'include_html': True
        },
        'logfile': {
            'class': 'logging.handlers.WatchedFileHandler',
            'filename': 'D:\home\site\wwwroot\myapp.log'
        }
    },
    'loggers': {
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': True,
        },
        'django': {
            'handlers': ['logfile'],
            'level': 'ERROR',
            'propagate': False,
        }
    }
    }
```
* Include smtp connection details in settings.py file as below
````
EMAIL_USE_TLS = True 
EMAIL_HOST = 'smtp.gmail.com' 
EMAIL_PORT = 587 
EMAIL_HOST_USER = 'Your_GMAIL@gmail.com' 
EMAIL_HOST_PASSWORD = 'Your_GMAIL_Password'
```
* Change recipient email address in setting.py file as Below
```
ADMINS = ( ('XYZ ABC', 'abc@xyz.com'), )
```
**Output :**

A email would be sent to recipients mentioned above when a application error occurs. Below is a Sample Application error message which I received for my website.

![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/3482.dj5.JPG)

You can also send an email in html format by including below line of code in logger handler. Below is a Sample Application error message which I received for my website in HTML format.

    'include_html': True

![](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/01/70/08/1031.dj6.JPG)

Find more details on using Python in Azure Web/API Apps at below links : 

* Python Developer Center - [http://azure.microsoft.com/en-us/develop/python/](http://azure.microsoft.com/en-us/develop/python/)
* Configuring Python in Azure Web Apps - [https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/](https://azure.microsoft.com/en-us/documentation/articles/web-sites-python-configure/)
