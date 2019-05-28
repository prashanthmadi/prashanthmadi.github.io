---
layout: post
title: Running Sqoop to get SQL data on Azure HDInsight Instance
date: '2018-04-05 18:37:47'
previewimg: '/content/images/2018/04/scoop_banner-2.png'
---

**Azure HDInsight** is a fully-managed cloud service that makes it easy, fast, and cost-effective to process massive amounts of data. Use popular open-source frameworks such as Hadoop, Spark, Hive, LLAP, Kafka, Storm, R & more.

Get started with Azure Hdinsight by following below link
https://azure.microsoft.com/en-us/services/hdinsight/

Apache Sqoop is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases. 
Source: http://sqoop.apache.org/

Let's say if you want to run Sqoop on HDInsight node to Receive/Transfer Data from SQL. 

Here is one such scenario where i was trying to list all the tables in my Azure SQL Database..
```
> sqoop list-tables --connect "jdbc:sqlserver://<YOUR_SQL_SERVER_NAME>.database.windows.net:1433;database=<YOUR_DATABASE_NAME>;user=<USER>;password=<PASSWORD>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;" -- --schema "<SCHEMA_IF_EXISTS>"
```

It might end up with below error
```
18/04/03 22:15:29 ERROR sqoop.Sqoop: Got exception running Sqoop: java.lang.RuntimeException: Could not load db driver class: com.microsoft.jdbc.sqlserver.SQLServerDr
java.lang.RuntimeException: Could not load db driver class: com.microsoft.jdbc.sqlserver.SQLServerDriver
        at org.apache.sqoop.manager.SqlManager.makeConnection(SqlManager.java:875)
        at org.apache.sqoop.manager.GenericJdbcManager.getConnection(GenericJdbcManager.java:52)
        at org.apache.sqoop.manager.SqlManager.execute(SqlManager.java:763)
        at org.apache.sqoop.manager.SqlManager.execute(SqlManager.java:786)
        at org.apache.sqoop.manager.SqlManager.getColumnInfoForRawQuery(SqlManager.java:289)
        at org.apache.sqoop.manager.SqlManager.getColumnTypesForRawQuery(SqlManager.java:260)
        at org.apache.sqoop.manager.SqlManager.getColumnTypes(SqlManager.java:246)
        at org.apache.sqoop.manager.ConnManager.getColumnTypes(ConnManager.java:328)
        at org.apache.sqoop.orm.ClassWriter.getColumnTypes(ClassWriter.java:1853)
        at org.apache.sqoop.orm.ClassWriter.generate(ClassWriter.java:1653)
        at org.apache.sqoop.tool.CodeGenTool.generateORM(CodeGenTool.java:107)
        at org.apache.sqoop.tool.ImportTool.importTable(ImportTool.java:488)
        at org.apache.sqoop.tool.ImportTool.run(ImportTool.java:615)
        at org.apache.sqoop.Sqoop.run(Sqoop.java:147)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.sqoop.Sqoop.runSqoop(Sqoop.java:183)
        at org.apache.sqoop.Sqoop.runTool(Sqoop.java:225)
        at org.apache.sqoop.Sqoop.runTool(Sqoop.java:234)
        at org.apache.sqoop.Sqoop.main(Sqoop.java:243)
```

Sqoop by default supports Several Databases, including MySQL but to use it for MSSQL you need to install SQL Driver.

Fortunately, we already have this installed for hive @ `/usr/hdp/2.6.3.2-13/hive/lib/sqljdbc41.jar` for each node in HDInsight.

All you have to do is run below line of code before using sqoop
```
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/usr/hdp/2.6.3.2-13/hive/lib/sqljdbc41.jar
```

Now i run the same query as above

```
$ sqoop list-tables --connect "jdbc:sqlserver://<YOUR_SQL_SERVER_NAME>.database.windows.net:1433;database=<YOUR_DATABASE_NAME>;user=<USER>;password=<PASSWORD>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;" -- --schema "<SCHEMA_IF_EXISTS>"
``` 
 
As you can see below, it has listed all the tables in my Database.

```
Warning: /usr/hdp/2.6.3.2-13/accumulo does not exist! Accumulo imports will fail.
Please set $ACCUMULO_HOME to the root of your Accumulo installation.
18/04/03 22:29:36 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6.2.6.3.2-13
18/04/03 22:29:36 INFO manager.SqlManager: Using default fetchSize of 1000
18/04/03 22:29:36 INFO manager.SQLServerManager: We will use schema SalesLT
Customer
ProductModel
vProductModelCatalogDescription
ProductDescription
Product
ProductModelProductDescription
vProductAndDescription
ProductCategory
vGetAllCategories
Address
CustomerAddress
SalesOrderDetail
SalesOrderHeader
```
