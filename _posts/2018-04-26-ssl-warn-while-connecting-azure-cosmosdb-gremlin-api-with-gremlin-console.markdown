---
layout: post
title: SSL warn while connecting Azure COSMOSDB(Gremlin API) from Gremlin console/driver
date: '2018-04-26 19:53:01'
tags:
- azure
- cosmosdb
- gremlin
- graph-api
---

Azure Cosmos DB supports Apache Tinkerpop's graph traversal language, Gremlin, which is a Graph API for creating graph entities, and performing graph query operations.

You can Get Started easily following https://docs.microsoft.com/en-us/azure/cosmos-db/graph-introduction

You might experience below warning while connecting your app with COSMOSDB remote server.

```
WARN  org.apache.tinkerpop.gremlin.driver.Cluster  - SSL configured without a trustCertChainFile and thus trusts all certificates without verification (not suitable for production)
```

Most of the Providers do provide a root cert that you could use to fix this warning.. 

You should be able to grab a Baltimore root certificate from below url.. Its valid till 2025..
https://cacert.omniroot.com/bc2025.crt

Convert this downloaded .crt file to .pem file. Mac has built-in keychain Access tool which should help you do it easily…

As you can see in below screenshot.. there is bc2025.crt and also bc2025.pem file for `ls` output


![gremlin_warn_out](/content/images/2018/04/gremlin_warn_out.PNG)

Below is my sample `remote-session.yaml` file.. 

For the first remote connect I have removed trustCertChainFile and it gave me SSL warning.

For the second scenario, I have added trustCertChainFile in it pointing to pem file that we created earlier from crt and haven’t see any warning..
```
hosts: ["xxxxxx.gremlin.cosmosdb.azure.com"]
port: 443
username: "/dbs/graphdb/colls/Persons"
password: "xxxxxxxxxxxxxxxxxxxxx"
connectionPool: {
  enableSsl: true,
  trustCertChainFile: "/Users/prashanth/workspace/apache-tinkerpop-gremlin-console-3.3.1/bc2025.pem"
  }
serializer: { className: org.apache.tinkerpop.gremlin.driver.ser.GraphSONMessageSerializerV1d0, config: { serializeResultToString: true }}
```

I’m sure similar option should exist for other drivers..

For Java App, check for configuration section at below link that has `connectionPool.trustCertChainFile`
http://tinkerpop.apache.org/docs/3.3.2/reference/#connecting-via-java