---
layout: post
title: Relay Docker Image tag to DockerFile during build phase
date: '2017-08-05 17:03:54'
tags:
- nodejs
- docker
- dockerhub
---

In Agile world, we started seeing many of the programming languages release a newer version of it every other week/month. 

You might be surprised to see number of nodejs versions released over past year.
https://nodejs.org/en/download/releases/ 
![never ending](/content/images/2017/08/never_ending.gif)

So how do we generate a Dockerfile based on nodejs that supports all of its versions ?

* Make a separate folder for each nodejs version and create DockerFile inside each of it. 

Below was our project with multiple folders

![Nodejs Folders](/content/images/2017/08/Screen-Shot-2017-08-05-at-1-03-45-AM.png)

This solution might work but what if you have duplicate code in all these folders and you found a bug in it

In one of our project, We currently have multiple folders with same content except a change in tag name used to get that particular nodejs version. It might get harder to manage/change all these files with more nodejs versions to be supported in future.

I did some research and found that hooks can be utilized to eliminate such scenarios and pass tag of main image into DockerFile during build at Docker Hub.

Here is a snippet of my Dockerfile at root folder. I have intentionally not defined a tag. This would be automatically replaced later.
```
FROM node:{{tag}}

COPY startup /opt/startup
COPY hostingstart.html /app/hostingstart.html
# more content .....

ENTRYPOINT ["/opt/startup/init_container.sh"]

```
* create hooks folder in project root
* create build file inside hooks and add below content in it
```
#!/usr/bin/env bash

# DOCKER_TAG would be replaced by tag in docker hub
sed -i 's@{{tag}}@'"${DOCKER_TAG}"'@' Dockerfile
docker build -t ${IMAGE_NAME} .
```

Sample Project: https://github.com/prashanthmadi/node

With this approach, now i can define tags at Docker hub and pass that to Dockerfile instead of maintaining multiple folders of same content.

![](/content/images/2017/08/Screen-Shot-2017-08-05-at-11-53-17-AM.png)
 
#### Future Improvements: 
With the existing approach, i'm using sed to replace tag as dockerhub uses 15.03 and doesn't support using image_tag in FROM directly.

using image_tag in FROM would be supported in docker >15.05 and we might not need sed operation in future.

#### Reference:

* Support for environment variables for building containers [#6822](https://github.com/moby/moby/issues/6822)