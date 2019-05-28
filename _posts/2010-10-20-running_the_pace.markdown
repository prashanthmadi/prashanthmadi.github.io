---
layout: post
title: Running the pace
date: '2010-10-20 17:18:00'
tags:
- bio_informatics
---

- cd PaCE-pipeline/PaCE-clustering 

- Preprocessing: 

This preprocessing step formats the input FASTA file and generates 
the corresponding input datafile for PaCE. 

Run the preprocessPaCE command to preprocess the EST input file (fasta format) 
eg., 
$ PreprocessPaCE.pl {FASTA data file} {1: prune PolyA/T, 0 otherwise} > tEST.data.PaCE 

If the second argument is : 
0: Does not modify the input sequences. Just concatenate each sequence 
such that each sequence appears in one line and also 
converts all DNA characters to upper case. 
1: In addition to the two effects produced by option '0' this option 
trims off streaks of As and Ts occurring at either ends 
of the sequence. This option is not required if the input FASTA 
GNU nano 1.2.5 File: PaCE-README 

sequences have already been stripped of poly As and Ts or if they 
they are required to be input. If you use this option, 
make sure you inspect manually some modifications to confirm 
there will be no negative impacts on the clustering. This inspection 
can be done by first running preprocessPaCE using flag 0 and then 
using flag 1 (both on the original file) and taking a diff of both 
the output files. 

eg., 
$ PreprocessPaCE.pl ../datafiles/tEST.data 0 > ../datafiles/tEST.data.PaCE 
This generates another file by name "tEST.data.PaCE" in ../datafiles/ . 

- Find "n": 
Find the number of sequences in the preprocessed output data file. 
Let us call it "n". 

This can be found by a simple unix command like: 
eg., grep -c ">" ../datafiles/tEST.data.PaCE 

ie., n=500 for ../datafiles/tEST.data.PaCE. 

- Parameterization: 
Parameters to PaCE are kept in the file PaCE.cfg. 
Check if PaCE.cfg is there in the directory of the executable. 

You typically do NOT need to change any parameters except "window". 

If the data size <=10,000 ESTs then a window size of 7 is recommended. If the data size <=30,000 and >=10,000 ESTs then a window size of 8 is recommended. 
Otherwise a window size of 9 is recommended. 

- Run PaCE: 
PaCE takes two parameters: 
Usage: {MPIRunCommand} PaCE {preprocessed FASTA datafile} {number of ESTs} 

(P.S: Number of processors should be AT LEAST 2) 

eg., 
$ mpirun -np 4 PaCE ../datafiles/tEST.data.PaCE 500 

where 4 is the number of processors to run on. 

"{MPIRunCommand}" depends on the available MPI implementation and job scheduler 
of the parallel cluster being used. 
For batch mode parallel platforms, use the specified batch submission routines like "qsub" or "llsubmit". 

- PaCE output: 

The results are of two categories: Run-time and Cluster results. 
A summary of these results are printed on the standard output. If the parallel platform 
uses batch processing which outputs the standard output to a file, then the summary 
will be present in that file. 

(i) Run-time results: 

The total run-time and the run-time in different components of the system 
is shown for each SLAVE processor. This indicates the total run-time for PaCE clustering. 

For eg., 

Time taken by slave 1 : Load<0> + Preprocessing Phase<3> + Clustering Phase<1>= 5 secs 

Here processor rank 1 took a total of 5 seconds to complete with the run-times in phases 
indicated separately. The numbers are truncated to integer values. 
Almost all the slave processors take the same amount of total 
run-time. Also the time to load the data file into memory 
indicated by Load<> first might vary with systems and as it is the 
time for initialization, subtracting it from the total run-time 
tells the actual time taken by the software. 

(ii) Clustering results: 

The standard output will also have something like this: 

Master: #Clusters Output:= 357 #Singletons=258 
Master: #Contained ESTs:= 63 

This means: The total number of clusters generated is 357, out of which 258 are singletons. 
Also out of the n(=500) ESTs supplied, 63 ESTs are completely contained 
(with 100% identity) in other ESTs. 

The clusters themselves are located in file estClust.n.p.PaCE 
where n is the number of ESTs and p is the number of slave processors. 
eg., estClust.500.3.PaCE 
PS: The number of slave processors is always one less than the total 
number of processors used to run PaCE. 

The size distribution of these clusters (in the number of ESTs) is present 
in estClustSize.n.p.PaCE. 
eg., estClustSize.500.3.PaCE 
Each line is of the format "{Cluster#} {Number of Members in Cluster#}". 

The set of EST sequences which are contained in (an)other EST sequence(s) are 
indicated in ContainedESTs.n.PaCE. 
eg., ContainedESTs.500.PaCE 
Each line is of the format "{Contained EST sequence header} IN {Container EST sequence header}". 
PS: One EST can be contained in multiple EST sequences, and only one container 
sequence is indicated here. 
Also the set of contained ESTs reported need not comprise of all the ESTs 
that are actually contained. More specifically, the contained ESTs 
reported are only based on the set for which alignments were performed by PaCE. 

The set of EST sequences which are not contained in any other EST sequence in the 
provided data set is present in NonContainedESTs.n.PaCE. 
eg., NonContainedESTs.500.PaCE 

Adding clone mates information : 

-------------------------------- 

As additional input, PaCE is designed to take as input clone mates information. 
This information should be present in a file which should be present in 
the following format: 

>clone mate id # 
FASTA header for sequences belonging to this clone mate (each in separate lines) 
.... 

eg., Let the clone mates be in a file myCloneMates that looks like this: 

>CloneId1 
gi|19863109| 
gi|19800130| 
>CloneId2 
gi|19863111| 
gi|19800132| 
... 

Step 1: 

Run the following command (for the above example) : 
$perl formatCloneMates.pl myCloneMates tEST.data.PaCE > myCloneMates.PaCE 

This will generate the PaCE formatted myCloneMates.PaCE. 
(The numbers in each line indicates the sequence number that PaCE 
provides for each input sequence.) 

Step 2: 

The PaCE formatted clone mate file should be in the folder where the 
PaCE executable resides. 
To specify the clone mate file as input, it has to be provided in the PaCE.cfg file as: 

ClonePairsFile clonematefilename 

eg., 
ClonePairsFile myCloneMates.PaCE 

This has to be done before starting to execute PaCE. PaCE will put each 
set of sequences linked by the same clone mate id together in one cluster 
in its final output.a 

If you do not have any clone pairs information to provide then set: 

ClonePairsFile None 

PS: Both these steps should be performed for each input FASTA file (even 
if you intend to run for subsets of the original FASTA data file).