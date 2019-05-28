---
layout: post
title: Running Dash app with HttpPlatformHandler in Azure App Services Windows
date: '2018-07-22 22:47:37'
previewimg: 'https://prmadi.com/content/images/2018/10/dash.jpg'
---

Dash is a Open Source Python library for creating reactive, Web-based applications. Dash is a user interface library for creating analytical web applications. 

You can find a Sample Python Dash project with above operations @ [GitHub Link](https://github.com/gangularamya/azure-dash-httpplatformhandler)

**Create Sample Project in local environment**

* Create app.py file with below content

```
import os

import dash
import dash_core_components as dcc
import dash_html_components as html
import pandas as pd

app = dash.Dash(__name__)
server = app.server

df = pd.read_csv('datafiles/SampleCSV.csv')


def generate_table(dataframe, max_rows=10):
    return html.Table(
        # Header
        [html.Tr([html.Th(col) for col in dataframe.columns])] +

        # Body
        [html.Tr([
            html.Td(dataframe.iloc[i][col]) for col in dataframe.columns
        ]) for i in range(min(len(dataframe), max_rows))]
    )

app.layout = html.Div(children=[
    html.H4(children='US Agriculture Exports (2011)'),
    generate_table(df)
])

if __name__ == '__main__':
    app.run_server(debug=True)
    
 ```   

* Create SampleCSV.csv file under datafiles foder. 

![12](/content/images/2018/07/12.PNG)

* Create requirements.txt file with below content

```
dash==0.21.1
waitress==1.1.0
dash-core-components==0.23.0
dash-html-components==0.11.0
dash-renderer==0.13.0
plotly==2.7.0
numpy==1.14.5
pandas==0.23.1
```

* Install dependencies listed in requirements.txt file using below command.
```c:\Tools\Python_3.6.6\python.exe -m pip install --upgrade -r requirements.txt ```
![3-1](/content/images/2018/07/3-1.PNG)

* Run app in local environment using below command

![4-1](/content/images/2018/07/4-1.PNG)

* Navigate to http://127.0.0.1:8050/ and you should see app up and running

![5-1](/content/images/2018/07/5-1.PNG)
**Create Azure WebApp and Use Site Extension to Upgrade Python**

Navigate to Azure portal
 
* Create an empty webApp on Azure
 
* Once it is successful, search for “Extensions” in Azure portal
![6](/content/images/2018/07/6.jpg) 
* Click on “Add”

![7](/content/images/2018/07/7.jpg)
* Select any of the Python version from Extensions and click “ok” to apply the changes. In the Sample App I did selected “Python 3.6.4x 64”

![8](/content/images/2018/07/8.jpg)

For Creating and changing Deployment Script @[link ](https://ourwayoflyf.com/running-flask-app-with-httpplatformhandler-in-azure-app-services/)
 
* Activate Deployment options as “Local Git Repository” and click Ok.

![9](/content/images/2018/07/9.jpg)
 
* Push the local code to Azure and finally browse the site.
https://sampledashapp.azurewebsites.net/

![11](/content/images/2018/07/11.PNG)
 

