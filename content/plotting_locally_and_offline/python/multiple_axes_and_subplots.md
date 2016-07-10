**Table of Contents**
<!-- toc -->
---

# Multiple axes and subplots

* Add an additional independent axis to a figure
* Add independent subplots to a figure

<!--sec data-title="Summary" data-id="s1" data-show=true data-collapse=false ces-->

<!--endsec-->

Plotly is quite liberal with its axes.  We can add as many axes as we wish and position them anyway in the figure.  Doing so requires the correct parameters to be set however.  

For adding an additional x or y axis, or adding subplots, however, there are quicker ways or helper functions.  The fact that plotly gives us freedom though helps explain some of the parameters we need to set below.

<br>
# Two y Axes

Let's start with a simple plot of the number robbery crimes in Victoria (Australia) versus the unemployment rate over a decade.


<!--sec data-title="Demo Data" data-id="d1" data-show=true data-collapse=true ces-->

```python

yrs = ['2004/05',
 '2005/06',
 '2006/07',
 '2007/08',
 '2008/09',
 '2009/10',
 '2010/11',
 '2011/12',
 '2012/13',
 '2013/14']
 
 # number of reported robberies
 robs = [1217.0,
 1374.0,
 1470.0,
 1844.0,
 1766.0,
 1678.0,
 1772.0,
 1655.0,
 1354.0,
 1311.0]

# average employment rate as a percentage
emp = [71.0,
 71.5,
 72.299999999999997,
 73.0,
 72.0,
 71.900000000000006,
 72.799999999999997,
 72.400000000000006,
 72.0,
 71.099999999999994]
```
<!--endsec-->


```python
data = [
    go.Scatter(x = yrs, y=robs, name='Robberies'),
    go.Scatter(x = yrs, y = emp, name='Empl Rate')
]

fig = go.Figure(data=data, layout=dict())

iplot(fig)
```

<!--sec data-title="Initial Plot" data-id="d2" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/64.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

As we can see, the data sets, the number of robberies and the employment rate, require different scales.  On a single y axis, employment rate is inaccurately flat.

---

To add an additional y axis for the employment rate, there are two steps:

* Add the y-axis
* Bind the employment rate trace to the second y axis.

<br>
## Adding an axis

<br>
### Basics

An axis is added to the layout dictionary of a figure.  Like the default ```xaxis``` and ```yaxis```, it takes a dictionary (see [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md)).  The graph objects ```go.XAxis``` and ```go.YAxis``` can be used.

```python
fig.layout.update(yaxis2 = go.YAxis())

```

As described in [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md), by default, the attribute or key for axes in the layout dictionary of a plot are: ```xaxis``` and ```yaxis```.  That is, to modify the format of an axis, one needs to modify ```fig.layout.xaxis``` or ```fig.layout.yaxis```.

Whenever additional axes are to be added, **plotly requires** that the same attributes be used (ie, ```yaxis``` and ```xaxis```) but with the number ```2```, or ```3``` etc, for the second or third axis of that kind.  For this reason, our second yaxis has to be given to the key ```yaxis2``` in the layout dictionary.


<br>
### Positioning the new axis

The above code is incomplete and won't work.  We need to tell the new axis two things:

* Whether it is free floating or to overlap with the pre-existing axis;
* Which side of the current plot is it to be (top, bottom, left or right).

In our case, we want the new axis to be overlapping.  Like mentioned above, plotly lets axes do what ever you want, essentially, so the default is that an axis is free.  We have to tell it to be sort of 'connect' with the pre-existing yaxis.  The attribute used for this setting is ```overlaying```.  Its default is ```free```.  To connect it to a pre-existing axis, pass the kind of axis it needs to connect to.  If it needs to connect to a y axis, ```overlaying='y'```; if it needs to connect to an x axis, ```overlaying='x'```.

The default side for a y axis, is the left, whilst for an x axis, it is the bottom.  Thus, for our new y axis, by default it will literally be placed on top of the pre-existing one, which doesn't work well.  For it to be placed on the other side, we must use the attribute ```side``` and set it to the opposite of the pre-existing one, which for us, by default is on the left side.

If you'd like, try adding a new axis without these attributes set appropriately to get a an intuitive feeling for what they do.

---

So, to appropriately position our axis, we must add it with the following attributes:

```python
fig.layout.update(yaxis2 = go.YAxis(overlaying='y', side='right'))

```

You'll notice though, that neither of the traces have been bound to the new axis.  Try zooming or panning the second y axis - the new axis remains unchanged and no trace follows it ...

