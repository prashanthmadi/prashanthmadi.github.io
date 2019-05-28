---
layout: post
title: running pace new method
date: '2010-10-29 21:01:00'
tags:
- bio_informatics
---

Step 1\. generate datafile with n sequences 

head -n*2 original.fsa > small_sample.fsa 

Step 2\. run preprocess 

./preprocessPaCE 5k.fsa 1 

Step 3\. run GItitle.pl 

./GItitle.pl 5k.fsa.PaCE > 5k.GI.fsa 

Step 4\. run PaCE 

#!/bin/csh 
#@ job_type = parallel 
#@ class = LONG 
#@ account_no = NONE 
#@ node = 2 
#@ tasks_per_node = 4 
#@ checkpoint = no 
#@ wall_clock_limit = 05:00:00 
#@ error = $(Executable).$(Cluster).err 
#@ output = $(Executable).$(Cluster).out 
#@ environment = COPY_ALL 
#@ queue 

llmachinelist 
mpirun -v -np 8 -machinefile /tmp/machinelist.$LOADL_STEP_ID ./PaCE_v9 
/N/gpfs/cap3/leesangm/HumanMRNA/split1mil/5k.GI.PaCE 5000 
./Phase.cfg 

llsubmit submitTest.sh 

Step 5\. split PaCE output 

./PaCEclusterFasta.pl test.fsa estClust.5000.3.PaCE 

##### 
Notes 

1\. Pace: How to run 

mpirun -v -np 8 ./PaCE /N/gpfs/cap3/leesangm/HumanMRNA/example5K/5k.GI.fsa 5000 ./PaCE.cfg