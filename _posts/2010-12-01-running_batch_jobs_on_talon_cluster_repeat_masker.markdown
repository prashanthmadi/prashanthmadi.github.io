---
layout: post
title: running batch jobs on talon cluster  ---->  RepeatMasker
date: '2010-12-01 19:25:00'
tags:
- bio_informatics
---

#!/bin/bash 
DIR=/users/prm0080/RepeatMasker/RepeatMasker/HMP_Bacteria_ContigCombine2 
J=0 
K=1 
for i in $DIR/* 
do 
files[$J]=$i 
let J=$J+$K 
done 
#BSUB -J "jobArray[1-560]" 
#BSUB -n 1 
#BSUB -M 2 
#BSUB -e mothur.%J.err output error file; %J=job number 
# $LSB_JOBINDEX 
#Run the application 
/users/prm0080/RepeatMasker/RepeatMasker/RepeatMasker ${files[$LSB_JOBINDEX]} -dir $DIR/suresh/