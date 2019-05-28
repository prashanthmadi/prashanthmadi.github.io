---
layout: post
title: Playing Piano(Python App) in Azure App Service Linux
date: '2017-07-03 21:13:02'
previewimg: '/content/images/2017/07/banner-1.jpg'
tags:
- azure
- app-services
- python
- tensorflow
- flask
- magenta
---

Azure App Service is a Paas solution to run Enterprise-grade Web Applications. Azure has recently announced [App Services on Linux](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-intro). It supports running web apps natively on Linux.

App Service Linux provides pre-defined application stacks(Nodejs, PHP and others ). App Service on Linux uses Docker containers to host these pre-built application stacks. You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.
More Info : https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-using-custom-docker-image

In this blog, I would like to provide steps for running a Python app on App Service Linux. To make it little more fun, I would be using [Magenta](https://github.com/tensorflow/magenta) to play Piano. 
Final project is available on Github @ https://github.com/prashanthmadi/ai-duet-tensor

Below is the architecture of App Service Linux
![Python App on App Services Linux](/content/images/2017/07/architecture-1.png)

Request would hit one of the App Service front-end and navigates to worker-role. Inside worker-role, There would be two different containers

- [Kudu](https://github.com/projectkudu/kudu/wiki) Container(Used for Tooling Purpose : `https://your_app_name.scm.azurewebsites.net`)
- App Container (Your App runs here)

Consider them as two different OS having their own file-system while share only `/home` directory(Remote persistent Storage). 
i.e, `/var` on Kudu is not same as `/var` on App container

```
Note : Only /home content is persistent, Anything written to other folders will be gone after App restart.
```
####Running Sample Python app on Local environment
As I have mentioned earlier, we would be using Magenta to play Piano that responds.

* Navigate to github page of [Magenta](https://github.com/tensorflow/magenta/tree/master/demos/ai-duet) and download ai-duet demo.
* Follow steps in README to run this sample app.

#### Using waitress
* Create `run_waitress_server.py` file in app and copy below content into it.
```
import os
from waitress import serve
from server import app
serve(app, host="127.0.0.1", port=8080)
```
* Add waitress in requirements.txt file

####Add Docker Related Files
* Create a new folder and copy above step sample app into `app` folder in project root.
* Copy `DockerFile` and others at root folder from [here](https://github.com/prashanthmadi/ai-duet-tensor)
* `DockerFile` would install
    * Python
    * nginx (Check `nginx.conf` for configuration)
    * openssh-server(Used to make web-ssh connection between Kudu and App Container. Check `sshd_config` file)
    * supervisor (To start nginx and python app simultaneous. Check `supervisord.conf` file)
    * Install Python App dependencies in `requirements.txt` file
* `init_container.sh` will run on first request and starts ssh, supervisord.  

#### Publish to DockerHub
* Publish app to github
    * ex: https://github.com/prashanthmadi/ai-duet-tensor
* Setup Automated build from git repository in [Dockerhub](https://hub.docker.com/).
    * ex: https://hub.docker.com/r/prashanthmadi/ai-duet-tensor/

Note: I have used Dockerhub but you can use other options like [Azure Container Services](https://docs.microsoft.com/en-us/azure/container-service/container-service-intro).

#### Create App Services Linux 
* Follow steps @ https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-how-to-create-web-app
* Select `Docker Hub` in Configure container and set Image,Tag.
 - Ex : prashanthmadi/ai-duet-tensor:latest
![](/content/images/2017/07/custom_container-2.PNG)
#### Final output
url : http://ai-duet-sample.azurewebsites.net/

![AI Duet on Azure App Service Linux](/content/images/2017/07/ai-duet-output.PNG)