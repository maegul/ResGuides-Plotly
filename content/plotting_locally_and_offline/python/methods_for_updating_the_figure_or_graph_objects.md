# Nicer Methods for updating the figure

As you've probably thought to yourself, editing and customising plotly graphs can be relatively verbose and cumbersome.

Plotly is, by design, very explicit.  Each plot has it's *'DNA'*, which outlines very clearly how the whole plot is built.  But sometimes programming a graph involves a bit too much redundant, repetitive and explicit code.

Here two general methods of dealing with and editing the code for a graph are explained which may be useful in either making the coding more efficient or making the mental task of managing the graph easier.


# Updating a graph object.

Most of the attributes of a plotly graph are in dictionaries.  There are exceptions - the data is always in a list or array, as are tick values.  But any styling or formatting options are in dictionaries.  This includes individual plots - that is, any single scatter or line with ```x``` and ```y``` data - where each one is a single dictionary.

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

# Using and editing the full description

## Copying and Pasting

Sometimes the best or easiest way to edit a particular parameter of a graph is to print out the full figure dictionary, edit as desired, and copy and paste it into an ```iplot``` function.

To copy the current description, call the figure or data or trace variable as needed.




## Update Function and looping