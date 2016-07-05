**Table of Contents**
<!-- toc -->
---

# Layout - titles, axes and ticks

* Adjusting Graph and axis titles
* Adjusting the axis and grid lines
* Adjusting tick locations, labels and axis ranges.

<!--sec data-title="Summary" data-id="s1" data-show=true data-collapse=false ces-->

<!--endsec-->


# Layout

As described in the section on the [DNA of a plot.ly graph](./dna_of_a_plotly_graph.md), general styling of a plot.ly graph occurs in a ```layout``` dictionary, which is the second variable in a figure dictionary.

That is, the general structure of making a plot in plotly is :

```python
data = [trace1, trace2, trace3, ...]

layout = dict(style1='parameter1', style2='parameter2', ...)

fig = dict(data = data, layout=layout)

iplot(fig)
```

All of the styling in this section will be done through attributes in this ```layout``` variable.

Moreover, from here on in, we will be adding our ```data``` and ```layout``` variables to a figure dictionary, and then passing this dictionary to our ```iplot``` function.


<br>
---

# Title

The title of a graph is an attribute of its ```layout```.

---

Let us move onto a real data set and manipulate the titles and axes.

The demo data if you want to replicate is in the section below and the code follows.

<!--sec data-title="Demo Data - Life expecancy" data-id="d1" data-show=true data-collapse=true ces-->

Life expectancy from 1900 to 2015 for four countries:

* United Kingodm
* France
* Germany
* Australia

