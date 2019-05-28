---
layout: post
title: Python Django App Integrated with Send Grid Email Delivery Service (Azure Web
  Apps on windows)
date: '2018-10-10 02:47:30'
---

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

- Create a sample application
- Create Azure Web App (windows) 
- Update python version from site extensions
- Create deployment script
- Configure Send Grid Email Delivery system
- Publish App

You can find a sample Python Django project with above operations @ [Github Link](https://github.com/gangularamya/azure-django-httpplatformhandler)

**Create a Sample Application**
- Install Django
- Check if Django is installed on your machine
```$ python -m django --version```
- Create a project
```$ django-admin startproject mysite```
- Create the polls app
```$ python manage.py startapp polls```

You can also follow https://www.djangoproject.com/start/ to get started with Django

**Create Azure WebApp and Site Extensions to Upgrade Python Version**

  -  Navigate to Azure Portal
  -  Create a new web app
  -  Setup [Continuous Deployment](https://docs.microsoft.com/en-us/azure/app-service/app-service-continuous-deployment) or Use local git to push your code to azure.
  -  From your web app serach for extensions and install the latest Python version.
  ![SG1](/content/images/2018/09/SG1.PNG)
  
 For this sample i did choosed Python 3.6.4 x64, that would install new version of python@ D:\home\Python364
 

**Create SendGrid Email Delivery from Azure Portal**

- From portal serach for SendGrid Email Delivery and create it using your details.

![Sendgrid1](/content/images/2018/09/Sendgrid1.PNG)

- After creating account, you will find the Username, SMTP sever under Configurations section as below screenshot

![SG3](/content/images/2018/09/SG3.PNG)

- In settings.py include Send grid configurations as below.

```EMAIL_HOST = 'smtp.sendgrid.net'
EMAIL_HOST_USER = 'Your username'
EMAIL_HOST_PASSWORD = 'Your Password'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
```
- Finally you can see the emails delivered from SendGrid Dashboard.

![SG4](/content/images/2018/09/SG4.PNG)

**Publish App**

![SG2](/content/images/2018/09/SG2.PNG)



