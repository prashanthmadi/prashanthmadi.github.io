---
layout: post
title: Push Notifications using FCM
date: '2017-09-15 05:40:48'
previewimg: '/content/images/2017/09/android-firebase-cloud-messaging.png'
tags:
- kotlin
- android
- firebase-cloud-messaging
- fcm
- push-notifications
---

Firebase cloud messaging is cross platform which supports Android, iOS and mobile wep applications.

Create new android studio project.

Log in to FCM console. Create or Add a project.

![Screen-Shot-2017-09-14-at-11.56.46-PM](/content/images/2017/09/Screen-Shot-2017-09-14-at-11.56.46-PM.png)

Give the project name & select the country

![Screen-Shot-2017-09-14-at-11.58.52-PM](/content/images/2017/09/Screen-Shot-2017-09-14-at-11.58.52-PM.png)

Select "Add Firebase to your android app"

![Screen-Shot-2017-09-15-at-12.01.01-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.01.01-AM.png)

Give your app package name and click on Register App.

![Screen-Shot-2017-09-15-at-12.02.16-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.02.16-AM.png)

Then you will receive **google-services.json file**. 

Navigate to android app folder and paste **google-services.json**.

![Screen-Shot-2017-09-15-at-12.08.22-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.08.22-AM.png)

Add the following code to the root level build.gradle file.

![Screen-Shot-2017-09-15-at-12.13.46-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.13.46-AM.png)
In the app level build.gradle add the plugin for **google-services**

![Screen-Shot-2017-09-15-at-12.12.00-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.12.00-AM.png)
Declare Activity & intent fliters to AndroidManifest.xml

![Screen-Shot-2017-09-15-at-12.25.07-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.25.07-AM.png)
Create a class called FirebaseIdService and get the registration token.

![Screen-Shot-2017-09-15-at-12.16.06-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.16.06-AM.png)
Add following lines of code to handle notification using Broadcast Receiver.

![Screen-Shot-2017-09-15-at-12.18.43-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.18.43-AM.png)
On Launch of MainActivity.kt register Broadcast receiver to check if we have any push notifications and unregister to release the resources. Also design the notification style.

![Screen-Shot-2017-09-15-at-12.21.20-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.21.20-AM.png)

From FCM console, select the created app  
Select **Notifications** option from navigation menu.

![Screen-Shot-2017-09-15-at-12.27.58-AM-1](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.27.58-AM-1.png)

Then select New Message and enter the message title and content and finally click on Send Message buton.

![Screen-Shot-2017-09-15-at-12.30.53-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.30.53-AM.png)
![Screen-Shot-2017-09-15-at-12.38.10-AM](/content/images/2017/09/Screen-Shot-2017-09-15-at-12.38.10-AM.png)


