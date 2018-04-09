

```python
# !pip install cufflinks
import pandas as pd
import numpy as np
import cufflinks as cf
import plotly.plotly as py
import plotly.tools as tls
import plotly.graph_objs as go

import sklearn 
from sklearn.preprocessing import StandardScaler
```


```python
tls.set_credentials_file(username="ashishpatel.ce", api_key='oLnw8eVRtPb9SPFkzNCJ')
```

# Basic Line Chart


```python
a = np.linspace(start=0, stop=36, num=36)
np.random.seed(25)
b = np.random.uniform(low=0.0, high=1.0, size=36)

trace = go.Scatter(x=a, y=b)
data = [trace]
py.iplot(data, filename = 'basic-file')
```

    High five! You successfully sent some data to your account on plotly. View your plot in your browser at https://plot.ly/~ashishpatel.ce/0 or inside your plot.ly account where it is named 'basic-file'
    




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/0.embed" height="525px" width="100%"></iframe>



# Small Line chart


```python
x = [1,2,3,4,5,6,7,8,9]
y = [1,2,3,4,0.5,4,3,2,1]
z = [10,9,8,7,6,5,4,3,2,1]

trace0 = go.Scatter(x=x, y=y, name = 'List Object',line = dict(width=5))
trace1 = go.Scatter(x=x, y=z, name = 'List Object 2',line = dict(width=5))

data = [trace0, trace1]
layout = dict(title = "Double Line Chart", xaxis = dict(title="X-Axis"),yaxis = dict(title="Y-Axis"))
fig = dict(data = data, layout = layout)
print(fig)
```

    {'layout': {'yaxis': {'title': 'Y-Axis'}, 'xaxis': {'title': 'X-Axis'}, 'title': 'Double Line Chart'}, 'data': [{'y': [1, 2, 3, 4, 0.5, 4, 3, 2, 1], 'type': 'scatter', 'x': [1, 2, 3, 4, 5, 6, 7, 8, 9], 'line': {'width': 5}, 'name': 'List Object'}, {'y': [10, 9, 8, 7, 6, 5, 4, 3, 2, 1], 'type': 'scatter', 'x': [1, 2, 3, 4, 5, 6, 7, 8, 9], 'line': {'width': 5}, 'name': 'List Object 2'}]}
    


```python
py.iplot(fig, filename = "basic-line-chart")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/2.embed" height="525px" width="100%"></iframe>




```python
car = pd.read_csv("https://gist.githubusercontent.com/seankross/a412dfbd88b3db70b74b/raw/5f23f993cd87c283ce766e7ac6b329ee7cc2e1d1/mtcars.csv")
df = car[['cyl','wt','mpg']]
layout = dict(title = "Chart from pandas dataframe", xaxis = dict(title="X-Axis"),yaxis = dict(title="Y-Axis"))
df.iplot(filename = "Simple-line-chart",layout=layout)
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/4.embed" height="525px" width="100%"></iframe>



# Creating Bar Chart


```python
data = [go.Bar(x=x,y=y)]
layout = dict(title = "Bar Chart from pandas dataframe", xaxis = dict(title="X-Axis"),yaxis = dict(title="Y-Axis"))
py.iplot(data, filename = "basic-barchart", layout = layout)
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/6.embed" height="525px" width="100%"></iframe>




```python
color_theme = dict(color = ['rgba(169,169,169,1)','rgba(255,160,122,1)','rgba(176,224,230,1)',
                   'rgba(189,183,107,1)','rgba(188,143,143,1)','rgba(221,160,221,1)','rgba(169,169,169,1)','rgba(255,160,122,1)','rgba(176,224,230,1)'])
```


```python
trace0 = go.Bar(x = x, y=y, marker = color_theme)
data = [trace0]
layout = go.Layout(title = "Custom Color")
fig = go.Figure(data=data, layout = layout)
py.iplot(fig,filename = "file-name")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/8.embed" height="525px" width="100%"></iframe>



# Create Pie Chart


