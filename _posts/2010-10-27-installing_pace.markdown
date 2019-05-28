---
layout: post
title: installing Pace
date: '2010-10-27 16:58:00'
tags:
- bio_informatics
---

Run the "make" command from the shell. 

(For system specific MPICH and C compilers modify the MakeFile appropriately.) 
After successful build, copy the executables into the folder: 

cp PreprocessPaCE.pl PaCE-pipeline/PaCE-clustering 
cp PaCE PaCE-pipeline/PaCE-clustering 

Checklist for a successful build: 
- Executables created: PaCE 
- No fatal errors or "serious" warnings flagged by the compiler (minor wa$ 
- The mk uses O3 optimization level. If this high level is not 
supported by the C compiler being used, change it to a lower level 
like O2 or O1 or O0 as appropriate.