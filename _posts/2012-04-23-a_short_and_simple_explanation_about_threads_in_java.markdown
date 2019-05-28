---
layout: post
title: A short and simple explanation about Threads in java
date: '2012-04-23 02:41:00'
tags:
- threads
- java
---

**Multi-tasking:**  it involves having multiple process (playing music and using text editor) -- Heavy weight 

**Multi-threading:** it involves having mulitple threads(in text editor editing and printing) -- Light Weight 

Creating a thread 

* Runnable Interface 
* Thread Class 


ex : 

    class B { 
     PSVM() { 
     A a_ref= new A(); 
     a_ref.UseThread(); 
     } 
    } 

**Using Runnable Interface**

Extend Runnable interface and use run method in it. 

    class A implements Runnable{ 
     public void UseThread(){ 
      Thread new_thread = Thread(this, "new thread"); 
      new_thread.start(); 
     } 

     private void run(){ 
     // some code 
      } 
    } 

**Using Thread Class**

    class A extends Thread { 
     public void UseThread(){ 
      start(); 
     } 

     private void run(){ 
     // some code 
     } 
    } 

* its better to implement runnable 

**Multiple Threads**

    class B{ 
     PSVM(){ 
      A a_ref= new A(); 
      a_ref.UseThread("one"); 
      a_ref.UseThread("two"); 
      a_ref.UseThread("three"); 
     } 
    } 

    class A implements Runnable{ 
    public void UseThread(String threadname){ 
     Thread new_thread = Thread(this, threadname); 
     new_thread.start(); 
    } 

     private void run() { 
       // some code 
     } 
    } 

**using isalive and join methods**

    // Using join() to wait for threads to finish. 
    class NewThread implements Runnable { 
     String name; // name of thread 
     Thread t; 
     NewThread(String threadname) { 
     name = threadname; 
     t = new Thread(this, name); 
     System.out.println("New thread: " + t); 
     t.start(); // Start the thread 
    } 

    // This is the entry point for thread. 
    public void run() { 
     try { 
      for(int i = 5; i > 0; i--) { 
      System.out.println(name + ": " + i); 
      Thread.sleep(1000); 
      } 
    } catch (InterruptedException e) { 
    System.out.println(name + " interrupted."); 
    } 
    System.out.println(name + " exiting."); 
    } 
    } 

    class DemoJoin { 
    public static void main(String args[]) { 
    NewThread ob1 = new NewThread("One"); 
    NewThread ob2 = new NewThread("Two"); 
    NewThread ob3 = new NewThread("Three"); 
    System.out.println("Thread One is alive: "+ ob1.t.isAlive());
    System.out.println("Thread Two is alive: "+ ob2.t.isAlive());
    System.out.println("Thread Three is alive: "+ ob3.t.isAlive());
    // wait for threads to finish
    try {
        System.out.println("Waiting for threads to finish.");
        ob1.t.join();
        ob2.t.join();ob3.t.join();
    } catch (InterruptedException e) {
    System.out.println("Main thread Interrupted");
    }
    System.out.println("Thread One is alive: "+ ob1.t.isAlive());
    System.out.println("Thread Two is alive: "+ ob2.t.isAlive());
    System.out.println("Thread Three is alive: "+ ob3.t.isAlive());
    System.out.println("Main thread exiting.");
    }
    } 

Do synchronize with  synchronized keyword or use synchrnoized(object) {  // some code }