<!--sec data-title="Initial Plot" data-id="d3" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/66.embed" height="450" width="100%"></iframe>

<!--endsec-->


<br>
## Binding a trace to a new axis

As mentioned above, plotly is liberal with how the axes are arranged and how traces are bound to them.  Traces can be bound to any trace, technically.  By default, each trace is bound to the default or initial x and y axes.

To change this, each trace has two attributes, ```yaxis``` and ```xaxis``` that determine which axis or axes that trace is bound to.  

To repeat, these are attributes of each **trace** and are different from the attributes of the layout dictionary.  In the definition of a trace, ```xaxis``` defines **which x axis the trace will be bound to**.  In the definition of the layout ```xaxis``` defines the formatting and styling of the x axis for that figure.

In our case, we want our second trace to be bound to the second y axis.  

** Annoying Convention!!**
**Now this is oddly inconsistent**, but even though the second y axis must be called ```yaxis2```, the name we must give in the trace is not this but rather ```y2```.  It is shorter, but annoyingly inconsistent.  The same, of course, applies to any new x axes.

---

So, our code for the second trace needs to be ...

```python

go.Scatter(x = yrs, y = emp, name='Empl Rate', 

            # bind this trace to the second y axis, 
            # or the y axis defined by the attrbite "yaxis2"
            yaxis='y2')
```


<br>
## Final

The final code for a second y axis would look something like

```python
data = [
    go.Scatter(x = yrs, y=robs, name='Robberies'),
    
    go.Scatter(x = yrs, y = emp, name='Empl Rate', 
                yaxis='y2') # binding to the second y axis
]

# settings for the new y axis
y2 = go.YAxis(overlaying='y', side='right')

# adding the second y axis
layout = go.Layout(yaxis2=y2)

fig = go.Figure(data=data, layout=go.Layout(yaxis2=y2))

iplot(fig)
```

<!--sec data-title="Finally, positioned and bound" data-id="d4" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/68.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

<br>

Adding some color to the axes to make it clearer which is for which trace is often helpful.

```python

data = [
    go.Scatter(x = yrs, y=robs, name='Robberies'),
    go.Scatter(x = yrs, y = emp, name='Empl Rate', yaxis='y2')
]

# Add titles and color the font of the titles to match that of the traces
# 'SteelBlue' and 'DarkOrange' are the defaults of the first two colors.

y1 = go.YAxis(title='Robberies per yr', titlefont=go.Font(color='SteelBlue'))
y2 = go.YAxis(title= 'Employment Rate', titlefont=go.Font(color='DarkOrange'))

# update second y axis to be position appropriately
y2.update(overlaying='y', side='right')
             
# Add the pre-defined formatting for both y axes 
layout = go.Layout(yaxis1 = y1, yaxis2 = y2)

fig = go.Figure(data=data, layout=layout)

iplot(fig)

```

<!--sec data-title="Final two Axes" data-id="d5" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/70.embed" height="450" width="100%"></iframe>

<!--endsec-->


<br>
# Two subplots

If the two traces were in their separate subplots, then we wouldn't need to worry about accommodating two scales.

---


