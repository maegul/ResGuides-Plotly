# Nicer Methods for updating the figure

As you've probably thought to yourself, editing and customising plotly graphs can be relatively verbose and cumbersome.

Plotly is, by design, very explicit.  Each plot has it's *'DNA'*, which outlines very clearly how the whole plot is built.  But sometimes programming a graph involves a bit too much redundant, repetitive and explicit code.

Here two general methods of dealing with and editing the code for a graph are explained which may be useful in either making the coding more efficient or making the mental task of managing the graph easier.



# General python

One advantage of the explicit design of plotly figures is that, being made up of dictionaries and lists, ordinary python methods for manipulating these objects work just fine.  Appending to lists, using for loops and conditionals, and whatever else is possible in python can all be used effectively to intelligently edit a plotly figure object.


# Updating a graph object.

Most of the attributes of a plotly graph are in dictionaries.  There are exceptions - the data is always in a list or array, as are tick values.  But any styling or formatting options are in dictionaries.  This includes individual traces - that is, any single scatter or line with ```x``` and ```y``` data - where each one is a single dictionary.

Dictionaries have an ```update()``` function.  This function takes whatever you have passed to it, and inserts it or overwrites the particular element being updated, without overwriting anything else that is already in the dictionary.

---

For instance

```python

myDict = dict(name='Errol', age=30)

myDict.update(age=31)  # I know, I'm sad too

myDict
```

*returns ...*

```python

{'age': 31, 'name': 'Errol'}

```

---

<br>

## Plotly update function

In plotly, this update function can be applied to any plotly attribute or graph object, including the ```data``` list which has each of the traces of a graph.

This can make your code neater when you are customising a plot.  Each modification can be a small single line of code, so you can keep track of what you've done more easily.

*More significantly*, though, in combination with for loops (or when dealing with the ```data``` list, as we'll cover below), it can also make editing the plot faster.


<br>

Let's make a simple plot ...

```python

x = np.linspace(0, 4, 50)

# various linear traces ... no styling
data = [
    go.Scatter(x=x, y=x),
    go.Scatter(x=x, y=x*2),
    go.Scatter(x=x, y=x*4),
    go.Scatter(x=x, y=x*8)
]

fig = go.Figure(data=data, layout=dict())

iplot(fig)

```

<br>
### Update the layout

We haven't formatted or styled anything so far, not even the traces.

If we were to look at the figure dictionary, without the data, it would be:

```python
{   'data': [   {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'}],
    'layout': {   }}
```

Let's say we wanted the height and width of the whole graph to be the same (plotly's auto-sizing is a bit deceptive for this graph).

A single line that updates the xaxis will do the job.  **Note**, that the code below also takes advantage of the ```dict.key``` method of accessing the elements of a dictionary.  This is specific to plotly.


```python
fig.layout.update(height=500, width=500)
```

Now the figure dictionary looks like:

```python
{   'data': [   {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'}],
    'layout': {   'height': 500, 'width': 500}}
```

<br>
### Update the traces

