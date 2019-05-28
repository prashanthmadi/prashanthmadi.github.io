---
layout: post
title: installing blast
date: '2010-10-08 20:47:00'
tags:
- bio_informatics
---

Steps to download and install BLAST 

* Visit the URL: ftp://ftp.ncbi.nih.gov/blast/executables/release/. 
* Click on 'LATEST' to get the latest version of BLAST. 
* Right click on the version and 'Copy link address'. 
* On the server, type wget and paste the url 

$ wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/release/release/2.2.24/blast-2.2.24-x64-linux.tar.gz 
$ tar zxvf blast-2.2.24-x64-linux.tar.gz 
$ cd blast-2.2.24/bin 
$ ls 
bl2seq blastall blastclust blastpgp copymat fastacmd formatdb formatrpsdb impala makemat megablast rpsblast seedtop