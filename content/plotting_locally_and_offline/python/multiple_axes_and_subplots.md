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

<br>
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

<br>
## Adding an axis

<br>
### Basics

An axis is added to the layout dictionary of a figure.  Like the default ```xaxis``` and ```yaxis```, it takes a dictionary (see [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md)).  The graph objects ```go.XAxis``` and ```go.YAxis``` can be used.

```python
fig.layout.update(yaxis2 = go.YAxis())

```

As described in [Layout - titles, axes and ticks](./layout_-_titles,_axes_and_ticks.md), by default, the attribute or key for axes in the layout dictionary of a plot are: ```xaxis``` and ```yaxis```.  That is, to modify the format of an axis, one needs to modify ```fig.layout.xaxis``` or ```fig.layout.yaxis```.

Whenever additional axes are to be added, **plotly requires** that the same attributes be used (ie, ```yaxis``` and ```xaxis```) but with the number ```2```, or ```3``` etc, for the second or third axis of that kind.  For this reason, our second yaxis has to be given to the key ```yaxis2``` in the layout dictionary.


<br>
### Positioning the new axis

The above code is incomplete and won't work.  We need to tell the new axis two things:

* Whether it is free floating or to overlap with the pre-existing axis;
* Which side of the current plot is it to be (top, bottom, left or right).

In our case, we want the new axis to be overlapping.  Like mentioned above, plotly lets axes do what ever you want, essentially, so the default is that an axis is free.  We have to tell it to be sort of 'connect' with the pre-existing yaxis.  The attribute used for this setting is ```overlaying```.  Its default is ```free```.  To connect it to a pre-existing axis, pass the kind of axis it needs to connect to.  If it needs to connect to a y axis, ```overlaying='y'```; if it needs to connect to an x axis, ```overlaying='x'```.

The default side for a y axis, is the left, whilst for an x axis, it is the bottom.  Thus, for our new y axis, by default it will literally be placed on top of the pre-existing one, which doesn't work well.  For it to be placed on the other side, we must use the attribute ```side``` and set it to the opposite of the pre-existing one, which for us, by default is on the left side.

If you'd like, try adding a new axis without these attributes set appropriately to get a an intuitive feeling for what they do.

---

So, to appropriately position our axis, we must add it with the following attributes:

```python
fig.layout.update(yaxis2 = go.YAxis(overlaying='y', side='right'))

```

You'll notice though, that neither of the traces have been bound to the new axis.  Try zooming or panning the second y axis - the new axis remains unchanged and no trace follows it ...

<!--sec data-title="Initial Plot" data-id="d3" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/66.embed" height="450" width="100%"></iframe>

<!--endsec-->


<br>
## Binding a trace to a new axis

As mentioned above, plotly is liberal with how the axes are arranged and how traces are bound to them.  Traces can be bound to any trace, technically.  By default, each trace is bound to the default or initial x and y axes.

To change this, each trace has two attributes, ```yaxis``` and ```xaxis``` that determine which axis or axes that trace is bound to.  

To repeat, these are attributes of each **trace** and are different from the attributes of the layout dictionary.  In the definition of a trace, ```xaxis``` defines **which x axis the trace will be bound to**.  In the definition of the layout ```xaxis``` defines the formatting and styling of the x axis for that figure.

In our case, we want our second trace to be bound to the second y axis.  

** Annoying Convention!!**
**Now this is oddly inconsistent**, but even though the second y axis must be called ```yaxis2```, the name we must give in the trace is not this but rather ```y2```.  It is shorter, but annoyingly inconsistent.  The same, of course, applies to any new x axes.

---

So, our code for the second trace needs to be ...

```python

go.Scatter(x = yrs, y = emp, name='Empl Rate', 

            # bind this trace to the second y axis, 
            # or the y axis defined by the attrbite "yaxis2"
            yaxis='y2')
```


<br>
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

<!--sec data-title="Finally, positioned and bound" data-id="d4" data-show=true data-collapse=false ces-->
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

<!--sec data-title="Final two Axes" data-id="d5" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/70.embed" height="450" width="100%"></iframe>

<!--endsec-->


<br>
# Two subplots

If the two traces were in their separate subplots, then we wouldn't need to worry about accommodating two scales.

---


