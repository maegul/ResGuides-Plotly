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

As we can see, the data sets, the number of robberies and the employment rate, require different scales.  On a single y axis, employment rate is inaccurately flat.

---

To add an additional y axis for the employment rate, there are two steps:

* Add the y-axis
* Bind the employment rate trace to the second y axis.


## Adding an axis

### Basics

An axis is added to the layout dictionary of a figure.  Like the default ```xaxis``` and ```yaxis```, it takes a dictionary (see [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md)).  The graph objects ```go.XAxis``` and ```go.YAxis``` can be used.

```python
fig.layout.update(yaxis2 = go.YAxis())

```

As described in [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md), by default, the attribute or key for axes in the layout dictionary of a plot are: ```xaxis``` and ```yaxis```.  That is, to modify the format an axis, one needs to modify ```fig.layout.xaxis``` or ```fig.layout.yaxis```.

Whenever additional axes are to be added, **plotly requires** that the same attributes be used (ie, ```yaxis``` and ```xaxis```) but with the number ```2```, or ```3``` etc, for the second or third axis of that kind.  For this reason, our second yaxis has to be given to the key ```yaxis2``` in the layout dictionary.


### Positioning the new axis

The above code is incomplete and won't work.  We need to tell the new axis two things:

* Whether it is free floating or to overlap with the pre-existing axis;
* Which side of the current plot is it to be (top, bottom, left or right).

In our case, we want the new axis to be overlapping.  Like mentioned above, plotly lets axes do what ever you want, essentially, so the default is that an axis is free.  We have to tell it to be sort of 'connect' with the pre-existing yaxis.  The attribute used for this setting is ```overlaying```.  Its default is ```free```.  To connect it to a pre-existing axis, pass the kind of axis it needs to connect to.  If it needs to connect to a y axis, ```overlaying='y'```; if it needs to connect to an x axis, ```overlaying='x'```.

The default side for a y axis, is the left, whilst for an x axis, it is the left.  Thus, for our new y axis, by default it will literally be placed on top of the pre-existing one, which doesn't work well.  For it to be placed on the other side, we must use the attribute ```side``` and set it to the opposite of the pre-existing one, which for us, by default is on the left side.

If you'd like, try adding a new axis without these attributes set appropriately to get a an intuitive feeling for what they do.

---

So, to appropriately position our axis, we must add it with the following attributes:

```python
fig.layout.update(yaxis2 = go.YAxis(overlaying='y', side='right'))

```

You'll notice though, that neither of the traces have been bound to the new axis.  Try panning and zooming - the new axis remains unchanged ...

<!--sec data-title="Initial Plot" data-id="d2" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/66.embed" height="450" width="100%"></iframe>

<!--endsec-->


## Binding a trace to a new axis

As mentioned above, plotly is liberal with how the axes are arranged and how traces are bound to them.  Traces can be bound to any trace, technically.  By default, each trace is bound to the default or initial x and y axes.

To change this, each trace has two attributes, ```yaxis``` and ```xaxis``` that determine which axis or axes that trace is bound to.

In our case, we want our second trace to be bound to the second y axis.  **Now this is oddly inconsistent**, but even though the second y axis must be called ```yaxis2```, the name we must give in the trace is not this but rather ```y2```.  It is shorter, but annoyingly inconsistent.  The same, of course, applies to any new x axes.

---

So, our code for the second trace needs to be ...

```python

go.Scatter(x = yrs, y = emp, name='Empl Rate', 
            yaxis='y2')
```


## Final

The final code for a second y axis would look something like

```python
data = [
    go.Scatter(x = yrs, y=robs, name='Robberies'),
    
    go.Scatter(x = yrs, y = emp, name='Empl Rate', 
                yaxis='y2') # binding to the second y axis
]

# settings for the new y axis
y2 = go.YAxis(overlaying='y', side='right')

# adding the second y axis
layout = go.Layout(yaxis2=y2)

fig = go.Figure(data=data, layout=go.Layout(yaxis2=y2))

iplot(fig)
```

<!--sec data-title="Positioned and bound" data-id="d3" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/68.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

<br>

Adding some color to the axes to make it clearer which is for which trace is often helpful.

```python

data = [
    go.Scatter(x = yrs, y=robs, name='Robberies'),
    go.Scatter(x = yrs, y = emp, name='Empl Rate', yaxis='y2')
]

# Add titles and color the font of the titles to match that of the traces
# 'SteelBlue' and 'DarkOrange' are the defaults of the first two colors.

y1 = go.YAxis(title='Robberies per yr', titlefont=go.Font(color='SteelBlue'))
y2 = go.YAxis(title= 'Employment Rate', titlefont=go.Font(color='DarkOrange'))

# update second y axis to be position appropriately
y2.update(overlaying='y', side='right')
             
# Add the pre-defined formatting for both y axes 
layout = go.Layout(yaxis1 = y1, yaxis2 = y2)

fig = go.Figure(data=data, layout=layout)

iplot(fig)

```

<!--sec data-title="Final two Axes" data-id="d4" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/70.embed" height="450" width="100%"></iframe>

<!--endsec-->


<br>
# Two subplots



<br>

life expect and GDP over time (+population) - two axes, then two subplots with a shared axis

note that can customise quite a bit with idea of domain