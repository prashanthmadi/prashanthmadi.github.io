---
layout: post
title: Close file handler in java while operating on files
date: '2011-11-08 06:54:00'
tags:
- java
---

I just bumped into one of the error with file io. if you dont close fie handler, it wont write anything into file. 

    import java.io.*;
    class FileWrite { 
    public static void main(String args[]) { 
      try{ 
        // Create file 
        FileWriter fstream = new FileWriter("out.txt"); 
        BufferedWriter out = new BufferedWriter(fstream); 
        out.write("Hello Java"); 
        //Close the output stream 
        out.close(); 
    }catch (Exception e){
    //Catch exception if any 
    System.err.println("Error: " + e.getMessage());
    } 
    }
    }