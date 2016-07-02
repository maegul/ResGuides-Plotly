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
* Use ```graph_objs``` to put your data into a plot
* Each single plot is called a ```trace``` in plotly.  Usually you give it its own variable name.
* Put your trace, or multiple traces if you have more than one, into a list.
* Pass your list to the ```iplot``` or ```plot``` function. 

```python
# data points along the x axis
xdata = np.linspace(0, 5, 50)

# data points along the y axis
ydata = x**2

# define a single plot
trace1 = go.Scatter(x=xdata, y=ydata)

# graph all plots in the IPython notebook
iplot([trace1]) # NOTE ... traces go inside a list
```
<!--sec data-title="Hello World" data-id="d1" data-show=true data-collapse=false ces-->
<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/33.embed"></iframe>

<!--endsec-->






