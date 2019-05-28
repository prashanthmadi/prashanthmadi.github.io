---
layout: post
title: left out with one dependency..
date: '2010-11-10 17:31:00'
---

installed all the java dependencies.. 

left out with the swarm jar file 

3) Swarm:Swarm:jar:0.9 

Try downloading the file manually from the project website. 

Then, install it using the command: 
mvn install:install-file -DgroupId=Swarm -DartifactId=Swarm -Dversion=0.9 -Dpackaging=jar -Dfile=/path/to/file 

Alternatively, if you host your own repository you can deploy the file there: 
mvn deploy:deploy-file -DgroupId=Swarm -DartifactId=Swarm -Dversion=0.9 -Dpackaging=jar -Dfile=/path/to/file -Durl=[url] -DrepositoryId=[id] 

Path to dependency: 
1) swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 
2) Swarm:Swarm:jar:0.9