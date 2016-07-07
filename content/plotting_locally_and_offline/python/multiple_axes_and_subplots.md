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

As we can see, the data sets, the number of robberies and the employment rate require different scales.  On a single y axis, employment rate is inaccurately flat.

---

To add an additional y axis for the employment rate, there are two steps:

* Add the y-axis
* Bind the employment rate trace to the second y axis.


## Adding an axis

As described in [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md) 




<br>

demo theft and employment data
two axes then two subplots with a shared axis

life expect and GDP over time (+population) - two axes, then two subplots with a shared axis

note that can customise quite a bit with idea of domain