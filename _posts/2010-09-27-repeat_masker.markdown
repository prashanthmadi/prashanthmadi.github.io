---
layout: post
title: Repeat masker
date: '2010-09-27 16:15:00'
tags:
- bio_informatics
---

<table class="code">

<tbody>

<tr>

<td>5.  Install RepeatMasker. Download from http://www.repeatmasker.org</td>

</tr>

<tr>

<td> a.  The most current version of RepeatMasker requires a program called TRF.</td>

</tr>

<tr>

<td>      This can be downloaded from http://tandem.bu.edu/trf/trf.html</td>

</tr>

<tr>

<td>  b.  The TRF download will contain a single executable file.  You will need to</td>

</tr>

<tr>

<th id="L122">[ 
](http://malachite.genetics.utah.edu/projects/maker/browser/INSTALL#L122)</th>

<td>      rename the file from whatever it is to just 'trf' (all lower case).</td>

</tr>

<tr>

<th id="L123">[ 
](http://malachite.genetics.utah.edu/projects/maker/browser/INSTALL#L123)</th>

<td>  c.  Make TRF executable by typing chmod +x+u trf.  You can then move this file</td>

</tr>

<tr>

<td>      wherever you want.  I just put it in the /RepeatMasker directory.</td>

</tr>

<tr>

<td>  d.  Unpack RepeatMasker to the directory of your choice (i.e. /usr/local).</td>

</tr>

<tr>

<td>  e.  If you do not have WuBlast installed, you will need to install the program</td>

</tr>

<tr>

<td>      RMBlast.  We do not recomend using cross_match, as RepeatMasker</td>

</tr>

<tr>

<td>      performance will suffer.</td>

</tr>

<tr>

<td>  f.  Now in the RepeatMasker directory type perl ./configure in the command</td>

</tr>

<tr>

<td>      line. You will be asked to identify the location of perl, wublast, and</td>

</tr>

<tr>

<td>      trf.  The script expects the paths to the folders containing the</td>

</tr>

<tr>

<td>      executables (because you are pointing to a folder the path must end in a</td>

</tr>

<tr>

<td>      '/' character or the configuration script throws a fit).</td>

</tr>

<tr>

<td>  g.  Add the location where you installed RepeatMasker to your PATH variable in</td>

</tr>

<tr>

<td>      .bash_profile (i.e. export PATH="/usr/local/RepeatMasker:$PATH").</td>

</tr>

<tr>

<td>  h.  You must register at http://www.girinst.org and download the Repbase</td>

</tr>

<tr>

<td>      repeat database, Repeat Masker edition, for RepeatMasker to work.</td>

</tr>

<tr>

<td>  i.  Unpack the contents of the RepBase tarball into the RepeatMasker/Libraries</td>

</tr>

<tr>

<td>      directory.</td>

</tr>

</tbody>

</table>