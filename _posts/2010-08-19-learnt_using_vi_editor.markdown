---
layout: post
title: learnt using vi editor
date: '2010-08-19 16:55:00'
tags:
- misc
---

finding hard to install java with all of its apps.... 
unable to find jdk in my server....... its really makin me to think.... 

learning about vi editor.... 

* **Moving around with cursor:** 

h key = LEFT, l key = RIGHT, k key = UP, j key = DOWN
* **Exiting vim editor without saving:** 

press ESC to get into command mode, enter :q! to exit.
* **Deleting characters in vim command mode:** 

delete with x key

* **Inserting / appending text:** 

Press i or a in command mode and type
* **Saving changes and exit:** 

in command mode :wq or SHIFT+zz 

* **Deleting words:** 

delete word with d operator and w or e motion
* **Deleting to the end of the line:** 

delete to the end of the line with d operator and $ motion
* **Using operators, motions and counts:** 

beginning of the line 0, end of the line $, end of the 2nd word 2e beginning of the 4th word 4w

* **Deleting multiple words:** 

to delete 3 words you would use d3w
* **Deleting lines:** 

to delete single line dd, delete n lines ndd
* **Undo changes:** 

undo changes with u

http://www.linuxconfig.org/Vim_Tutorial