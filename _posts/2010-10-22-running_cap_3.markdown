---
layout: post
title: Running cap3
date: '2010-10-22 21:10:00'
tags:
- bio_informatics
---

after installing cap3 

just take a sequence file and use the following terminal at command prompt 

> cap3 filename [options] 

you can specify constraints and qual 

CAP3 takes as input a file of sequence reads in FASTA format. If the names of reads contain a dot ('.'), CAP3 requres that the names of reads sequenced from the same subclone contain the same substring up to the first dot. CAP3 takes two optional files: a file of quality values 
in FASTA format and a file of forward-reverse constraints. 

The file of quality values must be named "xyz.qual", and the file of forward-reverse constraints must be named "xyz.con", where "xyz" is the name of the sequence file. 

my work involved 

input 
----- 
>cap3 seq 

seq is the file consisting of some sequence of data... 

output 
------ 
6 files 

seq.cap.ace 
seq.cap.contigs.links 
seq.cap.info 
seq.cap.contigs 
seq.cap.contigs.qual 
seq.cap.singlets 

seq.cap.ace 
----------- 

AS 1 5 

CO Contig1 1422 5 11 U 
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNAGTTTT 
AGTTTTCCTCTGAAGCAAGCACACCTTCCCTTTCCCGTCTGTCTATCCATCCCTGACCCT 
GTTGTCTGTCTATCCCTGACCCCGTAGTCTCCTAAGTCGCCCCAGATTTTGTGAACACCC 
TCTGGAACTAGAATCTAGTGGGCGGATGGACCATTTACTAGACGGAGGTAGAGGTGGGTG 
GATGCGAACGACAGGGTGCATAGTCAGCCCGGTTTTAAGGGCAGGTCACTTGGTAGGTCA 
GCAGGCGGGTCAGTGGGCGGGTGCCTGCAGCATTTATGAACTTATTTGGCCCAGCAAACA 
TTTTGAGTGTCAGGCCGTGCCTACCCAAGGTGAGGGTAAGGAGCAAAATCAGCCCAGCCC 
AGAGCACTGGGTGGCTACACAGAGCCGACCTCTAATGTGCGCTCCGGGTCGGGATGGCAC 
TCAGCTCGCCTTTAGGGAGTGATGATCTGGATGCCTGGCTTGGAGGTGACAGAGCCTGCC 
CTTATGAGACAATTAAGAGACTGACTAAGCACCCGGCAGGAGGCCACGAGAATCCCCATG 
TGAGAAAGAAGAGCATAAACAGGAAACACATTTAATAATTAAACAAAGATAACTCCCTCG 
TGTGCGCGCACCGGGCCAGCCCCTATAGAAACATCTGAGGAGTCACTTCCTCCCATGACT 
CTCGCCCGCCCGGCCGGCTGGAGTCGGCTCCTGGCAAGCTTCAGGCACCTCAGTTGTCCT 
GAATACACACAGCACCCTTTCCTTACTGAAGCCCCTGAGAGCCTCCAGTTCTCCCTCCTT 

BQ 
10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 1$ 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 2$ 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 2$ 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 2$ 
20 20 20 20 20 20 20 5 5 5 20 2 

AF R3 U 1 
AF R1 U 44 
AF R2 U 1 
AF R4 C 478 
AF R6 C 571 
BS 1 248 R2 
BS 249 250 R3 
BS 251 849 R2 
BS 850 850 R3 
BS 851 974 R2 
BS 975 1155 R4 
BS 1156 1157 R6 
BS 1158 1159 R4 
BS 1160 1168 R6 
BS 1169 1242 R4 
BS 1243 1422 R6 

------------------------------------------------------------------- 
seq.cap.contigs.qual 
--------------------- 

>Contig1 
10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 
10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 
10 10 10 10 10 10 10 10 10 10 10 10 10 10 20 20 20 20 20 20 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 
20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 

a clear documentation is present about pace at the link below 

http://icb.med.cornell.edu/crt/CAP3/example_usage.xml