```python
fig = { 'data' : [{'labels':['bicycle','motorbike','car','van','stroller'],
                   'values':[1,2,3,4,0.5],'type' : 'pie'}],
       'layout':{'title':'Simple Pie Chart'}}
py.iplot(fig,filename = 'pie chart')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/10.embed" height="525px" width="100%"></iframe>



# StatisticsPlot


```python
car = pd.read_csv("https://gist.githubusercontent.com/seankross/a412dfbd88b3db70b74b/raw/5f23f993cd87c283ce766e7ac6b329ee7cc2e1d1/mtcars.csv")
mpg = car.mpg
mpg.iplot(kind = "histogram", filename = "Simple Histogram")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/14.embed" height="525px" width="100%"></iframe>




```python
cars_data = car.ix[:,(1,3,4)].values
car_data_std = StandardScaler().fit_transform(cars_data)
car_select = pd.DataFrame(car_data_std)
car_select.columns = ['mpg','disp','hp']
car_select.iplot(kind = "histogram", filename = "Simple car Plot")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/16.embed" height="525px" width="100%"></iframe>




```python
car_select.iplot(kind = "histogram", filename = "Simple car Plot", subplots=True)
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/16.embed" height="525px" width="100%"></iframe>




```python
car_select.iplot(kind = "histogram", filename = "Simple car Plot", subplots=True, shape=(3,1))
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/16.embed" height="525px" width="100%"></iframe>



# Box Plot


```python
car_select.iplot(kind = "box", filename = "Boxplot")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/18.embed" height="525px" width="100%"></iframe>



 # Scatter plot 


```python
fig = {'data': [{'x':car_select.mpg, 'y':car_select.disp,'mode':'markers','name':'mpg'},
                {'x':car_select.hp, 'y':car_select.disp,'mode':'markers','name':'hp'}],
                'layout':{'xaxis':{'title':''}, 'yaxis' : {'title':'Stardardized Displacement'}}}
py.iplot(fig, filename="Group Scatter Plot")
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/22.embed" height="525px" width="100%"></iframe>



# Map Plot
#### 1.Cloropleth Map
#### 2.Point Map

# 1.Cloropleth Map


```python
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2011_us_ag_exports.csv')

for col in df.columns:
    df[col] = df[col].astype(str)

scl = [[0.0, 'rgb(242,240,247)'],[0.2, 'rgb(218,218,235)'],[0.4, 'rgb(188,189,220)'],\
            [0.6, 'rgb(158,154,200)'],[0.8, 'rgb(117,107,177)'],[1.0, 'rgb(84,39,143)']]

df['text'] = df['state'] + '<br>' +\
    'Beef '+df['beef']+' Dairy '+df['dairy']+'<br>'+\
    'Fruits '+df['total fruits']+' Veggies ' + df['total veggies']+'<br>'+\
    'Wheat '+df['wheat']+' Corn '+df['corn']

data = [ dict(
        type='choropleth',
        colorscale = scl,
        autocolorscale = False,
        locations = df['code'],
        z = df['total exports'].astype(float),
        locationmode = 'USA-states',
        text = df['text'],
        marker = dict(
            line = dict (
                color = 'rgb(255,255,255)',
                width = 2
            ) ),
        colorbar = dict(
            title = "Millions USD")
        ) ]

layout = dict(
        title = '2011 US Agriculture Exports by State<br>(Hover for breakdown)',
        geo = dict(
            scope='usa',
            projection=dict( type='albers usa' ),
            showlakes = True,
            lakecolor = 'rgb(255, 255, 255)'),
             )
    
fig = dict( data=data, layout=layout )
py.iplot( fig, filename='d3-cloropleth-map' )
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/26.embed" height="525px" width="100%"></iframe>



# World Map


