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


