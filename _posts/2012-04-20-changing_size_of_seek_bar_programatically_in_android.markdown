---
layout: post
title: Changing Size of SeekBar programatically in android
date: '2012-04-20 21:36:00'
tags:
- android
---

I had a scienario to change size of seekbar by changing the visibility of surrounding views. Took a while but below is small code snipped which may be helpful for sme1... 

    RelativeLayout.LayoutParams abc=new RelativeLayout.LayoutParams(526,30); 
    abc.addRule(RelativeLayout.CENTER_VERTICAL);
    abc.addRule(RelativeLayout.RIGHT_OF,R.id.pause); 
    mSeekBar.setLayoutParams(abc); 