```python
import plotly.plotly as py
import pandas as pd

df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2014_world_gdp_with_codes.csv')

data = [ dict(
        type = 'choropleth',
        locations = df['CODE'],
        z = df['GDP (BILLIONS)'],
        text = df['COUNTRY'],
        colorscale = [[0,"rgb(5, 10, 172)"],[0.35,"rgb(40, 60, 190)"],[0.5,"rgb(70, 100, 245)"],\
            [0.6,"rgb(90, 120, 245)"],[0.7,"rgb(106, 137, 247)"],[1,"rgb(220, 220, 220)"]],
        autocolorscale = False,
        reversescale = True,
        marker = dict(
            line = dict (
                color = 'rgb(180,180,180)',
                width = 0.5
            ) ),
        colorbar = dict(
            autotick = False,
            tickprefix = '$',
            title = 'GDP<br>Billions US$'),
      ) ]

layout = dict(
    title = '2014 Global GDP<br>Source:\
            <a href="https://www.cia.gov/library/publications/the-world-factbook/fields/2195.html">\
            CIA World Factbook</a>',
    geo = dict(
        showframe = False,
        showcoastlines = False,
        projection = dict(
            type = 'Mercator'
        )
    )
)

fig = dict( data=data, layout=layout )
py.iplot( fig, validate=False, filename='d3-world-map' )
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/28.embed" height="525px" width="100%"></iframe>



# Charoplath Map


```python
import plotly.plotly as py
import plotly.graph_objs as go

import pandas as pd
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2014_ebola.csv')
df.head()

cases = []
colors = ['rgb(239,243,255)','rgb(189,215,231)','rgb(107,174,214)','rgb(33,113,181)']
months = {6:'June',7:'July',8:'Aug',9:'Sept'}

for i in range(6,10)[::-1]:
    cases.append(go.Scattergeo(
        lon = df[ df['Month'] == i ]['Lon'], #-(max(range(6,10))-i),
        lat = df[ df['Month'] == i ]['Lat'],
        text = df[ df['Month'] == i ]['Value'],
        name = months[i],
        marker = dict(
            size = df[ df['Month'] == i ]['Value']/50,
            color = colors[i-6],
            line = dict(width = 0)
        ),
    ) )

cases[0]['text'] = df[ df['Month'] == 9 ]['Value'].map('{:.0f}'.format).astype(str)+' '+\
    df[ df['Month'] == 9 ]['Country']
cases[0]['mode'] = 'markers+text'
cases[0]['textposition'] = 'bottom center'

inset = [
    go.Choropleth(
        locationmode = 'country names',
        locations = df[ df['Month'] == 9 ]['Country'],
        z = df[ df['Month'] == 9 ]['Value'],
        text = df[ df['Month'] == 9 ]['Country'],
        colorscale = [[0,'rgb(0, 0, 0)'],[1,'rgb(0, 0, 0)']],
        autocolorscale = False,
        showscale = False,
        geo = 'geo2'
    ),
    go.Scattergeo(
        lon = [21.0936],
        lat = [7.1881],
        text = ['Africa'],
        mode = 'text',
        showlegend = False,
        geo = 'geo2'
    )
]

layout = go.Layout(
    title = 'Ebola cases reported by month in West Africa 2014<br> \
Source: <a href="https://data.hdx.rwlabs.org/dataset/rowca-ebola-cases">\
HDX</a>',
    geo = dict(
        resolution = 50,
        scope = 'africa',
        showframe = False,
        showcoastlines = True,
        showland = True,
        landcolor = "rgb(229, 229, 229)",
        countrycolor = "rgb(255, 255, 255)" ,
        coastlinecolor = "rgb(255, 255, 255)",
        projection = dict(
            type = 'Mercator'
        ),
        lonaxis = dict( range= [ -15.0, -5.0 ] ),
        lataxis = dict( range= [ 0.0, 12.0 ] ),
        domain = dict(
            x = [ 0, 1 ],
            y = [ 0, 1 ]
        )
    ),
    geo2 = dict(
        scope = 'africa',
        showframe = False,
        showland = True,
        landcolor = "rgb(229, 229, 229)",
        showcountries = False,
        domain = dict(
            x = [ 0, 0.6 ],
            y = [ 0, 0.6 ]
        ),
        bgcolor = 'rgba(255, 255, 255, 0.0)',
    ),
    legend = dict(
           traceorder = 'reversed'
    )
)

fig = go.Figure(layout=layout, data=cases+inset)
py.iplot(fig, validate=False, filename='West Africa Ebola cases 2014')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~ashishpatel.ce/30.embed" height="525px" width="100%"></iframe>




```python

```


```python

```


```python

```