Copy and past and convert to numpy arrays if desired (shouldn't be necessary).

If you are comfortable extracting data out of CSV files, download <a href="https://raw.githubusercontent.com/maegul/ResGuides-Plotly/master/data/reduced_life_exp_dat.csv" download>this file instead</a>.
```python

yrs = [1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
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
       
uk = [ 46.32 ,  47.91 ,  49.08 ,  50.43 ,  49.11 ,  50.86 ,  50.58 ,
        51.44 ,  51.84 ,  52.52 ,  53.99 ,  51.54 ,  54.55 ,  53.83 ,
        51.99 ,  48.2  ,  47.73 ,  45.57 ,  40.43 ,  54.12 ,  56.6  ,
        58.346,  57.122,  59.388,  58.154,  58.49 ,  59.636,  59.012,
        59.958,  57.674,  60.85 ,  60.066,  60.582,  60.618,  61.344,
        61.99 ,  61.786,  61.812,  63.228,  63.614,  60.89 ,  61.286,
        63.902,  63.918,  64.754,  65.75 ,  66.366,  66.332,  68.388,
        68.074,  68.58 ,  68.176,  69.472,  69.738,  70.104,  70.07 ,
        70.336,  70.452,  70.628,  70.724,  70.94 ,  70.686,  70.752,
        70.658,  71.444,  71.43 ,  71.346,  71.972,  71.598,  71.554,
        71.8  ,  72.   ,  72.   ,  72.   ,  72.3  ,  72.6  ,  72.9  ,
        73.1  ,  73.   ,  73.1  ,  73.4  ,  73.8  ,  74.1  ,  74.3  ,
        74.6  ,  74.7  ,  74.9  ,  75.1  ,  75.3  ,  75.5  ,  75.7  ,
        76.   ,  76.3  ,  76.5  ,  76.7  ,  76.8  ,  76.9  ,  77.2  ,
        77.4  ,  77.6  ,  77.8  ,  78.   ,  78.2  ,  78.5  ,  78.8  ,
        79.1  ,  79.3  ,  79.4  ,  79.5  ,  79.7  ,  80.   ,  80.4  ,
        80.8  ,  81.   ,  81.2  ,  81.4  ]

fr = [ 45.08  ,  47.01  ,  48.01  ,  48.43  ,  48.08  ,  48.36  ,
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


ge = [ 43.915     ,  44.222     ,  44.529     ,  44.836     ,
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

au = [ 49.92647059,  50.45568627,  50.98490196,  51.51411765,
        52.04333333,  52.57254902,  53.10176471,  53.63098039,
        54.16019608,  54.68941176,  55.21862745,  55.74784314,
        56.27705882,  56.80627451,  57.3354902 ,  57.86470588,
        58.39392157,  58.92313725,  54.80239165,  59.98156863,
        60.51078431,  61.0438    ,  62.8976    ,  61.7414    ,
        62.5452    ,  63.239     ,  62.9628    ,  62.9366    ,
        62.9904    ,  63.1842    ,  64.998     ,  65.4318    ,
        65.7356    ,  65.5694    ,  64.9332    ,  65.207     ,
        65.3308    ,  65.8946    ,  65.9384    ,  65.8922    ,
        66.336     ,  66.2198    ,  65.9636    ,  66.4874    ,
        68.1212    ,  68.555     ,  68.0788    ,  68.6926    ,
        68.6164    ,  69.2402    ,  69.134     ,  68.8378    ,
        69.2416    ,  69.8254    ,  69.9792    ,  70.303     ,
        70.1868    ,  70.4706    ,  71.0244    ,  70.5982    ,
        71.042     ,  71.3158    ,  71.0896    ,  71.1534    ,
        70.8172    ,  71.151     ,  70.9948    ,  71.2786    ,
        70.9124    ,  71.3262    ,  71.        ,  71.3       ,
        71.7       ,  72.        ,  72.1       ,  72.5       ,
        73.        ,  73.4       ,  73.8       ,  74.2       ,
        74.5       ,  74.8       ,  75.        ,  75.3       ,
        75.5       ,  75.7       ,  76.        ,  76.2       ,
        76.4       ,  76.6       ,  77.        ,  77.4       ,
        77.7       ,  78.        ,  78.2       ,  78.4       ,
        78.6       ,  78.9       ,  79.1       ,  79.3       ,
        79.7       ,  80.1       ,  80.4       ,  80.7       ,
        81.        ,  81.2       ,  81.4       ,  81.5       ,
        81.5       ,  81.6       ,  81.7       ,  81.8       ,
        81.8       ,  81.8       ,  81.8       ,  81.8       ]


```
<!--endsec-->


```python

# preparing some styling that applies to all traces beforehand to reduce replication
line_styl = go.Line(width=6) 
op = 0.55

data = go.Data([
    
    go.Scatter(x=years, y=uk, name='UK', opacity=op, line=line_styl),
    go.Scatter(x=years, y=fr, name='France', opacity=op, line=line_styl),
    go.Scatter(x=years, y=ge, name='Germany', opacity=op, line=line_styl),
    go.Scatter(x=years, y=au, name='Aust', opacity=op, line=line_styl)
    
])

# Creating the layout dictionary or graph object

# Title is an immediate attribute of the layout
layout = go.Layout(title='20th Cent Life Expectancy')

# Using a complete figure object, with both data and layout
fig = go.Figure(data=data, layout=layout)

iplot(fig)

```

<!--sec data-title="Graph Title" data-id="d2" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/48.embed" height="450" width="100%"></iframe>
<!--endsec-->


<br>
# Axes

There a number of options for the way axes are formatted.  The major ones will be covered below, whilst the [online reference](https://plot.ly/python/reference/) should be consulted for all possible options.

All of these options are controlled through the attributes ```yaxis``` and ```xaxis```, which are provided to the ```layout``` dictionary.

These take dictionaries of parameters, as does practically everything in the ```layout``` dictionary.  ```go.XAxis()``` and ```go.YAxis``` can be used for convenience.


<br>
## Axis Titles


To add titles to the axes, the axis dictionaries take a ```title``` attribute as was done for whole graph.

---

Thus, to the above code, we can add the code below:
```python
...

# Define axis dictionaries using a graph object function
xax = go.XAxis(title='Year') # provide a title
yax = go.YAxis(title='Life Exp (yrs)') # provide a title

# Provide our axis objects to the layout
layout = go.Layout(title='20th Cent Life Expectancy', xaxis=xax, yaxis=yax)

...
```

<!--sec data-title="Axis Titles" data-id="d3" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/50.embed" height="450" width="100%"></iframe>
<!--endsec-->


<br>
## Tick locations and labels

Probably the most important kind of control one wants over their axes - for what values there are ticks and what the labels are.

Plotly, as you would have noticed by now, takes care of this automatically, and does a good job.

But, if you wish, you have complete control over the ticks, as well as some quick options for slightly adjusting them from the defaults.

---

### Change the number of ticks

The easiest way to adjust the number of ticks on an axis.

```nticks``` defines the maximum number of ticks, which plotly tries to get to within reason while it takes care of the rest.

---

Let's say that we aren't happy with the amount of ```XAxis``` ticks and want more so that we have a great precision for the years.  We will increase ```nticks``` to 30

```python
...
                            # maximum of 30 ticks
xax = go.XAxis(title='Year', nticks=30)
...
```
<!--sec data-title="More ticks" data-id="d4" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/52.embed" height="450" width="100%"></iframe>
<!--endsec-->


### Set the interval for ticks

A slightly more complex method is to define the interval between each tick.  With out plot, let's say 10 years.  We do this with ```dtick```, the 'd' probably standing for 'delta'.

A handy parameter that goes with this one is ```tick0```.  This defines which value the ticks start from.  In our case, where our years start at *1900* and end at *2014*, if ```dtick=10```, the first tick would be *1900*, second, *1910* and so on.  ```tick0``` lets us determine which of those first 10 years becomes the first tick.  We may, for instance, want to start on *1903* and go up in units of 10.

As plotly's default is to cover all of the data, setting ```tick0``` to a year beyond one of our intervals, say *1912*, doesn't prevent ticks appearing before that year.  The range of the axis, dealt with below, needs to be changed for that.  If ```dtick = 10``` and ```tick0 = 1912```, the ticks would be: *1902*, *1912*, ....  Plotly obeys, providing *1912* as a tick, but still covers the full data range.

```python
...
xax = go.XAxis(title='Year', dtick=10, tick0=1903)
...
,,,

```

<!--sec data-title="Tick intervals" data-id="d5" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/54.embed" height="450" width="100%"></iframe>
<!--endsec-->


### Full Control

For the whole axis, the exact set of values for which there are ticks can be specified.  Additionally, the label for each of these ticks can be specified too.

```tickvals``` takes a list (or array) and defines the values for which there will be ticks.

```ticktext```, which is necessary only if the defaults need to be changed, takes a list and defines the label for each of the tick values defined in ```tickvals```.  As these two lists go together, they must have the same number of elements.

---

For our graph, let's say that I wanted to highlight the years that World Wars 1 and 2 started, by having ticks for the years 1914 and 1939, and nothing else except for another tick in the 1960s just to highlight how awesome they were.


```python
...
xax = go.XAxis(title='Year', 
                tickvals = [1914, 1939, 1969],
                ticktext = ['WW1', 'WW2', 'peace ... man']
              )
...
```

<!--sec data-title="Full Control" data-id="d6" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/56.embed" height="450" width="100%"></iframe>
<!--endsec-->


<br>

## Axis Range

Plotly sets the range of the axes by default quite well.  In fact, it is constantly ensuring that the axis ranges are appropriate for the data in the plot.  This means that when you click a trace in the legend to toggle its appearance, the axis ranges will adjust appropriately.

Sometimes this auto-rangeing is not desirable.  Sometimes you may desire a particular range so that there is consistency between different plots for easy comparison.

```range``` takes a list with the minimum and maximum values of the axis range.  The zooming and panning interactivity is still active.  But the auto-rangeing as traces are clicked on and off of the plot is disabled.

If you wish for there to be no zooming along a particular axis, providing ```fixedrange``` a boolean (```True``` or ```False```) toggles this feature, for the particular axis.

---

Let's say we want to focus our plot on the world wars ...

```python
...
xax = go.XAxis(title='Year', dtick=5, tick0=1904, range=[1900, 1950])
...
```

<!--sec data-title="Setting the axis range" data-id="d7" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/58.embed" height="450" width="100%"></iframe>
<!--endsec-->

<br>
## Styling ticks and grids

So far, none of our ticks have had any actual 'ticks' ... that is little lines indicating the location along the axis of that particular value.  Plotly, by default, relies on a faint gray grid.

You may wish otherwise.  The following styling options are available:

<br>
**Turn ticks on**

To turn ticks on, the attribute ```ticks``` takes a string, either ```outside``` or ```inside``` depending on whether you want the ticks on the inside or outside of the plot.

<br>
**Width, length and color of the ticks**

The ticks themselves, that is the little lines, can be customised with:

* ```ticklen```
* ```tickwidth```
* ```tickcolor```

<br>
**Adding or removing the grid**
```showgrid``` takes a boolean (```True``` or ```False```)

<br>
**Grid color and width**

* ```gridcolor```
* ```gridwidth```

<br>
**Background colors**

The color of the background of the plot is adjusted with two attributes.

* ```plot_bgcolor``` - is for the plot area where the traces are grid lines are located
* ```paper_bgcolor``` - is for the remainder of the graph


# Exercise

1. Using the data provided below, make a scatter plot with appropriate axis titles an appropriate title for the whole graph.
2. Adjust the range of the axes to focus in on one part of the data (you should see a decent spread in the data).
3. Using any of the styling options mentioned above or in the [online reference](https://plot.ly/python/reference/), such as the background color, change the look and feel of your plot.  Perhaps inverting the plot, so that the background is black and all the lines white and traces are bright.
4. **Challenge** - The default scale for the axes is linear.  Can you change the scale to be logarithmic, and then still alter the range?  The [online reference](https://plot.ly/python/reference/) should help.


<!--sec data-title="Exercise Data" data-id="ex1" data-show=true data-collapse=false ces-->

The data is the life expectancy and GDP per capita for a selection of nations in the year 1900.  A scatter plot is probably the more appropriate.

```python

life_expect = [ 46.32      ,  51.95      ,  48.288448  ,  49.92647059,
        45.08      ,  43.915     ,  48.4       ,  41.66      ,
        35.6       ,  35.        ,  33.5       ,  38.6       ,
        18.35      ,  32.        ,  30.        ,  30.4       ,  21.77272727]


gdp = [8013, 5566, 4858, 6688, 4314, 4596, 6063, 3528, 2412, 1985, 2802,
       1840, 1194,  894, 1198, 1340,  995]
```
<!--endsec-->

