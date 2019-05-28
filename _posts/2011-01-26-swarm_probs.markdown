---
layout: post
title: swarm probs
date: '2011-01-26 17:43:00'
---

[INFO] [jar:jar {execution: default-jar}] 
[INFO] Preparing exec:java 
[WARNING] Removing: java from forked lifecycle, to prevent recursive invocation. 
[INFO] No goals needed for project - skipping 
[INFO] [exec:java {execution: default}] 
11:05:36,441 DEBUG JobClient2:134 - 2011-01-26 11:05:36 JavaDaemonTest started 
11:05:36,443 DEBUG JobClient2:134 - 2011-01-26 11:05:36 2011-01-26 11:05:36 This is output to StdErr... 
11:05:36,906 DEBUG PropertyUtil:33 - L1 
11:05:36,914 DEBUG PropertyUtil:35 - L2 
11:05:36,914 DEBUG PropertyUtil:39 - L3 
11:05:45,709 DEBUG JobManager:742 - Job Submission Thread is running... 
11:05:45,807 DEBUG Programs:32 - Getting the list of jobs waiting to be submitted 
11:06:21,839 DEBUG JobManager:289 - Submitting 8 jobs 
11:06:21,843 DEBUG SwarmUtil:156 - Requesting ticket now 
11:06:21,870 DEBUG SwarmUtil:162 - org.apache.axis2.rpc.client.RPCServiceClient@1 
11:06:28,330 DEBUG SwarmUtil:166 - Ticket request result: Username: qdong 
Email: Default email address 
Project: GSA Project 
Organization: default organization 
Group Job Title: default job title 
Group Job Descriptiondefault job description 
Expected Number of Jobs130000 
Timestamp: Wed Jan 26 11:06:27 CST 2011 
TicketID-743724069 
Current number of jobs submitted0 
11:06:28,357 DEBUG JobManager:258 - ticketID : -743724069 
11:06:28,742 DEBUG JobManager:204 - 1017 RepeatMasker 
[INFO] ------------------------------------------------------------------------ 
[ERROR] BUILD ERROR 
[INFO] ------------------------------------------------------------------------ 
[INFO] An exception occured while executing the Java class. org/biojava/bio/BioException 

org.biojava.bio.BioException 
[INFO] ------------------------------------------------------------------------ 
[INFO] For more information, run Maven with the -e switch 
[INFO] ------------------------------------------------------------------------ 
[INFO] Total time: 2 minutes 22 seconds 
[INFO] Finished at: Wed Jan 26 11:06:28 CST 2011 
[INFO] Final Memory: 17M/42M 
[INFO] ------------------------------------------------------------------------ 
11:06:30,704 DEBUG JobClient2:134 - 2011-01-26 11:06:30 ShutdownHook started 
11:06:31,204 DEBUG JobClient2:134 - 2011-01-26 11:06:31 shutdown 
11:06:31,706 DEBUG JobClient2:134 - 2011-01-26 11:06:31 shutdown 
11:06:32,207 DEBUG JobClient2:134 - 2011-01-26 11:06:32 shutdown 
11:06:32,707 DEBUG JobClient2:134 - 2011-01-26 11:06:32 ShutdownHook completed