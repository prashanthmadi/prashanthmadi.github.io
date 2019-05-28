---
layout: post
title: Handling Volley Request when Network Connection is slow
date: '2016-09-28 04:23:00'
tags:
- android-2
- volley
---


Volley makes more than one call to same API, if the network is slow that gives misleading results. To avoid this scenario add setRetryPolicy flag before adding request to volley queue. 

**RetryPolicy** is an interface where you need to implement your logic of how you want to retry a specific request when a timeout happens. 
It has three parameters

* Timeout – Can specify Socket Timeout in milliseconds per every retry attempt.
* Number of retries – Number of times retry is attempted. Default is set to ‘1’.
* Back off Multiplier – A multiplier that is used to determine exponential time set to socket for     every retry attempt.

Ex: 
```
JsonObjectRequest jsonObjReq = new JsonObjectRequest(………….); 
jsonObjReq.setRetryPolicy(new DefaultRetryPolicy(0,DefaultRetryPolicy.DEFAULT_MAX_RETRIES,DefaultRetryPolicy.DEFAULT.BACKOFF_MULT)); 
SingletonClass.getInstance.addToRequestQueue(jsonObjReq);
```