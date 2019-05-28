---
layout: post
title: Using Custom Tomcat Configuration in  Azure App Services(Windows)
date: '2018-01-08 20:17:32'
tags:
- azure
- java
- tomcat
---

**Azure** makes it easy to deploy and scale **Java** apps, using the tools you know and love. You can easily get started following below link
https://docs.microsoft.com/en-us/java/azure/

There are multiple approaches to run Java app on Azure App Services. One such would be to use Application Settings for enabling Java and Web Container.

![java_appsettings](/content/images/2018/01/java_appsettings.PNG)

After Enabling above options,
- Navigate to kudu Console `https://<Your_App_Name>.scm.azurewebsites.net/DebugConsole`
- Go to `D:\home\site\wwwroot` folder and you should find a webapps folder inside it. 
- You can drop your app's .war file inside webapps folder (as in below image)
![kudu](/content/images/2018/01/kudu.PNG)
- It would explode automatically and your app should be up and running
![hello_world](/content/images/2018/01/hello_world.PNG)

Here is how it works internally, Request reaches one of your worker instance and hits IIS which in-turn forwards it to Tomcat.

![java_arch](/content/images/2018/01/java_arch.PNG)

After couple of days, you might want to Add/Change tomcat config while using existing approach. You should be able to find tomcat config files in `D:\Program Files (x86)\apache-tomcat-x.x.xx\conf` but unfortunately these files are not editable.

**Scienario :** By Default, Tomcat doesn't print time taken for request in site access log. Here i would alter tomcat config using a workaround for above approach to print time_taken. 

   - Create a `web.config` file inside `D:\home\site\wwwroot` with below content in it

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="httpPlatformHandlerMain" />
      <add name="httpPlatformHandlerMain" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="D:\Program Files (x86)\apache-tomcat-8.5.20\bin\startup.bat" requestTimeout="00:04:00" arguments="-config D:\home\site\wwwroot\conf\server.xml start" startupTimeLimit="60" startupRetryCount="3" stdoutLogEnabled="true">
        <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Xms1024m -Xmx1024m -Dport.http=%HTTP_PLATFORM_PORT% -Dsite.logdir=d:/home/LogFiles/ -Dsite.tempdir=d:/home/site" />
        </environmentVariables>
      </httpPlatform>
  </system.webServer>
</configuration>
```

`web.config` is an IIS configuration file and we are using it to pass extra config in arguments to tomcat when it starts tomcat for the first request.

Note: Here i have set processPath to `D:\Program Files (x86)\apache-tomcat-8.5.20\bin\startup.bat`. Change it as per your requirement


As you can see above, we are passing `D:\home\site\wwwroot\conf\server.xml` as our new tomcat config file. 

- Create new server.xml file at above mentioned location and copy content from
`D:\Program Files (x86)\apache-tomcat-x.x.xx\conf\server.xml `

Alter its value to obtain required config. I have added `%T` in pattern for site_access_log as below 

 ``` 
 <Valve className="org.apache.catalina.valves.AccessLogValve" directory="${site.logdir}" prefix="site_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b %T" /> 
 ```
 
 Here is my site_access_log with `time_taken` printed in it.
 ![Time_taken](/content/images/2018/01/Time_taken.PNG)
 
### Troubleshoot:

1. App did not start after above configuration.
 Make sure your app is using 64-bit java/platform. In above web.config file we have added few extra `CATALINA_OPTS`  that doesn't go well on 32-bit.
![java_appsettings_platform](/content/images/2018/01/java_appsettings_platform.PNG)

### Reference: 
https://docs.microsoft.com/en-us/iis/extensions/httpplatformhandler/httpplatformhandler-configuration-reference 