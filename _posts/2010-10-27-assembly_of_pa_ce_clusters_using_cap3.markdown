---
layout: post
title: 'Assembly of PaCE clusters using CAP3 :'
date: '2010-10-27 16:30:00'
tags:
- bio_informatics
---

This is a wrapper script for running CAP3 assembly on each of the PaCE cluster. 
This package does NOT include the "cap3" executable. 
If CAP3 is not available, it can be obtained by mailing 
Dr.Xiaoqiu Huang (xqhuang@cs.iastate.edu). 

For the scripts to work, the CAP3 executable ("cap3") should be 
present in the directory PaCE-pipeline/CAP3-assembly/ or in the path of the system. 

PS: 
Although the scripts are for running CAP3 as the assembly tool, 
they can be easily modified accordingly to enable usage of alternative assembly tools. 
The only script to be modified for this purpose 
is "PaCE-pipeline/CAP3-assembly/caploop". 

Input: 
------- 
Must have generated the cluster file using PaCE. 
For illustration, 
- let the organizm be denoted by "tEST", 
- let the FASTA data file be "tEST.data" 
(PS: this is the original data file - NOT the PaCE preprocessed version), 
- let the PaCE cluster file be denoted by "estClust.500.3.PaCE". 

Output: 
-------- 
CAP3 assembly output for each of the PaCE cluster in estClust.500.3.PaCE. 

Steps for Assembly: 
------------------- 

To start with, the following steps assumes the PaCE cluster file (estClust.500.3.PaCE) is 
in the directory PaCE-clustering. 

- From PaCE-pipeline directory: 
cd CAP3-assembly 

- mkdir tEST 

- cp estClust.500.3 tEST/tEST 
ie., copy the PaCE cluster file (from its current location) to the file named "tEST" inside the newly created directory 

- You can use the perl script: 
perl extractCF.pl tEST/tEST tEST.data 

This step will create one FASTA data file corresponding to each PaCE cluster for tEST. 

- rm tEST/tEST 
ie., Remove the cluster file from the tEST folder - so that now it has only 
the data files corresponding to each PaCE cluster 

- caploop tEST 
This script runs CAP3 on each of the FASTA data file present in the tEST folder, 
generating the CAP3 output for each in the same folder. 
This is the only script that requires modification if in case the assembly 
tool is NOT CAP3.