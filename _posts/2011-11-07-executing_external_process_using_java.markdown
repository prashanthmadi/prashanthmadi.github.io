---
layout: post
title: Executing external process using java
date: '2011-11-07 21:19:00'
tags:
- java
---

    Runtime rt=Runtime.getRuntime(); 
    Process x= rt.exec("ls -l"); 
    BufferedReader stdInput = new BufferedReader(new InputStreamReader(x.getInputStream())); 
    String s; 
    while ((s = stdInput.readLine()) != null) { 
      System.out.println(s); 
    }