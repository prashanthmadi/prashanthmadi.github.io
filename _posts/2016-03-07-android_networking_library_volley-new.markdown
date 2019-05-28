---
layout: post
title: Android Networking Library - Volley
date: '2016-03-07 05:34:00'
previewimg: '/content/images/2017/04/Android-Volley.jpg'
tags:
- android-2
- volley
---

####What is Volley? 

Volley is a library developed by Google, that makes easy and fast networking in Android. This library does put an end to writing lines of boiler plate code for consuming RESTful API. 

Volley handles networking calls asynchronously without again implementing separate AsyncTask with `doInBackground()` method. This approach is replacement for deprecated apache HttpClient library and HttpURLConnection. 

####Why Volley? 

Volley is embedded with extra features like 

1. Handles automatic scheduling of network requests. 
2. Provides Memory and Disk cache. 
3. Request prioritization. 
4. Can customize library as per requirement. 
5. Debugging and tracing tools. 
6. Cancelling the requests. (Can cancel single network request API or set of requests all together) 

####Steps to include library in the Android Project.
After creating a new project with some Blank Activity using Android studio. 

Include following line of code in build.gradle file under dependency section 

```
dependencies { 
  compile fileTree(dir: 'libs', include: ['*.jar']) 
  compile 'com.android.support:appcompat-v7:21.0.3' 
  compile 'com.mcxiaoke.volley:library-aar:1.0.0'
}
```

Make sure you include this piece of code in build.gradle file of **app Module section**.

####How to make a Simple Request using Volley?
Implement a singleton class with request queue, so that it can globally accessible through out the entire application.
```
RequestQueue queue = Volley. new RequestQueue(this);
```