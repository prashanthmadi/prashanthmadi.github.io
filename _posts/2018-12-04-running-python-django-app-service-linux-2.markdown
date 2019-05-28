---
layout: post
title: Running Python 3.7 Django App service Linux on Azure
date: '2018-12-04 05:03:04'
---

In this blog I'm creating Django app with Python 3.7 image from Azure Web App on Linux

- Create an app and open visual studio code
- Create requirements.txt with below content

    django==2.1.2

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/django1-1.PNG" class="kg-image"></figure>
- Make sure you create virtual env from Python 3.7 version

    python.exe -m venv venv

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image.png" class="kg-image"></figure>
- After creating it…Activate venv as below

    .\venv\Scripts\activat.bat

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-1.png" class="kg-image"></figure>
- Install requirements.txt

    pip install -r requirements.txt

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-2.png" class="kg-image"><figcaption>`</figcaption></figure>
- Check if Django is installed correctly

    python -m django --version

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-3.png" class="kg-image"><figcaption>`</figcaption></figure>
- Do **django-admin startproject \<somename\>** that creates auto-generate code to start Django app with

    django-admin startproject mydjangoapp

<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-4.png" class="kg-image"></figure>
- Replace application.py content with below (In line 6 &nbsp;“your djangoapp.settings”)
- Source:[https://github.com/gangularamya/AzurePythonDjangoWAFL/blob/master/application.py](https://github.com/gangularamya/AzurePythonDjangoWAFL/blob/master/application.py)
<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-7.png" class="kg-image"></figure>
- Include Allowed hosts in settings.py file
<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-8.png" class="kg-image"></figure>
- Navigate to Azure Portal.
- Create Web App on Linux.
<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-9.png" class="kg-image"></figure>
- Setup [Continuous Deployment](https://docs.microsoft.com/en-us/azure/app-service/app-service-continuous-deployment) or Use local git to push your code to azure.
<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-10.png" class="kg-image"></figure>
- You can find a sample Python Django project with above operations @[GitHub Link](https://github.com/gangularamya/AzurePythonDjangoWAFL)

**SERVING STATIC FILES:**

- Add whitenoise plugin to serve static files on Azure.

[https://pypi.org/project/whitenoise/](https://pypi.org/project/whitenoise/)

[https://devcenter.heroku.com/articles/django-assets](https://devcenter.heroku.com/articles/django-assets)

- My Sample output with static file.
<figure class="kg-card kg-image-card"><img src="/content/images/2018/12/image-11.png" class="kg-image"></figure>