Updating the traces works a little differently, as they are dictionaries in a list (ie each trace is a dictionary, and all the traces are stored in the list ```data```.


Let's say that we wanted all of the traces to be styled so that they had ```opacity=0.7```, ```width=10``` and ```mode='markers'```.  

We could just go and add those attributes to the code for every trace, or we could update all at once.  There are two ways to do this.


<br>

#### Use a for loop

As ```fig.data``` is a list (prove it by called ```fig.data[0]```), we can loop through each trace.  For each trace, we use the ```update()``` function as we did above.

```python

# loop through each trace in the data list, which is an element of the figure dict
for trace in fig.data:
  
  # update each trace using the update function
  trace.update(opacity=0.7, mode='markers', line=go.Line(width=10))

```

our figure dictionary now looks like:

```python
{   'data': [   {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'}],
    'layout': {   'xaxis': {   'range': [0, 30]}}}
```

<br>
#### Use only the update function

This is the most efficient way, but also less intuitive.  

**Note** - *If you're comfortable with loops in python, but find this a bit odd, sticking with the loops is perfectly fine and probably produces more readable code.*

---

You can call the ```update``` function directly on ```fig.data```.  You don't need to loop through each trace within ```fig.data``` and use the update function on them individually.  The ```update``` function does that for us.  

Also, recall that the update function *overwrites the particular element being updated, without overwriting anything else that is already in the dictionary*.

So, if we were to run:

```python
fig.data.update( dict(mode='markers') )
```

The ```update()``` function will:

* loop through each trace ...
* update each trace, which is a dictionary, with the dictionary we have provided.

As nothing is overwritten, the original contents of each trace remains, and everything new in the dictionary is inserted.  

To style the traces how we want them ...

```python
fig.data.update(dict(opacity=0.7, mode='markers', line=go.Line(width=10)))
```

The result is the same as when we ran a loop above ... every trace is updated.

For any formatting that is identical for each trace, this is the fastest way to code it.


<!--sec data-title="Before and After Demo" data-id="d1" data-show=true data-collapse=false ces-->
The results of the initial graph produced above and the updates demonstrated are below.

**Before**

<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/60.embed" height="450" width="100%"></iframe>


**After**

<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/62.embed" height="450" width="100%"></iframe>


<!--endsec-->



# Using and editing the full figure description


Sometimes the easiest way to edit the parameters of a graph is to print out the full figure dictionary, edit it as desired, and copy and paste it into an ```iplot``` function.  

Sometimes it helps to see all the settings in a structured format.


## Viewing or printing the full figure description

As a plotly graph's DNA is made up of dictionaries and lists, it can be viewed simply by called it.

We have made again a simple plot, but with some formatting and fewer data points for brevity ...

```python

x = np.linspace(0, 4, 20)

# various linear traces ... no styling
data = [
    go.Scatter(x=x, y=x, mode='markers'),
    go.Scatter(x=x, y=x*2, mode='markers+lines'),
    go.Scatter(x=x, y=x*4, line=go.Line(width=12)),
    go.Scatter(x=x, y=x*8)
]

fig = go.Figure(data=data, layout=dict(height=450, width=550))


# call fig

fig
```


Calling ```fig``` returns ...



```python
{'data': [{'mode': 'markers',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ])},
  {'mode': 'markers+lines',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.42105263,  0.84210526,  1.26315789,  1.68421053,
           2.10526316,  2.52631579,  2.94736842,  3.36842105,  3.78947368,
           4.21052632,  4.63157895,  5.05263158,  5.47368421,  5.89473684,
           6.31578947,  6.73684211,  7.15789474,  7.57894737,  8.        ])},
  {'line': {'width': 12},
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   0.84210526,   1.68421053,   2.52631579,
            3.36842105,   4.21052632,   5.05263158,   5.89473684,
            6.73684211,   7.57894737,   8.42105263,   9.26315789,
           10.10526316,  10.94736842,  11.78947368,  12.63157895,
           13.47368421,  14.31578947,  15.15789474,  16.        ])},
  {'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   1.68421053,   3.36842105,   5.05263158,
            6.73684211,   8.42105263,  10.10526316,  11.78947368,
           13.47368421,  15.15789474,  16.84210526,  18.52631579,
           20.21052632,  21.89473684,  23.57894737,  25.26315789,
           26.94736842,  28.63157895,  30.31578947,  32.        ])}],
 'layout': {'height': 450, 'width': 550}}
```


<br>

## Viewing or printing the description better - pply()

When you call the figure description, ```fig```, it has two potential problems:

* isn't in the most readable format
* It has all the data, which can get in the way of reading the formatting parameters.

An alternative is filter out the data and use a standard python library called ```pprint``` which stands for *pretty printer*.

Below, a function is defined that uses ```pprint``` for us.  

* All we have to do is pass in our figure dictionary.  
* There's also the option of printing our data too (set the key word arg ```data=True```).
* it's called ```pply``` for *pprint* + *plotly* = *pply*.

**Please copy the function code, use it and change it as you see fit**


```python
import pprint

# initialises a pretty printer
pp = pprint.PrettyPrinter(indent=4)

# We can now print with pp.pprint()

# use copy to make sure we don't break the original figure dictionary
import copy

# the function we'll use to print figure dictionaries
def pply(plyfig, data=False):
    
    # the data option allows us to control whether the data is printed or not
    if not data:
        po = copy.deepcopy(plyfig)
        po['data'] = [{i:trace[i] for i in trace if i not in ['x', 'y', 'z']} for trace in po['data']]

        pp.pprint(po)
    else:
        pp.pprint(plyfig)
```


<!--sec data-title="pply Demo" data-id="d2" data-show=true data-collapse=false ces-->


**Without pply()**
```python
fig
```

*returns ...*

```python

{'data': [{'mode': 'markers',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ])},
  {'mode': 'markers+lines',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.42105263,  0.84210526,  1.26315789,  1.68421053,
           2.10526316,  2.52631579,  2.94736842,  3.36842105,  3.78947368,
           4.21052632,  4.63157895,  5.05263158,  5.47368421,  5.89473684,
           6.31578947,  6.73684211,  7.15789474,  7.57894737,  8.        ])},
  {'line': {'width': 12},
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   0.84210526,   1.68421053,   2.52631579,
            3.36842105,   4.21052632,   5.05263158,   5.89473684,
            6.73684211,   7.57894737,   8.42105263,   9.26315789,
           10.10526316,  10.94736842,  11.78947368,  12.63157895,
           13.47368421,  14.31578947,  15.15789474,  16.        ])},
  {'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   1.68421053,   3.36842105,   5.05263158,
            6.73684211,   8.42105263,  10.10526316,  11.78947368,
           13.47368421,  15.15789474,  16.84210526,  18.52631579,
           20.21052632,  21.89473684,  23.57894737,  25.26315789,
           26.94736842,  28.63157895,  30.31578947,  32.        ])}],
 'layout': {'height': 450, 'width': 550}}
```

**with pply**

```python
pply(fig)
```

*returns...*

```python
{   'data': [   {   'mode': 'markers', 'type': 'scatter'},
                {   'mode': 'markers+lines', 'type': 'scatter'},
                {   'line': {   'width': 12}, 'type': 'scatter'},
                {   'type': 'scatter'}],
    'layout': {   'height': 450, 'width': 550}}
```



<!--endsec-->


<br>

## Using the full description

This full description has everything that makes up the plot, including the data.  In this sense, it can be a useful means of checking what's going on with the plot.  

Or, once the paraeter or attribute that is relevant to us has been identified, we can then use the ```update``` function or redo our original code accordingly. 

This full description can be copied and pasted and edited.  We can assign it to a new variable or simply pass it directly into an iplot function once edited.

<br>
### Note on copying and pasting the full description when using numpy

You'll note that in the full figure description above the data is written not as a list but as: ```'x': array([ ... ])```.  This is because we provided numpy arrays to the traces, not lists.  This is a good thing.  Numpy arrays are useful.  **But**, if we were to copy and paste the figure description above into ```iplot()```, we would get an error ...

```python
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-138-adacd319273c> in <module>()
      1 iplot({'data': [{'mode': 'markers',
      2    'type': 'scatter',
----> 3    'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
      4            1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
      5            2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,

NameError: name 'array' is not defined
```


We have imported ```numpy``` as ```np```, but the array function is ```np.array()```.  ```array()``` is not a global function.  Python is usually programmed this way to keep all the function names neat and tidy.

If we wished to copy and paste these figure descriptions, we would need to make the ```array()``` function a global variable, like so:

```python
import numpy as np
from numpy import array
```

After this, plotly won't have any problems understanding ```'x': array([...])```.

---

An alternative, which some of you may already be employing, is to use ```pylab```, which is a convenience library full of many of the useful functions for using python for research.  It's purpose is to make these useful functions global.

```python
from pylab import *
```


# Exercise

1. Copy and paste the full figure description in the collapsed section below into your own notebook or environment
2. Replicate the plot by passing it into ```iplot()``` or ```plot()```. 
  3. You may need to import array from numpy, on which see the section above.
  4. You may want to simply assign it to a a new variable, like ```fig```.
3. Update the layout to have a title using the ```update``` function
4. Update each of the traces to have whatever style you'd like using the ```update``` function.


<!--sec data-title="Exercise Data" data-id="d2" data-show=true data-collapse=true ces-->

Use this raw figure description for the exercise.

It is a plot of life expectancy over time for a few nations.  It was generated in previous chapters.

```python
{'data': [{'name': 'UK',
   'type': 'scatter',
   'x': array([1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
          1911, 1912, 1913, 1914, 1915, 1916, 1917, 1918, 1919, 1920, 1921,
          1922, 1923, 1924, 1925, 1926, 1927, 1928, 1929, 1930, 1931, 1932,
          1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941, 1942, 1943,
          1944, 1945, 1946, 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954,
          1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962, 1963, 1964, 1965,
          1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973, 1974, 1975, 1976,
          1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
          1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
          1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
          2010, 2011, 2012, 2013, 2014, 2015]),
   'y': array([ 46.32 ,  47.91 ,  49.08 ,  50.43 ,  49.11 ,  50.86 ,  50.58 ,
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
           80.8  ,  81.   ,  81.2  ,  81.4  ])},
  {'name': 'France',
   'type': 'scatter',
   'x': array([1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
          1911, 1912, 1913, 1914, 1915, 1916, 1917, 1918, 1919, 1920, 1921,
          1922, 1923, 1924, 1925, 1926, 1927, 1928, 1929, 1930, 1931, 1932,
          1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941, 1942, 1943,
          1944, 1945, 1946, 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954,
          1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962, 1963, 1964, 1965,
          1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973, 1974, 1975, 1976,
          1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
          1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
          1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
          2010, 2011, 2012, 2013, 2014, 2015]),
   'y': array([ 45.08  ,  47.01  ,  48.01  ,  48.43  ,  48.08  ,  48.36  ,
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
           81.8   ,  81.9   ])},
  {'name': 'Germany',
   'type': 'scatter',
   'x': array([1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
          1911, 1912, 1913, 1914, 1915, 1916, 1917, 1918, 1919, 1920, 1921,
          1922, 1923, 1924, 1925, 1926, 1927, 1928, 1929, 1930, 1931, 1932,
          1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941, 1942, 1943,
          1944, 1945, 1946, 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954,
          1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962, 1963, 1964, 1965,
          1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973, 1974, 1975, 1976,
          1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
          1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
          1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
          2010, 2011, 2012, 2013, 2014, 2015]),
   'y': array([ 43.915     ,  44.222     ,  44.529     ,  44.836     ,
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
           80.5       ,  80.7       ,  80.9       ,  81.1       ])},
  {'name': 'Aust',
   'type': 'scatter',
   'x': array([1900, 1901, 1902, 1903, 1904, 1905, 1906, 1907, 1908, 1909, 1910,
          1911, 1912, 1913, 1914, 1915, 1916, 1917, 1918, 1919, 1920, 1921,
          1922, 1923, 1924, 1925, 1926, 1927, 1928, 1929, 1930, 1931, 1932,
          1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941, 1942, 1943,
          1944, 1945, 1946, 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954,
          1955, 1956, 1957, 1958, 1959, 1960, 1961, 1962, 1963, 1964, 1965,
          1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973, 1974, 1975, 1976,
          1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
          1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
          1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
          2010, 2011, 2012, 2013, 2014, 2015]),
   'y': array([ 49.92647059,  50.45568627,  50.98490196,  51.51411765,
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
           81.8       ,  81.8       ,  81.8       ,  81.8       ])}],
 'layout': {}}
```
<!--endsec-->


