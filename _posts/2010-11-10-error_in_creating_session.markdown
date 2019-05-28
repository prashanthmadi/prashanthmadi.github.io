---
layout: post
title: error in creating session..
date: '2010-11-10 18:14:00'
---

org.hibernate.HibernateException: Could not parse configuration: /hibernate.cfg.xml 
at org.hibernate.cfg.Configuration.doConfigure(Configuration.java:1494) 
at org.hibernate.cfg.Configuration.configure(Configuration.java:1428) 
at org.hibernate.cfg.Configuration.configure(Configuration.java:1414) 
at com.mycompany.app.db.HibernateSessionFactory.<clinit>(HibernateSessionFactory.java:30) 
at com.mycompany.entity.Programs.getProgramsWaitingForSubmission2(Programs.java:33) 
at com.mycompany.app.job.JobManager.runJobSubmissions(JobManager.java:744) 
at com.mycompany.app.clients.JobClient2.runJobs(JobClient2.java:102) 
at com.mycompany.app.clients.JobClient2.access$000(JobClient2.java:18) 
at com.mycompany.app.clients.JobClient2$4.run(JobClient2.java:87) 
Caused by: org.dom4j.DocumentException: Error on line 2 of document : The processing instruction target matching "[xX][mM][lL]" is not allowed. Nested exception: The processing instruction target matching "[xX][mM][lL]" is not allowed. 
at org.dom4j.io.SAXReader.read(SAXReader.java:482) 
at org.hibernate.cfg.Configuration.doConfigure(Configuration.java:1484) 
... 8 more 
%%%% Error Creating SessionFactory %%%% 
org.hibernate.HibernateException: /var/www/site31/swarmapp/src/main/resources/hibernate.cfg.xml not found 
at org.hibernate.util.ConfigHelper.getResourceAsStream(ConfigHelper.java:147) 
at org.hibernate.cfg.Configuration.getConfigurationInputStream(Configuration.java:1405) 
at org.hibernate.cfg.Configuration.configure(Configuration.java:1427) 
at com.mycompany.app.db.HibernateSessionFactory.rebuildSessionFactory(HibernateSessionFactory.java:94) 
at com.mycompany.app.db.HibernateSessionFactory.getSession(HibernateSessionFactory.java:72) 
at com.mycompany.entity.Programs.getProgramsWaitingForSubmission2(Programs.java:33) 
at com.mycompany.app.job.JobManager.runJobSubmissions(JobManager.java:744) 
at com.mycompany.app.clients.JobClient2.runJobs(JobClient2.java:102) 
at com.mycompany.app.clients.JobClient2.access$000(JobClient2.java:18) 
at com.mycompany.app.clients.JobClient2$4.run(JobClient2.java:87)</clinit>