---
layout: post
title: "(Deprecated) Running Python Code on Azure Functions App"
date: '2017-03-30 03:41:43'
previewimg: '/content/images/2017/03/python_functions.png'
tags:
- python
- azure
- app-services
- functions
---

## Update 11/7/18

## Retiring this in favor of Azure Functions V2

http://aka.ms/functions-python-preview 




_Update 4/25/17 : Adding steps to install python from [Site Extensions](https://www.siteextensions.net/profiles/steve.dower). These are Python binaries patched to work well in Azure App Services. Thanks to Steve Dower for contributing  Python Site extensions and keeping them up-to-date_. 

**Azure Functions** is an event driven, compute-on-demand experience that extends the existing Azure application platform with capabilities to implement code triggered by events occurring in Azure or third party service as well as on-premises systems. 

More Info : https://azure.microsoft.com/en-us/blog/introducing-azure-functions/
Get Started with Azure Functions @ https://azure.microsoft.com/en-us/services/functions/

In this blog, I would provide details to run Python Code in Azure Functions. Below are the steps I would follow

1. Create Function App in Azure Portal
2. Using Custom Python Version
3. Install and Use Third-party Modules

### Note: Python is still in experimental mode for Azure Functions, so this experience is going to change before it comes to General Available

<br>

#### Create Function App in Azure Portal
Follow content in below link to quickly create a Function App in Azure Portal
https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function 

#### Adding your First Python Function
Python is still in experimental phase, so there is no easy way to create a function. I would use a little hack for now but it might change in future

* Select GenericWebHook-JS from available templates in portal and create it
![JS Generic Webhook](/content/images/2017/03/js_generic.PNG)
* Create new file `run.py` with below content and delete index.js using View Files Nav on right

```
import os
import platform

message = "Using Python '{0}'".format(platform.python_version())
print(message)
```

Above code will print the Python version after clicking `Run` Button on top
![Python First Function App](/content/images/2017/03/first_py.png)

#### Using Custom Python Version
You might have realized that it uses Python v`2.7.8` from above output which is very old. In this section I would provide details to upgrade python version

To Install Custom Python Version, 

* Navigate to Kudu Console -  https://`Your_APP_NAME`.scm.azurewebsites.net/DebugConsole
* Run Below command in kudu cli to install Python in `D:\home\site\tools` Folder


```
nuget.exe install -Source https://www.siteextensions.net/api/v2/ -OutputDirectory D:\home\site\tools python352x64 
```
Above command will install Python v3.5.2 64-bit. For other python versions/arch refer below link
https://www.siteextensions.net/profiles/steve.dower

* We need to have python.exe in D:\home\site\tools Folder. so lets move sub-folder content(`D:\home\site\tools\python352x64.3.5.2.6\content\Python35`
) to `D:\home\site\tools` using below command
```
mv /d/home/site/tools/python352x64.3.5.2.6/content/python35/* /d/home/site/tools/
```
Click Run for the function we created earlier in portal and it should use newer version of python now.
![After updating Python](/content/images/2017/04/python_updated.PNG)

#### Install and Use Third-party Modules

* Navigate to Kudu Console -  https://`Your_APP_NAME`.scm.azurewebsites.net/DebugConsole
* Run below command to install pandas module in function app
```
D:\home\site\tools\python.exe -m pip install pandas
```
![Installing Pandas on Azure Functions](/content/images/2017/03/pandas_install.PNG)

You can replace pandas with any other module in above command

Refer below link on different ways to install Python modules in app services
https://prmadi.com/install-python-modules-on-azure-app-services/

Using Panda module in our example code
```
import os
import platform
import pandas as pd
message = "Using Python '{0}'".format(platform.python_version())
print(message)
print('Pandas version ' + pd.__version__)
```
#### Final Output :

Function App Using Custom Python version(2.7.13) and Third-party Module(Pandas)

![Pandas on App Services](/content/images/2017/03/padans_on_app_service.PNG)


#### Additional Info

**1. How do I read post data in HTTP trigger ?**
```
postreqdata = open(os.environ['req']).read()
print postreqdata
```
**2. How do I output data in HTTP response ?**

```
response = open(os.environ['res'], 'w')
response.write("hello world prashanth")
response.close() 
```

#### Troubleshoot
Logging:
- Use basicConfig of logging and set filename. you should see file created in function folder with "Watch out!". 
```
import logging
logging.basicConfig(filename='example.log',level=logging.DEBUG)
logging.warning('Watch out!')
```
![](/content/images/2017/08/Screen-Shot-2017-08-03-at-3-01-31-PM.png)


#### References :
WHY ARE THERE SO MANY PYTHON INSTALLERS?
http://stevedower.id.au/blog/why-so-many-python-installers/

Thanks to Chris Anderson (@crandycodes) in helping me write this blog.
Thanks to [Laurent Mazuel](https://twitter.com/lmazuel) for blog-review and making it better.