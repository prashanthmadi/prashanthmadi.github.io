---
layout: post
title: Running Docker on Azure VM
date: '2016-11-28 22:04:00'
tags:
- azure
- docker
---

- Create Azure Ubuntu VM from portal
- Follow steps in below link to install docker on Linux VM
https://docs.docker.com/engine/installation/linux/ubuntulinux/

You can find docker cli docs @ [Link](https://docs.docker.com/engine/reference/commandline/cli/). I have documented on some of the important commands i use below

#### Operations on Docker Images
Search for docker image 
```
docker search ubuntu  
```
or use docker hub - https://hub.docker.com

Download Image from dockerhub
```
docker pull httpd:2.4
```
View Images in Local
```
docker images
```
Delete Image
```
docker rmi image_name
```
Delete all Image
```
docker rmi $(docker images -q)
```

#### Operations on Container
Run/Create Container from Image
```
docker run ubuntu
```
Run/Create Container from Image in background
```
docker run -d --name perlapp prashanthmadi/appserviceperl
```

Stop container
```
docker stop container_name
```
Start Container
```
docker start container_name
```

List active containers
```
docker ps
```

list all containers 
```
docker ps -a
```
delete container 
```
docker rm container_id
```
Delete all containers
```
docker rm $(docker ps -a -q)
```
login to container bash
```
docker exec -it container_name /bin/bash
```

docker container [logs](https://docs.docker.com/engine/reference/commandline/logs/)
```
docker logs [OPTIONS] CONTAINER
```
