---
layout: post
title: installing TRNAscan-SE
date: '2010-10-08 20:47:00'
tags:
- bio_informatics
---

TRNAscan-SE 

* tRNAscan-SE is a program for improved detection of transfer RNA genes in genomic sequence. 
* URL: http://lowelab.ucsc.edu/tRNAscan-SE/ 

[edit] Installation 

* Get the link location 

$ wget http://lowelab.ucsc.edu/software/tRNAscan-SE.tar.gz 
$ cd tRNAscan-SE-1.23/ 

* Edit Makefile to provide the following details 

## where you want things installed 
BINDIR = /usr/local/bin 
LIBDIR = /usr/local/lib/tRNAscan-SE 
MANDIR = /usr/local/man 

If you dont change the above path it will install in your home directory $HOME 

* Now make the package 

$ make 
.. 
.. 
sqio.c:238: error: conflicting types for ‘getline’ 
/usr/include/stdio.h:651: note: previous declaration of ‘getline’ was here 
make: *** [sqio.o] Error 1 
.. 

* The make did not complete because, there were 2 getline subroutines in 2 different files 
* Solution: 
o Checked if getline is present in any of the *.c files in this directory 
o opened sqio.c and changed all the getline to getLine 

$ make 

make ran with no error. 

NOTE: 

* there are some instructions at the end of make. It requires us to run source setup.tRNAscan-SE; rehash for the current session 
* Or include a line source /home/krevanna/Desktop/TOOL_TEST/tRNAscan-SE-1.23/setup.tRNAscan-SE in ~/.cshrc 
* This wont work because we are in bash shell and it expects us to be in C-shell 

* I did not follow the above instructions and i went ahead with make install 

$ sudo make install 
$ make testrun 
$ make clean