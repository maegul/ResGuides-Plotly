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
---

# Title

The title of a graph is an attribute of its ```layout```.



gap minder data

life expectancy over time for a few countries

titles, axis titles too

manipulate axes ... logarithmic, reduce number of years, angle the labels.

change the range of years (focus on world war)
