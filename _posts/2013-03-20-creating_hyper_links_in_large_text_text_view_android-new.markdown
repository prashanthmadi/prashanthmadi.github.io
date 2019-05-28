---
layout: post
title: Creating HyperLinks in Large Text (TextView) - Android
date: '2013-03-20 22:23:00'
previewimg: '/content/images/2017/09/android-app-banner.jpg'
tags:
- android
---

### String.xml

------------ 
```
<string name="totalText">Hello <u>World</u></string> 
```

``` 
public void hyperlinkWordsInText() 
{ 

Spanned sequence = html.fromhtml (context.getstring (r.string.totalText)); 

Spanablestringbuilder strbuilder = new Spanablestringbuilder(sequence); 

Underlinespan [] underlines = strbuilder.getspans (0, sequence.length (), Underlinespan.class); 

For (Underlinespan span : underlines) 

{ 

int start = strBuilder.getSpanStart(span); 

int end = strBuilder.getSpanEnd(span); 

int flags = strBuilder.getSpanFlags(span); 

ClickableSpan myActivityLauncher = new ClickableSpan() 

{ 

public void onClick(View view) 

{ 

// do wat ever u want on click 

} 

}; 

strBuilder.setSpan(myActivityLauncher,start,end,flags); 

} 
txt.setText(strBuilder); 
txt.setMovementMethod(LinkMovementMethod.getInstance()); 
}
```