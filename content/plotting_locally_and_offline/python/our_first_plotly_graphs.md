**Table of Contents**
<!-- toc -->

# Our first plot.ly graphs

## Imports

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

## Our first plots

### Basic Functions
#### Graph Objects
```
plotly.graph_objs
``` 
 ... imported here as ```go```, gives us functions that provide predefined plot types.

There are many of these.  The most common is ```go.Scatter()```.  Other common ones are ```go.Bar()```, ```go.Histogram``` and ```go.Heatmap()```.

These functions require only the bare information for your plot, usually just the data, and take care of the styling themselves.

Importantly though, they do provide a number of options for customising your plot, should you desire to do so.

First, we'll focus on the most fundamental kind of plots ... using ```go.Scatter()``` to make **Line and Scatter Plots**.

<br>

#### FINALLY Plotting

```iplot``` will embed plots into the notebook.  The 'i' in '**i**plot' stands for the 'i' in '**i**Python Notebook', which is what the tool used to be called before it becaume the Jupyter Notebook.

```plot``` will save the plot to an independent html file in the local directory.  This file can be opened by any browser, and will be opened automatically.  There is the option for giving the file your own filename.

### Lines and Scatters

#### The usual process
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

#### Lines or points

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
### Multiple plots on a single figure

When we define our plots using ```go.Scatter()``` or another ```graph object```, which plotly calls '*traces*', we put them into a list and pass that list to ```iplot``` or ```plot```.  Eg ```iplot([trace])```


To make multiple plots on a single figure, create multiple traces using the ```graph object``` functions, and put each one into the list that you give to ```iplot```.  Each one will be plotted independently.

#### Legends

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

