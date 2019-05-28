---
layout: post
title: google maps v2 illegalStateException
date: '2013-06-19 06:41:00'
tags:
- android
---

java.lang.<wbr style="background-color: white; color: #222222; font-family: Arial, Helvetica, sans-serif;">IllegalStateException: Not connected. Call connect() and wait for onConnected() to be called. 

This happens when you request for locationupdates before the actual location connection is established. Instead use a boolean variable to check if connection is established or call for locationupdates as below in onConnected. 

<table id="src_table_0" style="background-color: white; border-collapse: collapse; color: black; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Lucida Console', monospace; font-size: 12px; margin: 0px; padding: 0px; white-space: pre;">

<tbody style="margin: 0px; padding: 0px;">

<tr id="sl_svn984a069687e7a2239593d188527e1ade2bb9a1a0_230" style="margin: 0px; padding: 0px;">

<td class="source" style="margin: 0px; padding: 0px 0px 0px 4px; vertical-align: top; white-space: pre-wrap;">@Override 
</td>

</tr>

<tr id="sl_svn984a069687e7a2239593d188527e1ade2bb9a1a0_231" style="margin: 0px; padding: 0px;">

<td class="source" style="margin: 0px; padding: 0px 0px 0px 4px; vertical-align: top; white-space: pre-wrap;">        public void onConnected(Bundle connectionHint) { 
</td>

</tr>

<tr id="sl_svn984a069687e7a2239593d188527e1ade2bb9a1a0_232" style="margin: 0px; padding: 0px;">

<td class="source" style="margin: 0px; padding: 0px 0px 0px 4px; vertical-align: top; white-space: pre-wrap;">                Toast.makeText(this, "Connected", Toast.LENGTH_SHORT).show(); 
</td>

</tr>

<tr id="sl_svn984a069687e7a2239593d188527e1ade2bb9a1a0_233" style="margin: 0px; padding: 0px;">

<td class="source" style="margin: 0px; padding: 0px 0px 0px 4px; vertical-align: top; white-space: pre-wrap;">                mLocationClient.requestLocationUpdates(mLocationRequest, this); 
</td>

</tr>

<tr id="sl_svn984a069687e7a2239593d188527e1ade2bb9a1a0_237" style="margin: 0px; padding: 0px;">

<td class="source" style="margin: 0px; padding: 0px 0px 0px 4px; vertical-align: top; white-space: pre-wrap;">        }</td>

</tr>

</tbody>

</table>

example code 
[https://code.google.com/p/where-is-my-car/source/browse/src/com/prashanth/whereismycar/LocaterMapActivity.java](https://code.google.com/p/where-is-my-car/source/browse/src/com/prashanth/whereismycar/LocaterMapActivity.java)