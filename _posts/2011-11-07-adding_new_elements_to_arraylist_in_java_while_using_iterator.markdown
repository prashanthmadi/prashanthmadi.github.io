---
layout: post
title: Adding new elements to arraylist in java while using iterator
date: '2011-11-07 09:44:00'
tags:
- java
---

Today i had a problem with usage of arraylist along side of iterator. the problem was that i was unable to add elements to the arraylist. it gives you an error java.util.ConcurrentModificationException this is because u cant add elements to an arraylist while using an iterator. so i had used listiterator as below. 

    import java.util.ArrayList;
    import java.util.ListIterator;
    public class Test { 
        public static void main(String args[]) { 
            ArrayList array_test= new ArrayList(); 
            array_test.add("a"); 
            array_test.add("k"); 
            array_test.add("d"); 
            array_test.add("s"); 
            array_test.remove("d"); 
            int i=1; 
            for(ListIterator it=array_test.listIterator();it.hasNext();) {
                 String link=it.next(); 
                if(i==1) {
                 it.add("r"); 
                 it.previous(); 
                 it.add("kk"); 
                 it.previous(); 
                 i++;
                } 
                System.out.println(link); 
            } 
        System.out.println("Contents of arrays list "+array_test); 
        } 
    }

In the above code i had used **it.previous** whenever i used **it.add**. this is because i want to use the added value in the loop again. while the addition of new element in array is added just before next element in arraylist.