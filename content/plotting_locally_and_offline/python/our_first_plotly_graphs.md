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

To go between lines and dots, you must use our first option in a ```graph object```.

The option is ```mode```.  It has the following options:

* 'markers' ... renders data points as points or symbol; the symbol can be customised 
* 'lines' ... renders as simple lines
* 'text' ... renders only the text associated with the data point.  We don't have any yet, but will later.

<br>
your trace will now look like this:
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

# Exercise

* In the section *Exercise Data* below, three bits of data have been provided — Some raw data and the results of trying to fit two curves to that data.  The first curve fit was for a linear curve, and the second for a quadratic or parabola curve.
* Plot the raw data as well as the two curves.
* Give each of the trace appropriate names for the legend.
* Select an appropriate '*mode*' (ie ```markers``` or ```lines```) for each of the traces.

<!--sec data-title="Exercise Data" data-id="d3" data-show=true data-collapse=true ces-->

**Notes:**

* Below are the data sets to be plotted.
* They are provided as lists that can copy and pasted to your notebook or terminal or IDE.
* They may be converted to numpy arrays by performing the following: 

```python
x = np.array(x) # x is now an array
y = np.array(y) # y is now an array
```

<br>
**Curve Fit Results:**
```python
linfit = [ 5.54992634, -4.35896843]

quadfit = [ 0.81263065,  0.67414246,  0.46756511]
```

The ordering of these numbers corresponds to *a, b, c* where ...

{% math %}
  y_{lin} = ax + b
{% endmath %}

{% math %}
  y_{quad} = ax^2 + bx + c
{% endmath %}


Use these curve fit results as follows:
```python
lin_curve = linfit[0]*x + linfit[1]
quad_curve = quadfit[0] * x**2 + quadfit[1]*x + quadfit[2]
```


```python

x = [ 0.        ,  0.06060606,  0.12121212,  0.18181818,  0.24242424,
         0.3030303 ,  0.36363636,  0.42424242,  0.48484848,  0.54545455,
         0.60606061,  0.66666667,  0.72727273,  0.78787879,  0.84848485,
         0.90909091,  0.96969697,  1.03030303,  1.09090909,  1.15151515,
         1.21212121,  1.27272727,  1.33333333,  1.39393939,  1.45454545,
         1.51515152,  1.57575758,  1.63636364,  1.6969697 ,  1.75757576,
         1.81818182,  1.87878788,  1.93939394,  2.        ,  2.06060606,
         2.12121212,  2.18181818,  2.24242424,  2.3030303 ,  2.36363636,
         2.42424242,  2.48484848,  2.54545455,  2.60606061,  2.66666667,
         2.72727273,  2.78787879,  2.84848485,  2.90909091,  2.96969697,
         3.03030303,  3.09090909,  3.15151515,  3.21212121,  3.27272727,
         3.33333333,  3.39393939,  3.45454545,  3.51515152,  3.57575758,
         3.63636364,  3.6969697 ,  3.75757576,  3.81818182,  3.87878788,
         3.93939394,  4.        ,  4.06060606,  4.12121212,  4.18181818,
         4.24242424,  4.3030303 ,  4.36363636,  4.42424242,  4.48484848,
         4.54545455,  4.60606061,  4.66666667,  4.72727273,  4.78787879,
         4.84848485,  4.90909091,  4.96969697,  5.03030303,  5.09090909,
         5.15151515,  5.21212121,  5.27272727,  5.33333333,  5.39393939,
         5.45454545,  5.51515152,  5.57575758,  5.63636364,  5.6969697 ,
         5.75757576,  5.81818182,  5.87878788,  5.93939394,  6.        ]

y = [ -3.09233291e+00,   1.90717526e+00,  -5.69336351e-01,
          6.39914254e+00,  -2.17938388e+00,   8.72436651e+00,
         -7.36819806e+00,  -1.08437506e+01,   1.12980028e+01,
          6.31370006e-01,  -5.20210152e-01,   5.09465776e+00,
          2.21541613e+00,  -1.01217766e-02,  -4.68358528e+00,
          1.07158595e+00,   8.72718720e+00,  -3.09047307e+00,
          7.77094183e+00,   4.11756603e-01,   2.73233371e-01,
          3.09812258e+00,   1.46783963e-01,   4.97534776e+00,
          3.85660223e+00,   6.53119392e+00,   7.56149197e-01,
          4.12488410e+00,   2.33389129e+00,   5.11983041e+00,
          8.81718577e+00,   6.29290093e+00,   9.60142954e+00,
          1.06283855e+01,   1.03757766e+01,   2.87649711e-01,
          1.62231372e+01,   5.07861098e+00,   4.58831223e+00,
          5.40874424e+00,   5.14439855e+00,   6.56077653e+00,
          6.33345667e+00,   9.36323324e+00,   3.70292067e+00,
          1.02853050e+01,   6.94632835e+00,   8.79368194e+00,
          6.51028976e+00,   3.57346350e+00,  -4.25803408e+00,
          1.38133933e+01,   1.34639094e+01,   9.32537293e+00,
          1.40467984e+01,   2.56357083e+00,   8.17839257e+00,
          1.33301921e+01,   1.85428359e+01,   7.91668400e+00,
          2.16110874e+01,   1.68932180e+01,   1.48578946e+01,
          1.02573628e+01,   1.32339571e+01,   7.63886671e+00,
          2.72152824e+01,   1.96825771e+01,   1.29485692e+01,
          1.65348439e+01,   1.66771927e+01,   2.60677011e+01,
          1.26407244e+01,   2.04887472e+01,   2.17071719e+01,
          3.19046545e+01,   1.89442060e+01,   2.12339327e+01,
          1.75357528e+01,   1.86089298e+01,   2.09460276e+01,
          2.45535713e+01,   2.73048888e+01,   3.40154025e+01,
          2.86336815e+01,   1.45609864e+01,   2.91533720e+01,
          1.87013856e+01,   2.92753586e+01,   3.79359273e+01,
          2.72558198e+01,   3.06470096e+01,   2.81501572e+01,
          3.67861120e+01,   2.61474646e+01,   3.23849518e+01,
          2.11768805e+01,   2.95325072e+01,   3.84354289e+01,
          3.22521014e+01]
```
<!--endsec-->