**Table of Contents**
<!-- toc -->
---

# Customising our plot.ly graphs

## Colors, lines and symbols

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
myDict = dict(name='Errol, age=30)
```

It creates the same thing, doesn't require strings as keys, and uses more conventional equals signs rather than colons.  It is also more clearly identifiable in blocks of code.

---


