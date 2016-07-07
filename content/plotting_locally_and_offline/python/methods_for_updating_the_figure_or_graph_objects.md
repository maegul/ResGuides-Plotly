# Nicer Methods for updating the figure

As you've probably thought to yourself, editing and customising plotly graphs can be relatively verbose and cumbersome.

Plotly is, by design, very explicit.  Each plot has it's *'DNA'*, which outlines very clearly how the whole plot is built.  But sometimes programming a graph involves a bit too much redundant, repetitive and explicit code.

Here two general methods of dealing with and editing the code for a graph are explained which may be useful in either making the coding more efficient or making the mental task of managing the graph easier.



# General python

One advantage of the explicit design of plotly figures is that, being made up of dictionaries and lists, ordinary python methods for manipulating these objects work just fine.  Appending to lists, using for loops and conditionals, and whatever else is possible in python can all be used effectively to intelligently edit a plotly figure object.


# Updating a graph object.

Most of the attributes of a plotly graph are in dictionaries.  There are exceptions - the data is always in a list or array, as are tick values.  But any styling or formatting options are in dictionaries.  This includes individual traces - that is, any single scatter or line with ```x``` and ```y``` data - where each one is a single dictionary.

Dictionaries have an ```update()``` function.  This function takes whatever you have passed to it, and inserts it or overwrites the particular element being updated, without overwriting anything else that is already in the dictionary.

---

For instance

```python

myDict = dict(name='Errol', age=30)

myDict.update(age=31)  # I know, I'm sad too

myDict
```

*returns ...*

```python

{'age': 31, 'name': 'Errol'}

```

---

<br>

## Plotly update function

In plotly, this update function can be applied to any plotly attribute or graph object, including the ```data``` list which has each of the traces of a graph.

This can make your code neater when you are customising a plot.  Each modification can be a small single line of code, so you can keep track of what you've done more easily.

*More significantly*, though, in combination with for loops (or when dealing with the ```data``` list, as we'll cover below), it can also make editing the plot faster.


<br>

Let's make a simple plot ...

```python

x = np.linspace(0, 4, 50)

# various linear traces ... no styling
data = [
    go.Scatter(x=x, y=x),
    go.Scatter(x=x, y=x*2),
    go.Scatter(x=x, y=x*4),
    go.Scatter(x=x, y=x*8)
]

fig = go.Figure(data=data, layout=dict())

iplot(fig)

```

<br>
### Update the layout

We haven't formatted or styled anything so far, not even the traces.

If we were to look at the figure dictionary, without the data, it would be:

```python
{   'data': [   {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'}],
    'layout': {   }}
```

Let's say we wanted the height and width of the whole graph to be the same (plotly's auto-sizing is a bit deceptive for this graph).

A single line that updates the xaxis will do the job.  **Note**, that the code below also takes advantage of the ```dict.key``` method of accessing the elements of a dictionary.  This is specific to plotly.


```python
fig.layout.update(height=500, width=500)
```

Now the figure dictionary looks like:

```python
{   'data': [   {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'},
                {   'type': 'scatter'}],
    'layout': {   'height': 500, 'width': 500}}
```

<br>
### Update the traces

