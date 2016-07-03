**Table of Contents**
<!-- toc -->
---

# Imports

**This is for offline usage and presumes plotly for python has been installed**

```python
# Import base library
import plotly

# Import helper functions for making different kinds of plots
from plotly import graph_objs as go

# import offline plotting functions
from plotly.offline import iplot, plot, init_notebook_mode

# prepare the notebook to embed plotly graphs
init_notebook_mode()

# import numpy for convenience
import numpy as np
```

# Our first plots

## Basic Functions
### Graph Objects
```
plotly.graph_objs
``` 
 ... imported here as ```go```, gives us functions that provide predefined plot types.

There are many of these.  The most common is ```go.Scatter()```.  Other common ones are ```go.Bar()```, ```go.Histogram``` and ```go.Heatmap()```.

These functions require only the bare information for your plot, usually just the data, and take care of the styling themselves.

Importantly though, they do provide a number of options for customising your plot, should you desire to do so.

They accept key word arguments for all of their options.

First, we'll focus on the most fundamental kind of plots ... using ```go.Scatter()``` to make **Line and Scatter Plots**.

<br>

### FINALLY Plotting

```iplot``` will embed plots into the notebook.  The 'i' in '**i**plot' stands for the 'i' in '**i**Python Notebook', which is what the tool used to be called before it becaume the Jupyter Notebook.

```plot``` will save the plot to an independent html file in the local directory.  This file can be opened by any browser, and will be opened automatically.  There is the option for giving the file your own filename.

## Lines and Scatters

### The usual process
* Use a ```graph object``` from ```graph_objs``` to put your data into a plot
* Each single plot is called a ```trace``` in plotly.  Usually you give it its own variable name.
* Put your trace, or multiple traces if you have more than one, into a list.
* Pass your list to the ```iplot``` or ```plot``` function. 

---

```python
# data points along the x axis
xdata = np.linspace(0, 5, 50)

# data points along the y axis
ydata = x**2

# define a single plot
trace = go.Scatter(x=xdata, y=ydata)

# graph all plots in the IPython notebook
iplot([trace]) # NOTE ... traces go inside a list
```
<!--sec data-title="Hello World" data-id="d1" data-show=true data-collapse=false ces-->
<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/33.embed"></iframe>

<!--endsec-->

### Lines or points

Most common stylistic choice — whether to plot your data points as lines or points.

Despite its name, ```go.Scatter``` does both.  It is really the '*go-to*' plotting function.

To go between lines and dots, you must use our first attribute in a ```graph object```.

The attribute is ```mode```.  It has the following options:

* 'markers' ... renders data points as points or symbol; the symbol can be customised 
* 'lines' ... renders as simple lines
* 'text' ... renders only the text associated with the data point.  We don't have any yet, but will later.

<br>
your trace code will now look like this:
```python
...
# define a single plot ... now with a mode option
trace1 = go.Scatter(x=xdata, y=ydata, mode='markers')
...
```

To combine either of the modes simultaneously, connect them into a single string with a '+' symbol: ```markers+lines``` or ```lines+text``` or ```lines+markers+text```.

<br>
## Multiple plots on a single figure

When we define our plots using ```go.Scatter()``` or another ```graph object```, which plotly calls '*traces*', we put them into a list and pass that list to ```iplot``` or ```plot```.  Eg ```iplot([trace])```


To make multiple plots on a single figure, create multiple traces using the ```graph object``` functions, and put each one into the list that you give to ```iplot```.  Each one will be plotted independently.

### Legends

To give each trace a unique name for a legend, use the option ```name``` for each trace, providing a string.  That name will appear automatically in a legend formatted by plotly.

**Note** The automatically generated legend is also interactive.  Clicking each trace name toggles whether that trace appears in the plot or not.

