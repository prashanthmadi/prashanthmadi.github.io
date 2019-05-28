---
layout: post
title: installing repeatmasker
date: '2010-09-27 17:46:00'
tags:
- bio_informatics
---

there are few pre-requisite things to install repeatmasker.. 

repeatmasker is the first step involved in the est assembly pipeline 

the prerequisites are 

----perl 
----sequence search engine 

you can install one of the three search engines present 

-cross-match 

-rm blast  ( i am using this one)  http://www.repeatmasker.org/RMBlast.html 

-abblast/wublast (these requires licensing ) 

Try 1\. Download pre-compiled versions 

$ wget http://www.repeatmasker.org/rmblast-1.2-ncbi-blast-2.2.23+-x64-linux.tar.gz 
$ tar zxvf rmblast-1.2-ncbi-blast-2.2.23+-x64-linux.tar.gz 
$ cd rmblast-1.2-ncbi-blast-2.2.23+ 
$ cd bin 
$ ./rmblastn 
./rmblastn: error while loading shared libraries: libpcre.so.0: cannot open shared object file: 
No such file or directory 

I am unable to install this library. Things i found out, i may be wrong 

* libpcre is part of the 32-bit libraries 
* on ubuntu i was unable to find the library, maybe because of the repository. 

Try 2\. Download RMBlast source 

$ wget http://www.repeatmasker.org/rmblast-1.2-ncbi-blast-2.2.23+-src.tar.gz 
$ tar zxvf rmblast-1.2-ncbi-blast-2.2.23+-src.tar.gz 
$ cd rmblast-1.2-ncbi-blast-2.2.23+-src/c++ 
$ ./configure --with-mt --prefix=/usr/local/rmblast --without-debug 
$ make 
$ sudo make install 

This installed good without any problem Modify ~/.bashrc to include the line below 

export PATH=$PATH:/usr/local/rmblast/bin 

To check installation 

$ source ~/.bashrc 
$ rmblastn 
BLAST query/options error: Either a BLAST database or subject sequence(s) must be specified 

If you get the above message then RMBlast is installed 

---- tanden repeat finder (trf) is needed 

The TRF download will contain a single executable file. You will need to rename the file from whatever it is to just 'trf' (all lower case). Make TRF executable by typing chmod +x+u trf. You can then move this file wherever you want. I just put it in the /RepeatMasker directory. 

the next step is installing repeat database...... it takes 2 days to get registered soo temporarily this process would be out of service................. 

after 1 day.......... 

----Repeatmasker database 

* url: http://www.repeatmasker.org/RMDownload.html 
* download latest release version 

$ cd /usr/local 
$ wget http://www.repeatmasker.org/RepeatMasker-open-3-2-9.tar.gz 
$ tar zxvf RepeatMasker-open-3-2-9.tar.gz 

* It requires RepeatMasker Libraries 
o url: http://www.girinst.org/ 
o Go to Downloads > RepeatMasker libraries > RepeatMasker edition: local: 

$ tar zxvf repeatmaskerlibraries-20090604.tar.gz 
$ rm -rf repeatmaskerlibraries-20090604.tar.gz 
$ mv Libraries/RepeatMaskerLib.embl /usr/local/RepeatMasker/Libraries/. 

download RepeatMasker 
unpack it 
install RepeatMasker libraries..copy them into RepeatMasker main folder 

now configure the RepeatMasker script by using 
perl ./configure 

while configuring it would ask for so many where abouts ?? 
perl path 
trf path 

after finishing installation 
check whether its working or not by typing the command 

RepeatMasker in terminal..