---
layout: post
title: Inferal installation
date: '2010-10-08 20:49:00'
tags:
- bio_informatics
---

Infernal 

* Infernal ("INFERence of RNA ALignment") is for searching DNA sequence databases for RNA structure and sequence similarities. 
* It is an implementation of a special case of profile stochastic context-free grammars called covariance models (CMs). 
* A CM is like a sequence profile, but it scores a combination of sequence consensus and RNA secondary structure consensus, so in many cases, it is more capable of identifying RNA homologs that conserve their secondary structure more than their primary sequence. 
* URL: http://infernal.janelia.org/ 

$ wget ftp://selab.janelia.org/pub/software/infernal/infernal.tar.gz 
$ gunzip infernal.tar.gz 
$ tar xvf infernal.tar 
$ cd infernal-1.0.2/ 
$ ./configure [--enable-mpi] 
$ make 
$ sudo make install 

Testing 

* Just running the 7 commands that are available with this package 

$ cmalign 
$ cmbuild 
$ cmcalibrate 
$ cmemit 
$ cmscore 
$ cmsearch 
$ cmstat 

* if it gives the standard usage message, then it is installed.