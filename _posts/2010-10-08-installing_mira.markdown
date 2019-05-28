---
layout: post
title: installing mira
date: '2010-10-08 20:43:00'
tags:
- bio_informatics
---

* download url: http://sourceforge.net/projects/mira-assembler/files/ 
* version: 3.2.0 

$ wget http://sourceforge.net/projects/mira-assembler/files/MIRA/V3.2.0/mira_3.2.0_prod_linux-gnu_x86_64_static.tar.bz2/download 
$ bunzip2 mira_3.2.0_prod_linux-gnu_x86_64_static.tar.bz2 
$ tar xvf mira_3.2.0_prod_linux-gnu_x86_64_static.tar 
$ cd mira_3.2.0_prod_linux-gnu_x86_64_static/ 

* All the executables are in bin directory 
* Export the path to bin to bashrc 

$ vim ~/.bashrc 
export PATH=$PATH:/path/to/mira/bin 
$ source ~/.bashrc 
$ mira 
... 

[edit] Instructions 

* Open the index.html file present in docs folder on firefox. 

[edit] Usage 

mira \ 
[-project=<name>] 
[--job=arguments] 
[-fasta[=<filename>] | -fastq[=<filename>] | -caf[=<filename>] | -phd[=<filename>]] [-notraceinfo] [-noclipping[=...]] [-highlyrepetitive] [-lowqualitydata] [-highqualitydata] [-params=<filename>] [-GENERAL:arguments] 
[-STRAIN/BACKBONE:arguments] 
[-ASSEMBLY:arguments] 
[-DATAPROCESSING:arguments] 
[-CLIPPING:arguments] 
[-SKIM:arguments] 
[-ALIGN:arguments] 
[-CONTIG:arguments] 
[-EDIT:arguments] 
[-MISC:arguments] 
[-DIRECTORY:arguments] 
[-FILENAME:arguments] 
[-OUTPUT:arguments] 
[COMMON_SETTINGS | SANGER_SETTINGS | 454_SETTINGS | SOLEXA_SETTINGS | SOLID_SETTINGS] 

ESTs (simulated) 

* Generate a genome of 1,000,000 length 
* Generated ESTs of length 500-800 bp for the above genome 
* Around 10,000 ESTs were generated and stored in the file est.fasta 

$ mira --project=EST --job=denovo,genome,normal,454 -fasta=est.fasta -SK:mnr=yes:nrr=10 454_SETTINGS -LR:wqf=no -LR:mxti=no -AS:epoq=no >&log_assembly.txt 
$ cd EST_assembly/ 
$ ls -R 
.: 
EST_d_chkpt EST_d_info EST_d_log EST_d_results 

./EST_d_chkpt: 
passInfo.txt readpool.maf 

./EST_d_info: 
EST_info_assembly.txt EST_info_consensustaglist.txt EST_info_contigstats.txt EST_info_readrepeats.lst 
EST_info_callparameters.txt EST_info_contigreadlist.txt EST_info_debrislist.txt EST_info_readtaglist.txt 

./EST_d_log: 
EST_error_reads_invalid EST_info_reads_tooshort EST_out_pass.2.caf 
EST_info_consensustaglist.1.txt EST_info_readtaglist.1.txt EST_out_pass.3.caf 
EST_info_consensustaglist.2.txt EST_info_readtaglist.2.txt EST_readpoolinfo.lst 
EST_info_consensustaglist.3.txt EST_info_readtaglist.3.txt hashstat.bin 
EST_info_contigreadlist_pass.1.txt EST_int_clippings.0.txt miralog.ads_pass.4.adsfacts 
EST_info_contigreadlist_pass.2.txt EST_int_normalisedskims_pass.4.bin miralog.ads_pass.4.adsfacts.pclusters 
EST_info_contigreadlist_pass.3.txt EST_int_posmatchc_pass.4.lst miralog.ads_pass.4.complement 
EST_info_contigstats_pass.1.txt EST_int_posmatchc_pass.4.lst.reduced miralog.ads_pass.4.forward 
EST_info_contigstats_pass.2.txt EST_int_posmatchf_pass.4.lst miralog.ads_pass.4.reject 
EST_info_contigstats_pass.3.txt EST_int_posmatchf_pass.4.lst.reduced miralog.noqualities 
EST_info_debrislist_pass.1.txt EST_int_posmatch_megahubs_pass.4.lst miralog.usedids 
EST_info_debrislist_pass.2.txt EST_int_posmatch_multicopystat_preassembly.0.txt 
EST_info_debrislist_pass.3.txt EST_out_pass.1.caf 

./EST_d_results: 
EST_out.ace EST_out.maf EST_out.padded.fasta.qual EST_out.unpadded.fasta EST_out.wig 
EST_out.caf EST_out.padded.fasta EST_out.tcs EST_out.unpadded.fasta.qual 

[edit] Inference 

* Snippet of some of the information in EST_d_info/EST_info_assembly.txt 

.. 
.. 
Length assessment: 
------------------ 
Number of contigs: 106 
Total consensus: 944829 
Largest contig: 36580 
N50 contig size: 13625 
N90 contig size: 5366 
N95 contig size: 2945 
.. 
.. 

* Number of contigs in EST_out.unpadded.fasta and EST_out.padded.fasta 

$ grep -c '>' ./EST_d_results/EST_out.unpadded.fasta 
107</filename></filename></filename></filename></filename></name>