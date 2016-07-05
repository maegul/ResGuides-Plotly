**Table of Contents**
<!-- toc -->
---

# Layout - titles, axes and ticks

* Adjusting Graph and axis titles
* Adjusting the axis and grid lines
* Adjusting tick locations, labels and axis ranges.

<!--sec data-title="Summary" data-id="s1" data-show=true data-collapse=false ces-->

<!--endsec-->


# Layout

As described in the section on the [DNA of a plot.ly graph](./dna_of_a_plotly_graph.md), general styling of a plot.ly graph occurs in a ```layout``` dictionary, which is the second variable in a figure dictionary.

That is, the general structure of making a plot in plotly is :

```python
data = [trace1, trace2, trace3, ...]

layout = dict(style1='parameter1', style2='parameter2', ...)

fig = dict(data = data, layout=layout)

iplot(fig)
```

All of the styling in this section will be done through attributes in this ```layout``` variable.

Moreover, from here on in, we will be adding our ```data``` and ```layout``` variables to a figure dictionary, and then passing this dictionary to our ```iplot``` function.


<br>
# More graph objects

So far, we've really only used one graph object - ```go.Scatter()```.  Typing ```go.``` and hitting the ```tab``` key to see the autocomplete options will show you that there are many more handy graph objects.

Essentially, there is a graph object function for every kind of attribute needed to make a plotly graph, including ```go.Trace()```, ```go.Layout()``` and ```go.Figure()```.  You can compare back to the general structure in [DNA of a plot.ly graph](./dna_of_a_plotly_graph.md) to check this.

<br>
## What are graph objects good for ... again?

Using these functions rather than simply constructing lists and dictionaries, which is completely fine, has a few advantages:

* The function names are explicit and clear and makes it easier to identify what's going on in a bit of code.
* The functions know what attributes that they can and cannot accept, so any error reports will be more specific.
* Knowing what attributes they can accept, their help documentation lists them for easy reference.

**For example**

```python
go.Bar().help()
```
*returns ...*
```python
Valid attributes for 'bar' at path [] under parents []:

    ['orientation', 'stream', 'ysrc', 'dy', 'xsrc', 'visible', 'marker',
    'y0', 'tsrc', 'uid', 'showlegend', 'error_x', 'error_y', 'rsrc',
    'xaxis', 'text', 'bardir', 'type', 'opacity', 'legendgroup', 'textsrc',
    'dx', 'hoverinfo', 'x0', 'name', 'yaxis', 'r', 't', 'y', 'x']

Run `<bar-object>.help('attribute')` on any of the above.
'<bar-object>' is the object at []
```

<br>

* If a particular graph object is a dictionary, any of its items can be accessed directly by using ```dict.key``` notation rather than the conventional ```dict['key']``` notation.  This is not normal in python, but a feature plotly has programmed into its graph objects.

**For example**

Where the figure is defined using a graph object function ...
```python
fig = go.Figure(data=[trace1, trace2], layout=dict(...))  # Figure objects are dictionaries
```
... the underlying data or layout can be accessed by ...
```python
# conventional
fig['data'] = [trace1, trace2, trace3]

# more direct plotly graph object access
fig.data = [trace1, trace2, trace3]
```


---

# Title

gap minder data

life expectancy over time for a few countries

titles, axis titles too

manipulate axes ... logarithmic, reduce number of years, angle the labels.

change the range of years (focus on world war)