---
```python
x = np.linspace(0, 5, 50)

# Three sets of y-axis data
y1 = x**2
y2 = 15*np.sin(x)
y3 = 10*np.log(x)

# Three traces, each with a unique data set, mode and name
trace1 = go.Scatter(x=x, y=x**2, mode='markers', name='Markers')
trace2 = go.Scatter(x=x, y=y2, mode='lines', name='Lines')
trace3 = go.Scatter(x=x, y=y3, mode='lines+markers', name='Lines and Markers')

# put each trace into a single list, and plot all at once.
iplot([trace1, trace2, trace3])
```
<!--sec data-title="Multiple traces with legend" data-id="d2" data-show=true data-collapse=false ces-->
<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/35.embed"></iframe>
<!--endsec-->

---

# Exercise 1

* In the section *Exercise Data* below, there is a data set broken up into x and y components.  Copy and paste this data into your notebook or environment.
* Generate a plot, using either ```iplot``` or ```plot```, of this data.
* Change the ```mode``` of your plot.  Which is best?


<!--sec data-title="Exercise 1 Data" data-id="d3" data-show=true data-collapse=true ces-->

**Notes:**

* Below are the data sets to be plotted.
* They are provided as lists that can copy and pasted to your notebook or terminal or IDE.
* They may be converted to numpy arrays by performing the following: 

```python
x = np.array(x) # x is now an array
y = np.array(y) # y is now an array
```

<br>

**The raw data:**

```python

x = [ 0.        ,  0.12244898,  0.24489796,  0.36734694,  0.48979592,
        0.6122449 ,  0.73469388,  0.85714286,  0.97959184,  1.10204082,
        1.2244898 ,  1.34693878,  1.46938776,  1.59183673,  1.71428571,
        1.83673469,  1.95918367,  2.08163265,  2.20408163,  2.32653061,
        2.44897959,  2.57142857,  2.69387755,  2.81632653,  2.93877551,
        3.06122449,  3.18367347,  3.30612245,  3.42857143,  3.55102041,
        3.67346939,  3.79591837,  3.91836735,  4.04081633,  4.16326531,
        4.28571429,  4.40816327,  4.53061224,  4.65306122,  4.7755102 ,
        4.89795918,  5.02040816,  5.14285714,  5.26530612,  5.3877551 ,
        5.51020408,  5.63265306,  5.75510204,  5.87755102,  6.        ]

y = [ -4.77230983,  -5.22659968,  -6.10912627,   2.62439273,
         3.17193212,   3.92985444,   4.32653827,  -0.47683265,
         0.17638539,   4.88802425,  -0.29274781,  -4.0633262 ,
        -0.05369636,   2.42199466,   7.87335613,   2.92485951,
         3.83656283,   3.03218709,   2.47220117,   5.01351618,
        13.45426071,   5.59004046,  11.15600962,   2.41768145,
        12.68859787,  12.64836321,  12.48045846,   3.90270861,
        11.34526527,   4.63140355,  11.49365356,  13.59514573,
        19.88436659,   9.18282506,  19.14753706,  19.60772532,
        20.88308577,  20.05346221,  26.35313549,  18.68721231,
        24.04982145,  28.52843377,  22.62437669,  35.89023336,
        29.58917845,  37.07338193,  31.38718976,  28.33350353,
        42.82223893,  30.69027333]
```


**Y axis data points for the linear curve fit**

```python
y_linear = [ -6.76139873,  -5.99082022,  -5.22024171,  -4.44966321,
        -3.6790847 ,  -2.90850619,  -2.13792768,  -1.36734918,
        -0.59677067,   0.17380784,   0.94438635,   1.71496486,
         2.48554336,   3.25612187,   4.02670038,   4.79727889,
         5.56785739,   6.3384359 ,   7.10901441,   7.87959292,
         8.65017143,   9.42074993,  10.19132844,  10.96190695,
        11.73248546,  12.50306396,  13.27364247,  14.04422098,
        14.81479949,  15.58537799,  16.3559565 ,  17.12653501,
        17.89711352,  18.66769203,  19.43827053,  20.20884904,
        20.97942755,  21.75000606,  22.52058456,  23.29116307,
        24.06174158,  24.83232009,  25.6028986 ,  26.3734771 ,
        27.14405561,  27.91463412,  28.68521263,  29.45579113,
        30.22636964,  30.99694815]
```

