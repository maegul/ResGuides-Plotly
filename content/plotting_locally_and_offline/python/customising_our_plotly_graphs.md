**Table of Contents**
<!-- toc -->
---

# Customising our plot.ly graphs

## Colors, lines and markers

By the end of the exercise in the previous section, you should have ended up with a graph looking like this:

<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/38.embed"></iframe>

Here, we shall alter the styling of the lines and symbols.

---

### Styling Options

Before, we used the ```mode``` attribute to alter the appearence of the traces.  To take our options further, we will use two more attributes that are a little more complex.

Two things to note:

1. We'll use two ```attributes``` depending on the mode of the trace: 
  2. ```line``` for line traces 
  3. ```marker``` for point or scatter traces
4. These attributes do not take single string options, but dictionaries with potentially a number of ```attributes``` defined within them.

---

**If you are not completely comfortable creating and manipulating dictionaries in python, take a refresher with the crash course in these materials**

---

#### A quick note on making dictionaries  

***NB*** *If you have come straight from the crash course, you will have already covered this*

Ordinarily, dictionaries are crated in python using curly brackets, where the keys are usually strings:

```python
myDict = {'name':'Errol', 'age':30}
```

A more convenient method for us, employed in this material, is to use the function ```dict()```:

```python
myDict = dict(name='Errol', age=30)
```

It creates the same thing, doesn't require strings as keys, and uses more conventional equals signs rather than colons.  It is also more clearly identifiable in blocks of code.

---

### Styling markers

Let us style our scatter or marker plots first.

In the ```graph object``` we add the attribute ```marker```.  To this attribute we give a dictionary with all the styling attributes we want to edit for this particular trace.

The styling attributes we will be editing are:

* size
* color
* symbol
* opacity
* line

You can find a complete reference of all of these attributes [on the plot.ly web page here](https://plot.ly/python/reference/).  It is not the most attractive or user friendly reference page, but all the attributes are listed there.

---

Let us alter the color and size of the raw data scatter plot in our graph from the previous exercise.

```python

# define the traces in directly the list
data = [
    # our scatter trace
    go.Scatter(x=x, y=y2, mode='markers', name='Raw Data',
        marker=dict(    # marker takes a dictionary of more attributes
            color='Plum', # colors can be defined in a number of ways, here, with HTML names
            size=22
        )
    ),
    
    
    # curve fit traces ... not being altered here
    go.Scatter(x=x, y=ylin, mode='line', name='Linear Fit'),
    go.Scatter(x=x, y=yquad, mode='line', name='Quadratic Fit')
]

# plot the traces
iplot(data)
```



