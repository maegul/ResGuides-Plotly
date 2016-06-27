# Introduction to Plot.ly for Python

## What the python module gives you
* The ability to generate web-based and interactive visualisations using native python code.

```python
import plotly
from plotly import graph_objects as go
from plotly.offline import iplot, init_notebook_mode

iplot([go.Scatter(x=[1,2,3], y=[1,4,9])])
```

* These visualisations may be viewed in any one of three ways:
  * As a web-page, viewed through your web-browser, but stored locally and privately on your personal computer.
  * Embedded directly in your IPython or Jupyter notebook.
  * Viewed online through the free plot.ly hosting service

## Fundamental Workings
There are two main ways you can code you plotly graphs, the **hard way** and the **easy way**.  The hard way gives you more power and options but takes longer;  the easy way is the opposite.  We'll cover both in this course.

The main difference between the two, though, is that the hard way involves editing the features of the plot directly, whilst the easy way involves using user-friendly python functions that speed up your coding and provide more helpful errors when you've done something wrong.

The main point here, though, is that by having a sense of how to edit the features of the plot directly, you get a sense of the fundamental structure of a plot.ly plot.  This structure is not complex - there just happens to be an easier way to code up a plot.ly graph by using the helpful functions in the python library.  

But, it is a comprehensive description of the graph.  It is rather like it's **DNA**.  So, when you want to do anything a bit more customised or non-trivial with a plot, you will need to be able to edit this description, or **DNA**. 