There is a helper function that does the heavy lifting for generating subplots for us.  (It's useful to remember though that you could do it all yourself just by manipulating the positioning and binding of various axes.)


<br>
## make_subplots() function

### Import

We will need to import the helper function from ```plotly.tools```.

```python
from plotly.tools import make_subplots
```

<br>
### Initialising the figure for subplots

```make_subplots``` prepares a figure dictionary that is set up to have subplots.  

So, unlike for previous plots, if you want subplots, you will tend to *start* by defining your figure graph object or dictionary and then define your traces etc.

```make_subplots``` expects the subplots to be arranged in a grid or table, with a certain amount of rows and columns, which you have to specify.

Thus, it's main options or key-word arguments are:

* ```rows``` - number of rows of subplots
* ```cols``` - number of columns of subplots

---

For our case, we will only have two subplots.  Let's arrange them in a single row, with two columns for each of the subplots.

```python
fig = make_subplots(rows=1, cols=2)
```

---

<br>
#### The guide output

**Note** - ```make_subplots``` returns a handy summary of the grid of subplots we've just initialised ...

```python
This is the format of your plot grid:
[ (1,1) x1,y1 ]  [ (1,2) x2,y2 ]
```

* Each square brack - ```[]``` - represents a single subplot
* the numbers in round brackets - ```(1, 2)``` - represents which row and column the subplot belongs to.  Ie ```(row, col)```.
* The ```x1, y1``` tells us which of the axes are bound to each subplot.  Recall from above that ```yaxis2``` is referred to as ```y2```, ```yaxis3``` as ```y3```, etc.  These references are what we see here.  You'll notice that there are new axes for each subplot.  Ie, the second subplot has ```x2, y2```You don't really need to change these unless you're doing some serious customising.  But it is helpful to see that all this function is doing is the same sort of stuff we were doing above.

---

<br>

#### The figure object

It's worthwhile at this point to see what our figure dictionary looks like, keeping in mind that all ```make_subplots()``` has done is write out this particular figure dictionary for us.

```python
pply(fig)
```
(see [Methods for updating the figure ...](./methods_for_updating_the_figure_or_graph_objects.md) for using ```pply()```)

*returns ...*

```python
{   'data': [],
    'layout': {   'xaxis1': {   'anchor': 'y1', 'domain': [0.0, 0.45]},
                  'xaxis2': {   'anchor': 'y2', 'domain': [0.55, 1.0]},
                  'yaxis1': {   'anchor': 'x1', 'domain': [0.0, 1.0]},
                  'yaxis2': {   'anchor': 'x2', 'domain': [0.0, 1.0]}}}
```

What has been done:

* separate x and y axes were added to the layout for each subplot
* The two pairs of axes were *bound* to each other using ```'anchor': 'y1'```.
* Each axis was given a portion of the whole figure using ```'domain': [0.0, 0.45]```.  This means that the axis spans, in this example, from the bottom left to 45% of the way to the right.  FOr y axes, ```0.0``` corresponds to the top left.

**Note** - after using ```make_subplots()```, we can change these default settings to customise the spatial arrangement of our plot.



<br>

## Append traces

To add a particular trace to a particular subplot, use ```fig.append_trace(trace, row, col)```.

This is a function built into figure graph objects.  You pass into the function the trace you want append, and then the row and column *coordinates* of the subplot you want to add the trace to.  This is what the *guide output* of the ```make_subplots()``` function is really useful for.


___

For us, we'll append the robberies trace to the first subplot ```(1, 1)```, and the employment rate trace to the second subplot ```(1, 2)```.


```python
fig.append_trace(go.Scatter(x = yrs, y=robs, name='Robberies'), 
                  1, 1) # first row, first column

fig.append_trace(go.Scatter(x = yrs, y = emp, name='Empl Rate'), 
                  1, 2) # first row, second column

iplot(fig)
```

With the subplot helper functions, this is easier than adding a new axis.


<!--sec data-title="Two subplots" data-id="d6" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/72.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

It's worthwhile looking at the figure dictionary again, to see how the traces were '*appended*' to their subplots


```python
pply(fig)
```

*returns ...*

```python
{   'data': [   {   'name': 'Robberies',
                    'type': 'scatter',
                    'xaxis': 'x1',        # This how the trace is bound
                    'yaxis': 'y1'},       # This how the trace is bound
                {   'name': 'Empl Rate',
                    'type': 'scatter',
                    'xaxis': 'x2',        # This how the trace is bound   
                    'yaxis': 'y2'}],      # This how the trace is bound
    'layout': {   'xaxis1': {   'anchor': 'y1', 'domain': [0.0, 0.45]},
                  'xaxis2': {   'anchor': 'y2', 'domain': [0.55, 1.0]},
                  'yaxis1': {   'anchor': 'x1', 'domain': [0.0, 1.0]},
                  'yaxis2': {   'anchor': 'x2', 'domain': [0.0, 1.0]}}}
```

You'll notice that all '*appending*' involved was binding the trace to the appropriate axes in the same way we were binding a trace to a new y axis above.  Also notice that the appropriate axes for each subplot are those that were listed in the guide ouput of the ```make_subplots()``` function.

---

<br>

## Share Axes

With our two data sets, one axis is identical for them - *time*.  This is how we did the first plot with two y axes ... both y axes shared the same x axis.  

We do this by using the ```shared_xaxes=True``` and/or ```shared_yaxes=True``` option or key-word argument of the ```make_subplots()``` function.

```python
fig = make_suplots(rows=r, cols=c, shared_xaxes=True)
```

For our two subplots, and any subplots for that matter, x or y axes can be shared also.

So, for us, we'll rearrange our subplots into a single column, so that they can share an x axis of time.

---

<br>
### Initialise the figure

```python

# two subplots, each in a row, forming one column
fig = make_subplots(rows=2, cols=1, 
                    shared_xaxes=True) # sharing the x axis.

```

*returns ...*

```python
This is the format of your plot grid:
[ (1,1) x1,y1 ]
[ (2,1) x1,y2 ]
```

**Note** - there are two y axes (```y1``` and ```y2```) but only one x axis, that is bound to both suplots.


<br>
### Append traces

Just as before, but with the rows and cols swapped.

```python
fig.append_trace(go.Scatter(x = yrs, y=robs, name='Robberies'), 1,1)
fig.append_trace(go.Scatter(x = yrs, y = emp, name='Empl Rate'), 2, 1)
```


<!--sec data-title="Two subplots sharing an x axis" data-id="d7" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/74.embed" height="450" width="100%"></iframe>
<!--endsec-->



<br>

life expect and GDP over time (+population) - two axes, then two subplots with a shared axis

note that can customise quite a bit with idea of domain