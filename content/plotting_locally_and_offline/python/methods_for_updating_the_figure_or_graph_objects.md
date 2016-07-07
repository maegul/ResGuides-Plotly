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



You can call the ```update``` function directly on ```fig.data```.  You don't need to loop through each trace within ```fig.data``` and use the update function on them individually.  The ```update``` function does that for us.  

Also, recall that the update function *overwrites the particular element being updated, without overwriting anything else that is already in the dictionary*.

So, if we were to run:

```python
fig.data.update( dict(mode='markers') )
```

The ```update()``` function will:

* loop through each trace ...
* update each trace, which is a dictionary, with the dictionary we have provided.

As nothing is overwritten, the original contents of each trace remains, and everything new in the dictionary is inserted.  The result is the same as when we ran a for loop above. 







-before 
https://plot.ly/~research.bazaar/60.embed


# Using and editing the full description

## Copying and Pasting

Sometimes the best or easiest way to edit a particular parameter of a graph is to print out the full figure dictionary, edit as desired, and copy and paste it into an ```iplot``` function.

To copy the current description, call the figure or data or trace variable as needed.




## Update Function and looping