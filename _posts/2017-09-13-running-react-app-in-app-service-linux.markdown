---
layout: post
title: Running React App in Azure App Service Linux with Continuous Deployment
date: '2017-09-13 02:52:28'
tags:
- react
- azure
- app-services
- linux
- docker
---

[React](https://facebook.github.io/react/) is a Javascript library for building User Interface. I had multiple requests to write this blog on best way to run SPA(Single page applications) at Azure App Service Linux.

_Check my previous blog for deploying SPA (Single Page Applications) in Azure App Service (Windows)@ https://prmadi.com/running-angular2-app-on-azure-app-services-with-ci-cd/_

Azure App Service is a PAAS solution to run Enterprise-grade Web Applications. Azure has recently announced [App Services on Linux](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-linux-intro). It supports running web apps natively on Linux using Docker Technology.

You can find a Sample React project with below operations @ [GitHub Link](https://github.com/prashanthmadi/azure-react-sample)

## Requirements:
- VS Code (or any other good editor)
- Node.js installed on your machine

## Create Sample React App
- I have used [Create React App](https://github.com/facebookincubator/create-react-app#getting-started) module to quickly create a sample react application.
```
> npm install -g create-react-app
> create-react-app azure-demo
> cd azure-demo
```

If you open azure-demo folder in VS code. It should look like below

![react_files](/content/images/2017/09/react_files.PNG)

## Run it in Local env
```
> npm start
```
Output:

![react_local](/content/images/2017/09/react_local.PNG)

## Add deployment script
In Azure App Service, there is a good feature to run a bash script after moving code to App service. Check below links for more info
- https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script
- https://prmadi.com/azure-custom-deployment/

Basically, We would add below two files in root folder

- `.deployment` : https://github.com/prashanthmadi/azure-react-sample/blob/master/.deployment
- `deploy.sh` : https://github.com/prashanthmadi/azure-react-sample/blob/master/deploy.sh

Above mentioned links would have content of each file

![Screen-Shot-2017-09-12-at-1.17.01-AM](/content/images/2017/09/Screen-Shot-2017-09-12-at-1.17.01-AM.png)

### what are we doing in custom deployment script(`deploy.sh`) ?
After Content is moved from remote git repository to `/home/site/repository`. we use deployment script to perform below actions
- Navigate to `/home/site/repository` folder
- execute command `npm install`
- execute command `npm run build` that creates `/home/site/repository/build` folder
- Kudu Sync, moves content from `/home/site/repository/build` folder to `/home/site/wwwroot`

## Create Web App(Linux) in Azure Portal 
- Click on below button and enter required details in portal

[![Azure Deploy](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fprashanthmadi%2Fazure-appservice-nginx%2Fmaster%2Ftemplate.json) 
This would create Azure App service Linux and uses below nginx image
Docker Hub : https://hub.docker.com/r/prashanthmadi/azure-appservice-nginx/

                                   (or)

Note: You can ignore below steps if you used Deploy to Azure button above

- Navigate to portal and select "Web App for Containers"
- Set `prashanthmadi/azure-appservice-nginx:1.13` as Image

![custom_docker](/content/images/2017/09/custom_docker.PNG)

- set `WEBSITES_ENABLE_APP_SERVICE_STORAGE` to `true` in Application settings

![appsetting](/content/images/2017/09/appsetting.PNG)

## Push your App to Azure
- If your app is on bitbucket/github/local git, follow content in below link to setup continuous deployment

https://docs.microsoft.com/en-us/azure/app-service-web/app-service-continuous-deployment

## Final Output

![Screen-Shot-2017-09-12-at-1.34.12-AM](/content/images/2017/09/Screen-Shot-2017-09-12-at-1.34.12-AM.png)

You can find a Sample React project with above operations @ [GitHub Link](https://github.com/prashanthmadi/azure-react-sample)

## Extra features
You can control nginx configuration used in app container by creating  `nginx.conf` file @ `/home/site` folder

Ex: default root folder is set to `/home/site/wwwroot`. You can change it to `/home/site/wwwroot/build` by creating `nginx.conf` file @ `/home/site` with below content.

```
worker_processes auto;
pid          /var/run/nginx.pid;
daemon off;

events {
  worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';
    access_log off;
    tcp_nopush     on;
    keepalive_timeout  65;
    gzip  on;

    server {
        listen 80;
        server_name  www.example.com;
        error_log  /home/LogFiles/error.log warn;
        root   /home/site/wwwroot/build;
        index  Default.htm Default.html index.html index.htm hostingstart.html;

        # Make site accessible from http://localhost/
        server_name _;
        sendfile on;

        location ~* \.(js|css|png|jpg|jpeg|gif|ico|mp3|html)$ {
            expires 1d;
        }

    }
}

```

If you are using react/angular, make sure all your requests end up at index.html else you would receive 404 errors. Below is the sample for location that should do the trick.

```
location / {
        try_files $uri /index.html;
        add_header   Cache-Control public;
        expires      1d;
    }
```