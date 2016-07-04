<!--toc-->

**If you are not completely comfortable creating and manipulating dictionaries and lists in python, take a refresher with the [crash course in these materials](./dicts_and_lists_crash_course.md)**

# The basic idea

The two container type of variables in python, *lists and dictionaries*, can have within them other variables, including more lists and/or dictionaries.

Each plot is defined by a single dictionary.  And this dictionary, which contains further lists and dictionaries, contains all the information needed to make that plot.  

The dictionary you were asked to make in the exercises in [the crash course on lists and dicts](./dicts_and_lists_crash_course.md) is very much like the kind used by ploly.

The graph objects or traces you've been creating, such as with```go.Scatter()```, as used in this course, are essentally nested lists and dictionaries.

You would have noticed this when placing a line dictionary inside a marker dictionary inside a trace (ie ```go.Scatter(..., marker=dict( ... line=dict(...) ) )```)

<br>
# Importance

Though there are user friendly python functions that generate plotly graphs for us, sometimes it will be necessary to interact with these figure dictionaries in order to make adjustments.  Doing so may be more powerful or quicker or necessary.  So, it is useful for us to know our way around them.

<br>
# Structure

## Basic Rules
1. Everything in is a container, either a dictionary or a list
2. If a bunch variables are of the same kind and not generally unique, they go together into a **list**.  
  3. Eg - multiple traces for a single plot go into a list
3. If a bunch of variables are unique and/or require a unique identifier, they go together into a **dictionary** with a name or a key.  
  4. Eg - styling variables like ```width``` and ```color``` go into a dictionary.

<br>
## Basic Structure

* The top most container is the ```Figure``` container.  It is a dictionary.
* ```Figure``` always contains two variables: ```data``` and ```layout```.
* ```data``` is a list and contains the traces of teh plot.
* ```layout``` is a dictionary and contains general styling parameters

Thus, the basic structure for a plotly graph is:

```python
data = [trace1, trace2, trace3, ...]

layout = dict(style1='parameter1', style2='parameter2', ...)

fig = dict(data = data, layout=layout)

iplot(fig)
```

**Note** Up to now, we have been passing only a ```data``` container, that is, a list of traces, into ```iplot()```, without it being in a dictionary along with any layout variable.  This is because ```iplot()``` is happy to do that and presume default settings for the layout of the plot.  The moment any layout parameters are to be changed, then the structure above will need to be used.

<br>
## Going Deeper

Here most of the entire hierarchy of possible attributes and containers will be outlined.  Not everything will be outlined, and in the lowest container, there may be many attributes that you would want to customise, which can be seen [on the plot.ly web page here](https://plot.ly/python/reference/).  But this gives a good picture of where everything that you *could* customise would be in the 'DNA'.

```python

Figure           {}
  data           []
    trace        {}
      x, y, z    []   # these lists are the data
      color      []   # and these three are styling for each data point
      size       []
      text       []
      
      marker     {}
        color    's'
        symbol   's'
        line     {}
          width  12
          ...
        ...
        
      line       {}
        color    's'
        width    12
        dash     12/'s'
      
      opacity    12
      
      
  layout         {}
    title        's'
    xaxis        {}
      title      's'
      tickvals   []
      ticktext   []
      type       's'  # eg, logarithmic or linear
      ...
    yaxis        {}
      title      's'
      ...

      

```

