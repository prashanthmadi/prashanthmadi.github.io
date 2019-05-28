---
layout: post
title: got struck with installing biojava..
date: '2010-11-09 22:26:00'
tags:
- bio_informatics
---

i installed it using the Readme file for the swarmapp but actually it need to be installed using maven... 

atlast the following command worked out 

mvn install:install-file -DgroupId=biojava -DartifactId=biojava -Dversion=1.6.1 -Dpackaging=jar -Dfile=/path/to/file