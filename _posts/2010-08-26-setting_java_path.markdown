---
layout: post
title: setting java path
date: '2010-08-26 20:43:00'
tags:
- java
---

goto nano ~/.bashrc file 

JAVA_HOME=/usr/java/jdk1.6.0_21 
export JAVA_HOME 
PATH=$PATH:/usr/java/jdk1.6.0_21/bin 
export PATH 
PATH=$PATH:/usr/share/maven2/bin 
export PATH 
ANT_HOME=/usr/share/ant 
PATH=$PATH:${ANT_HOME}/bin 
export PATH