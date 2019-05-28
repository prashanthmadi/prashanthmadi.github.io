---
layout: post
title: Reading  styled data from String.xml - Android
date: '2013-03-06 02:35:00'
tags:
- android
---

    <string name="my_text"> <![CDATA[ <b>Autor:</b>Prashanth Madi<br/> <b>Contact:</b>prm0080@gmail.com<br/> <i>Copyright © 2012-2013 </i> ]]></string> 

From our Java code we could now utilize it like this:

    TextView tv = (TextView);
    findViewById(R.id.myTextView);tv.setText(Html.fromHtml(getString(R.string.my_text)));