** Y axis data points for the quadratic curve fit**
```python
y_quadratic = [ -1.02315297,  -0.9552168 ,  -0.85800387,  -0.73151417,
        -0.57574771,  -0.39070448,  -0.17638449,   0.06721226,
         0.34008578,   0.64223607,   0.97366311,   1.33436692,
         1.7243475 ,   2.14360484,   2.59213894,   3.06994981,
         3.57703744,   4.11340183,   4.67904299,   5.27396091,
         5.8981556 ,   6.55162705,   7.23437527,   7.94640025,
         8.68770199,   9.4582805 ,  10.25813577,  11.08726781,
        11.94567661,  12.83336217,  13.7503245 ,  14.69656359,
        15.67207945,  16.67687207,  17.71094145,  18.7742876 ,
        19.86691051,  20.98881019,  22.13998663,  23.32043984,
        24.5301698 ,  25.76917654,  27.03746004,  28.3350203 ,
        29.66185732,  31.01797111,  32.40336166,  33.81802898,
        35.26197306,  36.73519391]
```
<!--endsec-->

# Exercise 2

* In the section *Exercise Data* below, two more bits of data have been provided — the results of trying to fit two curves to the raw data given above.  
* The first curve fit was for a linear curve, and the second for a quadratic or parabola curve.
* Add these two data sets to your previous plot
* Give each of the trace appropriate names for the legend.
* Select an appropriate '*mode*' (ie ```markers``` or ```lines```) for each of the traces.


<!--sec data-title="Exercise 2 Data" data-id="d4" data-show=true data-collapse=true ces-->


**Y axis data points for the linear curve fit**

```python
y_linear = [ -6.76139873,  -5.99082022,  -5.22024171,  -4.44966321,
        -3.6790847 ,  -2.90850619,  -2.13792768,  -1.36734918,
        -0.59677067,   0.17380784,   0.94438635,   1.71496486,
         2.48554336,   3.25612187,   4.02670038,   4.79727889,
         5.56785739,   6.3384359 ,   7.10901441,   7.87959292,
         8.65017143,   9.42074993,  10.19132844,  10.96190695,
        11.73248546,  12.50306396,  13.27364247,  14.04422098,
        14.81479949,  15.58537799,  16.3559565 ,  17.12653501,
        17.89711352,  18.66769203,  19.43827053,  20.20884904,
        20.97942755,  21.75000606,  22.52058456,  23.29116307,
        24.06174158,  24.83232009,  25.6028986 ,  26.3734771 ,
        27.14405561,  27.91463412,  28.68521263,  29.45579113,
        30.22636964,  30.99694815]
```

** Y axis data points for the quadratic curve fit**
```python
y_quadratic = [ -1.02315297,  -0.9552168 ,  -0.85800387,  -0.73151417,
        -0.57574771,  -0.39070448,  -0.17638449,   0.06721226,
         0.34008578,   0.64223607,   0.97366311,   1.33436692,
         1.7243475 ,   2.14360484,   2.59213894,   3.06994981,
         3.57703744,   4.11340183,   4.67904299,   5.27396091,
         5.8981556 ,   6.55162705,   7.23437527,   7.94640025,
         8.68770199,   9.4582805 ,  10.25813577,  11.08726781,
        11.94567661,  12.83336217,  13.7503245 ,  14.69656359,
        15.67207945,  16.67687207,  17.71094145,  18.7742876 ,
        19.86691051,  20.98881019,  22.13998663,  23.32043984,
        24.5301698 ,  25.76917654,  27.03746004,  28.3350203 ,
        29.66185732,  31.01797111,  32.40336166,  33.81802898,
        35.26197306,  36.73519391]
```
<!--endsec-->