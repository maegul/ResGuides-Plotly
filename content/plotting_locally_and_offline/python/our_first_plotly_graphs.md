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

### Lines and Scatters

```python
# data points along the x axis
xdata = np.linspace(0, 5, 50)

# data points along the y axis
ydata = x**2

# define a single plot
trace1 = go.Scatter(x=xdata, y=ydata)

# graph all plots in the IPython notebook
iplot([trace1])
```
<!--sec data-title="Hello Worls" data-id="d1" data-show=true data-collapse=false ces-->
<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/33.embed"></iframe>

<!--endsec-->

#### Graph Objects
```
plotly.graph_objs
``` 
imported here as ```go```, gives us functions that provide predefined plot types.

There are many of these.  The most common is ```go.Scatter()```.  Other common ones are ```go.Bar()```, ```go.Histogram``` and ```go.Heatmap()```.

These functions




