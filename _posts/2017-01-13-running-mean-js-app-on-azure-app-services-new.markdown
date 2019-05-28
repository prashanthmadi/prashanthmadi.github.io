---
layout: post
title: Running Mean.js App on Azure App Services with Continuous Integration and Delivery
date: '2017-01-13 02:49:16'
previewimg: '/content/images/2017/01/MEAN-image.png'
tags:
- nodejs
- mongodb
- mean
- angularjs
---

**MEAN.JS** is a full-stack JavaScript solution that helps you build fast, robust, and maintainable production web applications using MongoDB, Express, AngularJS, and Node.js.

#### Pre-requisites:
1) Create a **Mongodb** instance in Azure Portal
    * Navigate to Azure Portal and search for mongodb in Marketplace
    * You should find different options. For this blog, I'm choosing SAAS option from Microsoft.
![Create Mongodb instance](/content/images/2017/01/mongo.PNG)
    * Navigate to your newly created mongodb instance and get `MONGO_Connection_String`
![Mongodb Connection String](/content/images/2017/01/mongo_connection.PNG)

2) Create a **App Services Web App** in Azure Portal

* Navigate to Azure Portal and click on Web+Mobile option to select Web App
![Create Web App instance](/content/images/2017/01/webapp.PNG)
* Finish Next steps to create a web app by providing necessary details.
* After Creating Web App, Navigate to Application Settings and add below App settings
```
Key : MONGODB_URI
Value : MONGO_Connection_String from above step.
```
![Mongodb Connection String](/content/images/2017/01/appsettings.PNG)

* Set-up Continuous Deployment. Details are available at https://docs.microsoft.com/en-us/azure/app-service-web/app-service-continuous-deployment. For this blog, I'm using local git deployment.

You can find a Sample Mean.js project with below operations @ [GitHub Link](https://github.com/prashanthmadi/mean)

### Getting Started
You can find below steps @ http://meanjs.org/docs.html. For convenience, I would include important steps here

If you have git installed on your Laptop, Use below command to download latest meanjs code.
```
git clone https://github.com/meanjs/mean.git meanjs
```

#### Running in Local environment
**Install Node Modules**: Make sure your `NODE_ENV` is not set to production as we need both _dependencies_ and _devDependencies_ in local.
```
npm install
```
**Install Bower Components**: After installing node modules, it should have created bower executable in ./node_modules/.bin folder. We can utilize that instead of installing bower globally.
```
.\node_modules\.bin\bower install
```
```
Note: Set MONGOHQ_URL or MONGODB_URI if you don't have mongo instance running in local env. Check config/env/development.js file for details
```
**Run App** Enter below command and navigate to http://localhost:3000/ in browser.
It would run gulp tasks in this section mentioned in gulpfile.js.
```
npm start
```
![Local WOrking](/content/images/2017/01/localworking.PNG)

#### Running in Azure App Services

**Using Custom Deployment Script**: Azure Source Control deployment process would involve below steps

1. Moves content to azure web app
2. Creates default deployment script, if there is no .deployment file in web app root folder
3. Run’s deployment script. In case of a nodejs app it would do npm install here

At Step 2, Instead of deployment process creating a default script. We can include custom deployment script and change it’s content to run other tasks.

I have a separate Blog on this topic. Please Refer https://prmadi.com/azure-custom-deployment/

We would basically need to add two new files

`.deployment` file with below content inside it
```
[config]
command = bash deploy.sh
```
 `deploy.sh` file with content from [Link](https://github.com/prashanthmadi/mean/blob/master/deploy.sh). 

#### What are we doing in this deploy.sh other than default actions ?
* Install node modules (By default it would ignore devDependencies as NODE_ENV would be production, So we need to change Deployment Script to run extra npm install with --only=dev flag)
```
# 3. Install NPM packages
if [ -e "$DEPLOYMENT_TARGET/package.json" ]; then
  cd "$DEPLOYMENT_TARGET"
  eval $NPM_CMD install --production
  eval $NPM_CMD install --only=dev
  exitWithMessageOnError "npm failed"
  cd - > /dev/null
fi
```
* Add Content to Install bower components
```
# 4. Install Bower modules
if [ -e "$DEPLOYMENT_TARGET/bower.json" ]; then
  cd "$DEPLOYMENT_TARGET"
  eval ./node_modules/.bin/bower install
  exitWithMessageOnError "bower failed"
  cd - > /dev/null
fi
```
* Add Content to Run Gulp Tasks
```
# 5. Run Gulp Task
if [ -e "$DEPLOYMENT_TARGET/gulpfile.js" ]; then
  cd "$DEPLOYMENT_TARGET"
  eval ./node_modules/.bin/gulp prod
  exitWithMessageOnError "gulp failed"
  cd - > /dev/null
fi
```

* Change gulpfile.js (Here it's starting nodemon which we really don't need in production app. Replace `prod` task with below content in gulpfile.js)

```
// Run the project in production mode
gulp.task('prod', function (done) {
  runSequence(['copyLocalEnvConfig', 'makeUploadsDir', 'templatecache'], 'build', 'env:prod', 'lint', done);
});
```

There are two other changes

- Lock nodejs/npm version in package.json file
- Remove nodemon from gulpfile.js

Below commit diff has all the changes i made to make it run in Azure App Services - Windows.
https://github.com/prashanthmadi/mean/commit/f509f1eaec397784e4d62c62552d08ca33c229e6

#### Publish App 
Navigate to your root folder and commit your changes to `WEB_APP_GIT_URL`
```
git init  
git add .  
git commit -m "initial commit"  
git remote add meanapp WEB_APP_GIT_URL  
git push meanapp master  
```

Here is my App on Azure After publish

![Meanjs App Azure](/content/images/2017/01/webappworking.PNG)

You can find a Sample Mean.js project with above operations @ [GitHub Link](https://github.com/prashanthmadi/mean)