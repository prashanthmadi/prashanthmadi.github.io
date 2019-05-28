---
layout: post
title: workit out !!!!!!
date: '2010-11-08 18:15:00'
tags:
- bio_informatics
---

Missing: 
---------- 
1) biojava:biojava:jar:1.6.1 

Try downloading the file manually from the project website. 

Then, install it using the command: 
mvn install:install-file -DgroupId=biojava -DartifactId=biojava -Dversion=1.6.1 -Dpackaging=jar -Dfile=/path/to/file 

Alternatively, if you host your own repository you can deploy the file there: 
mvn deploy:deploy-file -DgroupId=biojava -DartifactId=biojava -Dversion=1.6.1 -Dpackaging=jar -Dfile=/path/to/file -Durl=[url] -DrepositoryId=[id] 

Path to dependency: 
1) swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 
2) biojava:biojava:jar:1.6.1 

2) javax.sql:jdbc-stdext:jar:2.0 

Try downloading the file manually from: 
http://java.sun.com/products/jdbc/download.html 

Then, install it using the command: 
mvn install:install-file -DgroupId=javax.sql -DartifactId=jdbc-stdext -Dversion=2.0 -Dpackaging=jar -Dfile=/path/to/file 

Alternatively, if you host your own repository you can deploy the file there: 
mvn deploy:deploy-file -DgroupId=javax.sql -DartifactId=jdbc-stdext -Dversion=2.0 -Dpackaging=jar -Dfile=/path/to/file -Durl=[url] -DrepositoryId=[id] 

Path to dependency: 
1) swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 
2) javax.sql:jdbc-stdext:jar:2.0 

3) Swarm:Swarm:jar:0.9 

Try downloading the file manually from the project website. 

Then, install it using the command: 
mvn install:install-file -DgroupId=Swarm -DartifactId=Swarm -Dversion=0.9 -Dpackaging=jar -Dfile=/path/to/file 

Alternatively, if you host your own repository you can deploy the file there: 
mvn deploy:deploy-file -DgroupId=Swarm -DartifactId=Swarm -Dversion=0.9 -Dpackaging=jar -Dfile=/path/to/file -Durl=[url] -DrepositoryId=[id] 

Path to dependency: 
1) swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 
2) Swarm:Swarm:jar:0.9 

4) javax.security:jaas:jar:1.0.01 

Try downloading the file manually from: 
http://java.sun.com/products/jaas/index-10.html 

Then, install it using the command: 
mvn install:install-file -DgroupId=javax.security -DartifactId=jaas -Dversion=1.0.01 -Dpackaging=jar -Dfile=/path/to/file 

Alternatively, if you host your own repository you can deploy the file there: 
mvn deploy:deploy-file -DgroupId=javax.security -DartifactId=jaas -Dversion=1.0.01 -Dpackaging=jar -Dfile=/path/to/file -Durl=[url] -DrepositoryId=[id] 

Path to dependency: 
1) swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 
2) javax.security:jaas:jar:1.0.01 

---------- 
4 required artifacts are missing. 

for artifact: 
swarmapp:swarmapp:jar:0.0.1-SNAPSHOT 

from the specified remote repositories: 
central (http://repo1.maven.org/maven2) 

[INFO] ------------------------------------------------------------------------ 
[INFO] For more information, run Maven with the -e switch 
[INFO] ------------------------------------------------------------------------ 
[INFO] Total time: 5 seconds 
[INFO] Finished at: Mon Nov 08 10:01:07 CST 2010 
[INFO] Final Memory: 11M/26M 
[INFO] ------------------------------------------------------------------------