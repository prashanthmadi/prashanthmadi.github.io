---
layout: post
title: Import SQL Data in spark/pyspark cli
date: '2018-04-10 02:24:38'
tags:
- spark
- sql
---


**Apache Spark** is a lightning-fast unified analytics engine for big data and machine learning

While trying to connect/retreive data from SQL Database using spark/pyspark cli you might receive below error
```
File '/usr/hdp/current/spark2-client/python/lib/py4j-0.10.4-src.zip/py4j/protocol.py', line 319, in get_return_value
py4j.protocol.Py4JJavaError: An error occurred while calling o58.jdbc.
: java.sql.SQLException: No suitable driver
        at java.sql.DriverManager.getDriver(DriverManager.java:315)
```

This is because by-defalult SQL driver is not loaded into spark/pyspark cli..
- You have to add –driver-class-path option while starting cli and provide SQL driver path to load it
- Fortunately, In case of Azure HDInsight we already have SQL Driver installed in hive lib folder.
```
pyspark --driver-class-path /usr/hdp/2.6.3.2-13/hive/lib/sqljdbc41.jar
```
- Here is my code to connect SQL and retrieve a RDD
```	
df1 = spark.read.option('user','sparkdatabasetestsql@sparkdatabasetestsql').option('password','xxxxxxxxxxx').jdbc('jdbc:sqlserver://sparkdatabasetestsql.database.windows.net:1433;database=sparkdatabasetestsql;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;','SalesLT.Customer');

```
- Getting number of rows from above RDD
```
df1.count()
```

![pyspark-cli](/content/images/2018/04/pyspark-cli.png)