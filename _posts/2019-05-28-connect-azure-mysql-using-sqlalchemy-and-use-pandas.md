---
title: Connect Azure Mysql using Sqlalchemy and use Pandas
layout: post
tags:
- Azure Mysql
- sqlalchemy
- pandas
- notebook
---

I have been hosting my blog for a while using [Ghost](https://ghost.org/) on Azure App Services. You can find details on how i did that at [link](https://prashanthmadi.github.io/2017/08/29/ghost-v1-0-on-app-service-linux-new.html). I personally liked running my blog on ghost with all great functionalities it provides(definitely better than wordpress :) ) but it was getting tiresome to maintain it(upgrades in app services + newer version of ghost).

While looking for alterntate solutions, jekyll looked something very interesting and also free to host with github pages. You can find details on how to migrate online

### Issue:
I was trying to add preview image in [front-matter](https://jekyllrb.com/docs/front-matter/) that would be used later on home page. Luckily preview image info is available in posts table of ghost database, I have used below steps to get that info and insert in posts.

It would involve, Connecting Azure MySQL database using sqlalchemy and retrieve info using pandas. Perform some data manuplation and insert it into posts.

Later used below command to generate markdown content of my jupyter notebook that i copied below.

```
jupyter nbconvert --to markdown azuremysql_sqlalchemy_pandas.ipynb
```


```python
from sqlalchemy import create_engine
from urllib.parse import quote_plus
engine = create_engine("mysql+pymysql://%s:%s@prashanthmadi.mysql.database.azure.com/prashanthmadi"
                   % (quote_plus("prashanthmadi@prashanthmadi"),quote_plus("xxx3333@@"))  
                      )

```


```python
#making sure connection works
conn = engine.connect()
```


```python
query = "SELECT slug,published_at,feature_image FROM posts where feature_image!='None' limit 5"
```


```python
# Read data with sqlalchemy
result = engine.execute(query)
for _r in result:
   print(_r)

```

    ('nodejs-npm-versions-azure-webaps', datetime.datetime(2016, 7, 25, 1, 44, 40), '/content/images/2016/07/7587-AzureLovesNode_4657B74B.png')
    ('creating_hyper_links_in_large_text_text_view_android', datetime.datetime(2013, 3, 20, 22, 23), '/content/images/2017/09/android-app-banner.jpg')
    ('azure-custom-deployment', datetime.datetime(2016, 7, 31, 0, 56), '/content/images/2016/07/bower-composer-gulp.jpg')
    ('wordpress-performance-azure', datetime.datetime(2016, 7, 29, 19, 22, 9), '/content/images/2016/07/fimg2.jpg')
    ('hosting-mysql-on-azure-linux-vm', datetime.datetime(2016, 7, 31, 17, 15, 8), '/content/images/2016/07/mysql.png')



```python
# Read data using Pandas
import pandas as pd
df = pd.read_sql_query(query, engine)
```


```python
# data manipulation and clean-up
df['slug']= df.published_at.dt.date.map(str)+"-"+df.slug.map(str)
dfnew = df.rename(columns={'slug': 'fileName','feature_image':'previewimg'}).drop("published_at", axis=1)
```


```python
print(dfnew.fileName[0])
```

    2016-07-25-nodejs-npm-versions-azure-webaps



```python
import os
def addPreviewImg(filename,previewimg):
    try:
        filename = "/Users/prashanth/workspace/prashanthmadi.github.io/_posts/"+filename
        with open (filename+".markdown","r") as inp,open (filename+"-new.markdown","w") as ou:
            for a,d in enumerate(inp.readlines()):
                if a==4:
                    ou.write("previewimg: " +"'"+previewimg+"'\n")
                ou.write(d)
        os.remove(filename+".markdown");
    except FileNotFoundError as e:
        print(e)
        pass     
```


```python
[addPreviewImg(x, y) for x, y in zip(dfnew['fileName'], dfnew['previewimg'])]
```

    [Errno 2] No such file or directory: '/Users/prashanth/workspace/prashanthmadi.github.io/_posts/2016-08-28-videos.markdown'





    [None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None,
     None]




```python

```
