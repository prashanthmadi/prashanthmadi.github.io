---
layout: post
title: installing diya
date: '2010-10-08 20:44:00'
tags:
- bio_informatics
---

* Download url: http://sourceforge.net/projects/diyg/ 

$ tar zxvf diya-1.0-rc4.tar.gz 
$ cd diya-1.0-rc4/ 

[edit] Prerequisites 

* Perl Modules (How to check Perl module) 
o Bioperl 
o Data::Merger 
o Getopt::Long 
o FileHandle 
o XML::Simple 
o File::Basename 
* Software 
o Perl (>= 5.8) 
o MUMmer v3.20 
o Glimmer v3.02 
o BLAST 
o tRNAscan-SE v1.23 
o Infernal v0.81 
o rfamscan.pl v0.1 
* Database 
o UniRef50 (refer to Others) 
o Protein Clusters (refer to Others) 

[edit] Installation 

* Steps to install 

$ perl Makefile.PL 
$ make 
$ sudo make install