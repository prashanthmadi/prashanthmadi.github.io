---
layout: post
title: Getting started with React-Native App and Parse
date: '2017-03-26 02:05:00'
previewimg: '/content/images/2017/03/react_native.png'
tags:
- react-native
- redux
- parse
- redux-saga
---

**React Native** lets you build mobile apps using only JavaScript. With React Native, you don't build a “mobile web app”, an “HTML5 app”, or a “hybrid app”. You build a real mobile app that's indistinguishable from an app built using Objective-C or Java.

#### Getting Started

*Update 03/21/17: Creating React-native app has got simple now using create-react-native-app cli. Refer [Link](https://facebook.github.io/react-native/blog/2017/03/13/introducing-create-react-native-app.html)*

* Install and create a sample app following below link
https://facebook.github.io/react-native/docs/getting-started.html#content

If you haven't tried android development earlier, try to use [GenyMotion](https://www.genymotion.com/) as emulator.

Below is a bare minimum app with login and sign-up screens backed by parse server 
https://github.com/prashanthmadi/react-native-login-signup-sample

#### What modules should i use ?

Awesome react-native has curated list of awesome resources 
https://github.com/jondot/awesome-react-native

Below are the modules i have used for my project(involves Forms and makes outbound calls to Parse Server). You can find my app @ https://github.com/prashanthmadi/Badi-mobile


#### Navigation
* react-native-router-flux [Link](https://www.npmjs.com/package/react-native-router-flux)


#### Redux and it's relatives(to maintain global state)
* redux
* react-redux
* redux-saga (alternative: redux-thunk)
* redux-logger

#### Forms
* redux-form - [Link](https://www.npmjs.com/package/redux-form)

#### UI Elements
* react-native-elements
* react-native-datepicker
* react-native-action-button
* react-native-drawer

I have also tried **shoutem** but their theme concept was little confusing with unclear documentation.

#### Other API's
* Parse - [Link](https://www.npmjs.com/package/parse) : Used to connect with Parse server hosted on Azure App services. 

You would find better tutorials online on above modules. It took me a while to figure out redux part and would like to contribute on it in this blog.

### What is Redux ?
Redux is a predictable state container for JavaScript apps.

**Example :**
Think of a startup where everyone stay together in one small room and work together. In such scenario, you rarely have Scrum master (or) follow best practices to develop a product. 

When company grows big, you have to define specific standards and follow them for better results. Like a Scrum master who would help collaborate between teams and has total knowledge of project at any given state.

I found some good images @ http://slides.com/jenyaterpil/redux-from-twitter-hype-to-production#/ and would use them here

**History :**
Redux is inspired by Facebook's Flux. Here is how Flux work's

* User interacts with View
* Actions describe the fact that something happened on View
* There would be multiple stores in Flux and Dispatcher would pass this action info to Stores that subscribed for it

![Flux](/content/images/2017/03/flux.png)

In **Redux**, we would have single store instead of multiple as in Flux above. In addition, we would have Reducer's. Reducer's specify how the application's state changes in response
![Redux](/content/images/2017/03/redux.png)

**Sample Flow**
![Redux Flow](/content/images/2017/03/redux_flow.gif)
Let's consider above Bank Transaction of $10 deposit,

* An Event is fired in View to deposit $10
* Action would pass this info to Reducer that would change the state
* New State info is passed to View reflecting changes in it

**Side Effects**
Many applications would need asynchronous actions. Handling them would be little complex with normal redux.
Ex: Server Communication
![Side Effects](/content/images/2017/03/redux_sideeffects.gif)

**Middleware's**
There are many middleware's available to perform these Side Effects and make life easy. Notably are

* Redux-Thunks (Asynchronous Action Creators)
* Redux-Saga (async code in a synchronous Style)

![Redux Middleware](/content/images/2017/03/redux_middleware.gif)
