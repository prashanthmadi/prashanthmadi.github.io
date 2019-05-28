---
layout: post
title: installing Java
date: '2010-10-18 16:08:00'
tags:
- java
---

i know many of us get struck with the little things... the code below are few simple steps to install java on your machine 

Linux 
----- 
Add partner repository using the following command 

> sudo add-apt-repository "deb http://archive.canonical.com/ lucid partner" 

Update the source list 

> sudo apt-get update 

Now install sun java packages using the following commands 

> sudo apt-get install sun-java6-jre sun-java6-plugin sun-java6-fonts 

test by using the following command 

java -verison 

Just installing new Java flavours does not change the default Java pointed to by /usr/bin/java. You must explicitly set this: 

Open a Terminal window 
Run sudo update-java-alternatives -l to see the current configuration and possibilities. 
Run sudo update-java-alternatives -s XXXX to set the XXX java version as default. For Sun Java 6 this would be sudo update-java-alternatives -s java-6-sun 
Run java -version to ensure that the correct version is being called. 
You can also use the following command to interactively make the change; 

Open a Terminal window 
Run sudo update-alternatives --config java 
Follow the onscreen prompt 
You can also try IcedTea NPR Web Browser Plugin