There is a helper function that does the heavy lifting for generating subplots for us.  (It's useful to remember though that you could do it all yourself just by manipulating the positioning and binding of various axes.)


<br>
## make_subplots() function

### Import

We will need to import the helper function from ```plotly.tools```.

```python
from plotly.tools import make_subplots
```

<br>
### Initialising the figure for subplots

```make_subplots``` prepares a figure dictionary that is set up to have subplots.  

So, unlike for previous plots, if you want subplots, you will tend to *start* by defining your figure graph object or dictionary and then define your traces etc.

```make_subplots``` expects the subplots to be arranged in a grid or table, with a certain amount of rows and columns, which you have to specify.

Thus, it's main options or key-word arguments are:

* ```rows``` - number of rows of subplots
* ```cols``` - number of columns of subplots

---

For our case, we will only have two subplots.  Let's arrange them in a single row, with two columns for each of the subplots.

```python
fig = make_subplots(rows=1, cols=2)
```

---

<br>
#### The guide output

**Note** - ```make_subplots``` returns a handy summary of the grid of subplots we've just initialised ...

```python
This is the format of your plot grid:
[ (1,1) x1,y1 ]  [ (1,2) x2,y2 ]
```

* Each square brack - ```[]``` - represents a single subplot
* the numbers in round brackets - ```(1, 2)``` - represents which row and column the subplot belongs to.  Ie ```(row, col)```.
* The ```x1, y1``` tells us which of the axes are bound to each subplot.  Recall from above that ```yaxis2``` is referred to as ```y2```, ```yaxis3``` as ```y3```, etc.  These references are what we see here.  You'll notice that there are new axes for each subplot.  Ie, the second subplot has ```x2, y2```You don't really need to change these unless you're doing some serious customising.  But it is helpful to see that all this function is doing is the same sort of stuff we were doing above.

---

<br>

#### The figure object

It's worthwhile at this point to see what our figure dictionary looks like, keeping in mind that all ```make_subplots()``` has done is write out this particular figure dictionary for us.

```python
pply(fig)
```
(see [Methods for updating the figure ...](./methods_for_updating_the_figure_or_graph_objects.md) for using ```pply()```)

*returns ...*

```python
{   'data': [],
    'layout': {   'xaxis1': {   'anchor': 'y1', 'domain': [0.0, 0.45]},
                  'xaxis2': {   'anchor': 'y2', 'domain': [0.55, 1.0]},
                  'yaxis1': {   'anchor': 'x1', 'domain': [0.0, 1.0]},
                  'yaxis2': {   'anchor': 'x2', 'domain': [0.0, 1.0]}}}
```

What has been done:

* separate x and y axes were added to the layout for each subplot
* The two pairs of axes were *bound* to each other using ```'anchor': 'y1'```.
* Each axis was given a portion of the whole figure using ```'domain': [0.0, 0.45]```.  This means that the axis spans, in this example, from the bottom left to 45% of the way to the right.  FOr y axes, ```0.0``` corresponds to the top left.

**Note** - after using ```make_subplots()```, we can change these default settings to customise the spatial arrangement of our plot.



<br>

## Append traces

To add a particular trace to a particular subplot, use ```fig.append_trace(trace, row, col)```.

This is a function built into figure graph objects.  You pass into the function the trace you want append, and then the row and column *coordinates* of the subplot you want to add the trace to.  This is what the *guide output* of the ```make_subplots()``` function is really useful for.


___

For us, we'll append the robberies trace to the first subplot ```(1, 1)```, and the employment rate trace to the second subplot ```(1, 2)```.


```python
fig.append_trace(go.Scatter(x = yrs, y=robs, name='Robberies'), 
                  1, 1) # first row, first column

fig.append_trace(go.Scatter(x = yrs, y = emp, name='Empl Rate'), 
                  1, 2) # first row, second column

iplot(fig)
```

With the subplot helper functions, this is easier than adding a new axis.


<!--sec data-title="Two subplots" data-id="d6" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/72.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

It's worthwhile looking at the figure dictionary again, to see how the traces were '*appended*' to their subplots


```python
pply(fig)
```

*returns ...*

```python
{   'data': [   {   'name': 'Robberies',
                    'type': 'scatter',
                    'xaxis': 'x1',        # This how the trace is bound
                    'yaxis': 'y1'},       # This how the trace is bound
                {   'name': 'Empl Rate',
                    'type': 'scatter',
                    'xaxis': 'x2',        # This how the trace is bound   
                    'yaxis': 'y2'}],      # This how the trace is bound
    'layout': {   'xaxis1': {   'anchor': 'y1', 'domain': [0.0, 0.45]},
                  'xaxis2': {   'anchor': 'y2', 'domain': [0.55, 1.0]},
                  'yaxis1': {   'anchor': 'x1', 'domain': [0.0, 1.0]},
                  'yaxis2': {   'anchor': 'x2', 'domain': [0.0, 1.0]}}}
```

You'll notice that all '*appending*' involved was binding the trace to the appropriate axes in the same way we were binding a trace to a new y axis above.  Also notice that the appropriate axes for each subplot are those that were listed in the guide ouput of the ```make_subplots()``` function.

---

<br>

## Share Axes

With our two data sets, one axis is identical for them - *time*.  This is how we did the first plot with two y axes ... both y axes shared the same x axis.  

We do this by using the ```shared_xaxes=True``` and/or ```shared_yaxes=True``` option or key-word argument of the ```make_subplots()``` function.

```python
fig = make_suplots(rows=r, cols=c, shared_xaxes=True)
```

For our two subplots, and any subplots for that matter, x or y axes can be shared also.

So, for us, we'll rearrange our subplots into a single column, so that they can share an x axis of time.

---

<br>
### Initialise the figure

```python

# two subplots, each in a row, forming one column
fig = make_subplots(rows=2, cols=1, 
                    shared_xaxes=True) # sharing the x axis.

```

*returns ...*

```python
This is the format of your plot grid:
[ (1,1) x1,y1 ]
[ (2,1) x1,y2 ]
```

**Note** - there are two y axes (```y1``` and ```y2```) but only one x axis, that is bound to both suplots.


<br>
### Append traces

Just as before, but with the rows and cols swapped.

```python
fig.append_trace(go.Scatter(x = yrs, y=robs, name='Robberies'), 1,1)
fig.append_trace(go.Scatter(x = yrs, y = emp, name='Empl Rate'), 2, 1)
```


<!--sec data-title="Two subplots sharing an x axis" data-id="d7" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/74.embed" height="450" width="100%"></iframe>
<!--endsec-->


### Figure dictionary

It's worthwhile looking at the figure dictionary again.

```python
{   'data': [   {   'name': 'Robberies',
                    'type': 'scatter',
                    'xaxis': 'x1',
                    'yaxis': 'y1'},
                {   'name': 'Empl Rate',
                    'type': 'scatter',
                    'xaxis': 'x1',
                    'yaxis': 'y2'}],
    'layout': {   'xaxis1': {   'anchor': 'y2', 'domain': [0.0, 1.0]},
                  'yaxis1': {   'anchor': 'free',
                                'domain': [0.575, 1.0],
                                'position': 0.0},
                  'yaxis2': {   'anchor': 'x1', 'domain': [0.0, 0.425]}}}
```


What was done differently to share an axis:

* Both traces were bound to the same x axis
* No second x axis was defined
* The first y axis, which is for the top subplot, was not bound to any x axis, but left free (```'anchor': 'free'```).


<br>

# Exercise

1. ...



```python

years = [1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
       1911, 1912, 1913, 1914, 1915, 1916, 1917, 1918, 1919, 1920, 1921,
       1922, 1923, 1924, 1925, 1926, 1927, 1928, 1929, 1930, 1931, 1932,
       1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941, 1942, 1943,
       1944, 1945, 1946, 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954,
       1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962, 1963, 1964, 1965,
       1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973, 1974, 1975, 1976,
       1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
       1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
       1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
       2010, 2011, 2012, 2013, 2014, 2015]


le_fr = [ 45.08  ,  47.01  ,  48.01  ,  48.43  ,  48.08  ,  48.36  ,
        47.74  ,  48.28  ,  49.3   ,  50.01  ,  51.37  ,  48.17  ,
        51.62  ,  51.35  ,  37.85  ,  35.63  ,  39.51  ,  42.6   ,
        34.34  ,  47.52  ,  51.6   ,  52.6968,  54.9336,  54.6704,
        55.2972,  54.424 ,  54.0708,  55.8476,  55.4944,  54.3312,
        56.938 ,  57.0048,  57.3416,  57.7884,  58.4552,  58.422 ,
        58.9188,  59.2856,  59.0924,  59.7492,  49.586 ,  57.8128,
        57.5896,  53.4864,  47.3532,  55.13  ,  62.5568,  64.1636,
        66.0204,  65.1172,  66.594 ,  66.3308,  67.6276,  67.5644,
        68.4412,  68.708 ,  68.7448,  69.1816,  70.4184,  70.4552,
        70.672 ,  71.2588,  70.7956,  70.6524,  71.6192,  71.456 ,
        71.8728,  71.8696,  71.8664,  71.6032,  72.5   ,  72.6   ,
        72.8   ,  73.1   ,  73.3   ,  73.2   ,  73.4   ,  73.8   ,
        74.1   ,  74.3   ,  74.5   ,  74.8   ,  75.    ,  75.2   ,
        75.5   ,  75.7   ,  76.    ,  76.4   ,  76.6   ,  76.9   ,
        77.1   ,  77.3   ,  77.5   ,  77.7   ,  77.9   ,  78.1   ,
        78.4   ,  78.7   ,  78.8   ,  78.9   ,  79.1   ,  79.2   ,
        79.4   ,  79.7   ,  80.1   ,  80.4   ,  80.7   ,  80.9   ,
        81.    ,  81.    ,  81.2   ,  81.4   ,  81.6   ,  81.7   ,
        81.8   ,  81.9   ]


le_ge = [ 43.915     ,  44.222     ,  44.529     ,  44.836     ,
        45.143     ,  45.45      ,  46.04166667,  46.63333333,
        47.225     ,  47.81666667,  48.40833333,  49.        ,
        49.59166667,  50.18333333,  46.17648422,  40.52556325,
        38.9888193 ,  40.08037644,  32.93682031,  48.32065914,
        53.5       ,  55.01820257,  55.62354801,  56.22889344,
        56.83423887,  57.4395843 ,  57.85150116,  58.26341802,
        58.67533488,  59.08725174,  59.4991686 ,  59.91108546,
        60.32300232,  60.73491918,  61.14683604,  61.5587529 ,
        61.84933643,  62.13991996,  62.43050348,  61.07442034,
        60.73821096,  59.08225406,  55.08617092,  49.79008778,
        37.09400464,  29.0979215 ,  60.61319836,  62.21527522,
        63.81735208,  65.41942894,  67.0215058 ,  67.18742266,
        67.51033952,  67.82125638,  68.12117324,  68.4080901 ,
        68.70345102,  68.62532856,  69.36929231,  69.48021979,
        69.40190727,  69.99702797,  70.16889372,  70.26131586,
        70.82344196,  70.81075623,  70.92828395,  71.15404398,
        70.80345367,  70.65682236,  70.9       ,  71.        ,
        71.2       ,  71.5       ,  71.8       ,  71.9       ,
        72.3       ,  72.6       ,  72.7       ,  72.9       ,
        73.1       ,  73.4       ,  73.6       ,  74.        ,
        74.4       ,  74.6       ,  74.8       ,  75.1       ,
        75.3       ,  75.4       ,  75.4       ,  75.6       ,
        75.9       ,  76.2       ,  76.4       ,  76.6       ,
        76.9       ,  77.3       ,  77.7       ,  77.9       ,
        78.1       ,  78.3       ,  78.5       ,  78.8       ,
        79.1       ,  79.4       ,  79.7       ,  79.8       ,
        80.        ,  80.        ,  80.2       ,  80.3       ,
        80.5       ,  80.7       ,  80.9       ,  81.1       ]

gdp_fr = [ 4314,  4100,  4048,  4181,  4261,  4367,  4304,  4648,  4629,
        4774,  4542,  5004,  5420,  5373,  4506,  3968,  4548,  4506,
        3861,  4258,  4550,  4326,  5188,  5434,  6032,  6075,  6284,
        6157,  6522,  7078,  6835,  6534,  5962,  6140,  5929,  5785,
        5869,  6008,  5861,  6106,  4821,  4666,  4700,  4691,  3594,
        4423,  5909,  6228,  6988,  7367,  7914,  8301,  8446,  8622,
        9006,  9453,  9907, 10442, 10681, 10911, 11642, 12168, 12767,
       13235, 13969, 14514, 15158, 15759, 16321, 17339, 18185, 18891,
       19570, 20486, 20997, 20851, 21661, 22270, 22928, 23647, 23962,
       24186, 24753, 25188, 25497, 25917, 26453, 26963, 28101, 28942,
       29476, 29707, 30033, 29719, 30303, 30823, 31141, 31756, 32764,
       33707, 34774, 35197, 35333, 35371, 36090, 36395, 37001, 37641,
       37505, 36215, 36745, 37328, 37227, 37309, 37218, 37599]

gdp_ge = [ 4596,  4422,  4457,  4634,  4751,  4783,  4858,  5002,  5017,
        5049,  5162,  5277,  5477,  5692,  4793,  4559,  4633,  4679,
        4746,  4131,  4482,  4969,  5415,  4500,  5270,  5857,  6015,
        6618,  6909,  6884,  6791,  6276,  5809,  6178,  6738,  7232,
        7852,  8305,  8894,  9674,  9711, 10310, 10407, 10722, 11120,
        8284,  4084,  4504,  5258,  6112,  7251,  7884,  8561,  9252,
        9926, 10998, 11751, 12385, 12884, 13759, 14808, 15317, 15872,
       16221, 17100, 17838, 18262, 18311, 19254, 20409, 21218, 21695,
       22497, 23461, 23662, 23630, 24904, 25678, 26444, 27515, 27765,
       27846, 27645, 28227, 29135, 29851, 30514, 30986, 31906, 32706,
       31476, 32844, 33221, 32689, 33375, 33843, 34008, 34578, 35254,
       35931, 36953, 37517, 37458, 37167, 37614, 37901, 39352, 40693,
       41199, 38975, 40632, 42080, 42959, 42887, 43444, 44053]

```