Updating the traces works a little differently, as they are dictionaries in a list (ie each trace is a dictionary, and all the traces are stored in the list ```data```.


Let's say that we wanted all of the traces to be styled so that they had ```opacity=0.7```, ```width=10``` and ```mode='markers'```.  

We could just go and add those attributes to the code for every trace, or we could update all at once.  There are two ways to do this.


<br>

#### Use a for loop

As ```fig.data``` is a list (prove it by called ```fig.data[0]```), we can loop through each trace.  For each trace, we use the ```update()``` function as we did above.

```python

# loop through each trace in the data list, which is an element of the figure dict
for trace in fig.data:
  
  # update each trace using the update function
  trace.update(opacity=0.7, mode='markers', line=go.Line(width=10))

```

our figure dictionary now looks like:

```python
{   'data': [   {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'},
                {   'line': {   'width': 10},
                    'mode': 'markers',
                    'opacity': 0.7,
                    'type': 'scatter'}],
    'layout': {   'xaxis': {   'range': [0, 30]}}}
```

<br>
#### Use only the update function

This is the most efficient way, but also less intuitive.  

**Note** - *If you're comfortable with loops in python, but find this a bit odd, sticking with the loops is perfectly fine and probably produces more readable code.*

---

You can call the ```update``` function directly on ```fig.data```.  You don't need to loop through each trace within ```fig.data``` and use the update function on them individually.  The ```update``` function does that for us.  

Also, recall that the update function *overwrites the particular element being updated, without overwriting anything else that is already in the dictionary*.

So, if we were to run:

```python
fig.data.update( dict(mode='markers') )
```

The ```update()``` function will:

* loop through each trace ...
* update each trace, which is a dictionary, with the dictionary we have provided.

As nothing is overwritten, the original contents of each trace remains, and everything new in the dictionary is inserted.  

To style the traces how we want them ...

```python
fig.data.update(dict(opacity=0.7, mode='markers', line=go.Line(width=10)))
```

The result is the same as when we ran a loop above ... every trace is updated.

For any formatting that is identical for each trace, this is the fastest way to code it.


<!--sec data-title="Before and After Demo" data-id="d1" data-show=true data-collapse=false ces-->
The results of the initial graph produced above and the updates demonstrated are below.

**Before**

<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/60.embed" height="450" width="100%"></iframe>


**After**

<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/62.embed" height="450" width="100%"></iframe>


<!--endsec-->



# Using and editing the full figure description


Sometimes the easiest way to edit the parameters of a graph is to print out the full figure dictionary, edit it as desired, and copy and paste it into an ```iplot``` function.  

Sometimes it helps to see all the settings in a structured format.


## Viewing or printing the full figure description

As a plotly graph's DNA is made up of dictionaries and lists, it can be viewed simply by called it.

We have made again a simple plot, but with some formatting and fewer data points for brevity ...

```python

x = np.linspace(0, 4, 20)

# various linear traces ... no styling
data = [
    go.Scatter(x=x, y=x, mode='markers'),
    go.Scatter(x=x, y=x*2, mode='markers+lines'),
    go.Scatter(x=x, y=x*4, line=go.Line(width=12)),
    go.Scatter(x=x, y=x*8)
]

fig = go.Figure(data=data, layout=dict(height=450, width=550))


# call fig

fig
```


Calling ```fig``` returns ...



```python
{'data': [{'mode': 'markers',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ])},
  {'mode': 'markers+lines',
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([ 0.        ,  0.42105263,  0.84210526,  1.26315789,  1.68421053,
           2.10526316,  2.52631579,  2.94736842,  3.36842105,  3.78947368,
           4.21052632,  4.63157895,  5.05263158,  5.47368421,  5.89473684,
           6.31578947,  6.73684211,  7.15789474,  7.57894737,  8.        ])},
  {'line': {'width': 12},
   'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   0.84210526,   1.68421053,   2.52631579,
            3.36842105,   4.21052632,   5.05263158,   5.89473684,
            6.73684211,   7.57894737,   8.42105263,   9.26315789,
           10.10526316,  10.94736842,  11.78947368,  12.63157895,
           13.47368421,  14.31578947,  15.15789474,  16.        ])},
  {'type': 'scatter',
   'x': array([ 0.        ,  0.21052632,  0.42105263,  0.63157895,  0.84210526,
           1.05263158,  1.26315789,  1.47368421,  1.68421053,  1.89473684,
           2.10526316,  2.31578947,  2.52631579,  2.73684211,  2.94736842,
           3.15789474,  3.36842105,  3.57894737,  3.78947368,  4.        ]),
   'y': array([  0.        ,   1.68421053,   3.36842105,   5.05263158,
            6.73684211,   8.42105263,  10.10526316,  11.78947368,
           13.47368421,  15.15789474,  16.84210526,  18.52631579,
           20.21052632,  21.89473684,  23.57894737,  25.26315789,
           26.94736842,  28.63157895,  30.31578947,  32.        ])}],
 'layout': {'height': 450, 'width': 550}}
```

<br>

## Using the full description





