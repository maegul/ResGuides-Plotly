**Table of Contents**
<!-- toc -->
---

# Customising our plot.ly graphs

* Adjusting the symbols, colors and opacity of markers
* Adjusting the width and color of lines
* Introducing the way plotly specifies all details of the plot.

<!--sec data-title="Summary" data-id="s1" data-show=true data-collapse=false ces-->

<!--endsec-->

<br>

By the end of the exercise in the previous section, you should have ended up with a graph looking like this:

<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/38.embed"></iframe>

Here, we shall alter the styling of the lines and symbols.

---

# Styling Options

Before, we used the ```mode``` attribute to alter the appearence of the traces.  To take our options further, we will use two more attributes that are a little more complex.

Two things to note:

1. We'll use two ```attributes``` depending on the mode of the trace: 
  2. ```line``` for line traces 
  3. ```marker``` for point or scatter traces
4. These attributes do not take single string options, but dictionaries with potentially a number of ```attributes``` defined within them.

---

**If you are not completely comfortable creating and manipulating dictionaries in python, take a refresher with the [crash course in these materials](./dicts_and_lists_crash_course.md)**

---

## A quick note on making dictionaries  

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

# Styling markers

Let us style our scatter or marker plots first.

In the ```graph object``` we add the attribute ```marker```.  To this attribute we give a dictionary with all the styling attributes we want to edit for this particular trace.

The styling attributes we will be editing are:

* size
* color
* symbol
* opacity
* line

Code for our trace will look like this:
```python
trace1 = go.Scatter(x=x, y=y, mode='markers',
                    marker = dict(
                                color='RadColor',
                                symbol='RocknRoll',
                                ...
                              )
                    )
```

You can find a complete reference of all of these attributes [on the plot.ly web page here](https://plot.ly/python/reference/).  It is not the most attractive or user friendly reference page, but all the attributes are listed there.

---

Let us alter the color and size of the raw data scatter plot in our graph from the previous exercise.

```python

# define the traces in directly the list
data = [
    # our scatter trace
    go.Scatter(x=x, y=y2, mode='markers', name='Raw Data',
    
        # marker takes a dictionary of more attributes
        marker=dict(   # open dictionary function
            color='LightSteelBlue', # colors can be defined in a number of ways, here, with HTML names
            size=22       # size in pixels
        )  # close ditionary function
    ),     # close graph_obj.Scatter function
    
    
    # curve fit traces ... not being altered here
    go.Scatter(x=x, y=ylin, mode='line', name='Linear Fit'),
    go.Scatter(x=x, y=yquad, mode='line', name='Quadratic Fit')
]

# plot the traces
iplot(data)
```

<!--sec data-title="New Markers" data-id="eg" data-show=true data-collapse=false ces-->

<iframe scrolling="no" style="border:none;" frameborder='0' src="https://plot.ly/~research.bazaar/40.embed" height="450" width="100%"></iframe>

<!--endsec-->

# Colors

There are three ways to define colours in plotly, listed here in increasing order of difficulty to use.  The first and second ways are recommended.  The third way is if you want to show off hexadecimal. 

* Use the [HTML Color Names](http://www.w3schools.com/colors/colors_names.asp).  A handy list of predefined colors with easy to remember names, such as <span style="color:LightSteelBlue">LightSteelBlue</span>, used above, or <span style="color:Teal">Teal</span> or <span style="color:SlateBlue">SlateBlue</span>.


* Use **RGB** or **RGBA** values.  These define the amount of **R**ed, **G**reen and **B**lue in the color.  The values range from ```0``` to ```255```.  If **RGBA** values are used, the **A** stands for **A**lpha, and ranges from ```0``` to ```1```.  High values mean the color is opaque (not see-through); low values mean the color is transparent (see-through).
  * In plotly, use rgb or rgba values as follows:
     
     ```python
     color = 'rgba(190, 45, 110, 0.75)'  # red, green, blue, alpha - shoud be purpleish
     ```
     

* Use hex values.  These are like rgb values in that you provide the amount of red, green and blue.  But, instead of values from 0 to 255, you use hexadecimal numbers.  In hexadecimal, 0 to 255 becomes 00 to FF.  If you aren't familiar with hexadecimal, and don't especially want to be, just stick with rgb.  If you would like to use hexadecimal, the rgb color above would be coded as follows:
    ```python
    color = '#be2d6e'
    ```
It is more efficient but also more difficult to use.

<br>
## Using color picking tools.

Using a visual tool that provides the necessary color code for you is the easiest and best way to use colors effectively.  

Recommendations:

* [HTML Color Picker](http://www.w3schools.com/colors/colors_picker.asp) - provides everything you need to see a particular color, and generate the required ```RGB``` or ```hex``` color code.  **NB** No color blindness assistance.

* [Human Friendly Color Space](http://www.husl-colors.org/) - Similar to the Color Picker above, but works hard to keep all colors equally bright.  This makes nice colors, and allows color blindness to be accommodated somewhat.

* [Color Brewer](http://colorbrewer2.org/) - Produces color scales, all mostly made up of nice colors, with support for accommodating color blindness.  

<br>

---

# Exercise 1
1. Alter the color and size of the markers in your plot from last exercise.
2. Use the reference page to alter the symbol and opacity of the same trace.

<br>

---

# Styling markers 2 - boundary lines

Markers come default without any border or boundary lines.  We can add boundary line styling using the attribute ```line```.  

Like the attribute ```marker```, ```line``` takes its own dictionary. 

The two key attributes of ```line``` are:

* ```color``` - the color of the line
* ```width``` - the width of the line (in pixels)


As ```line``` takes its own dictionary, we will have a dictionary inside a dictionary.  

For more readability, it often helps to define the styling in a separate variable outside of the trace definition.

---

```python

# Define our boundary line attributes for the raw_data trace
raw_line = dict(
            color='Black',   # using an HTML named color
            width=1.5
        )

# Define the marker attributes, this time in a separate variable
raw_mark = dict(
            color='White',    # Changed marker color to look cleaner with a boundary
            size=22,
            symbol='circle',
            opacity=0.4,      # Brought down the opacity and boundaries often allow for this
            line = raw_line   # We give the pre-defined dictionary to this attribute.
    )


data = [
    go.Scatter(x=x, y=y2, mode='markers', name='Raw Data',
    
                  # Instead of all the code we had before, just the pre-defined dictionary
                  marker=raw_mark),

    # Still unaltered
    go.Scatter(x=x, y=ylin, mode='line', name='Linear Fit'),
    go.Scatter(x=x, y=yquad, mode='line', name='Quadratic Fit')   
]

iplot(data)
```

<!--sec data-title="Markers with Boundaries" data-id="eg1" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/42.embed" height="450" width="100%"></iframe>

<!--endsec-->

<br>
# Styling lines

Styling lines is just like styling the boundary lines of markers.

When the ```mode``` of a Scatter trace is set to ```line```, then there is not a ```marker``` attribute, but a ```line``` attribute.  Give to this attribute a dictionary, just as we did for ```marker```.  

The main attributes of the ```line``` dictionary are the same as for the boundary lines of markers:

* ```color``` - color of the line
* ```width``` - width of the line
* ```dash``` - whether the line is ```solid```, ```dot``` or ```dash```.  Alternatively, the length of the dashes and gaps between them can be given as a number, in pixels

<br>
## Opacity

For lines, ```opacity``` is not an attribute of the line styling attribute or dictionary.  Trying to do so will give an error.  Rather, ```opacity``` is an attribute of the graph object.  That is, it goes directly into the ```go.Scatter()```.  This is (presumably) because it is an attribute of the whole line, not, as in the case of markers, each circle or marker individually.

**Question** - what happens when you give a marker trace (ie a ```go.Scatter()``` graph object with ```mode='markers'```) an opacity attribute directly rather than within the ```marker``` attribute.  It turns out to be a subtle but perhaps useful difference.

---

** A quick example: **
```python
x = np.linspace(0, 3*np.pi, 100)

data = [
    go.Scatter(x=x, y=np.sin(x), opacity=0.7, 
               line=dict(width=6,  #line styling
                       color='Purple', 
                       dash='solid')),
    
    go.Scatter(x=x, y=np.sin(x-0.5*np.pi), opacity=0.7, 
               line=dict(width=6, 
                       color='Red', 
                       dash='dot')),
    
    go.Scatter(x=x, y=np.sin(x-1*np.pi), opacity=0.7, 
               line=dict(width=6, 
                       color='Orange', 
                       dash='dash')),
    
    go.Scatter(x=x, y=np.sin(x-1.5*np.pi), opacity=0.7, 
               line=dict(width=6, 
                       color='Green', 
                       dash=3))  # the dashes and gaps will each be 3 pxs in length.
]

iplot(data)
```


<!--sec data-title="Line Styles" data-id="eg2" data-show=true data-collapse=false ces-->
<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/44.embed" height="450" width="100%"></iframe>

<!--endsec-->

---

# Exercise 2


1. Go back to your curve fit and scatter plot.  Make your two curves wider and more transparent and have two new colors of your choice.
2. Give them some dash patterns


<!--sec data-title="Exercise Example" data-id="ex2" data-show=true data-collapse=false ces-->

**Before**

<iframe width="100%" height="450" frameborder="0" scrolling="no" src="https://plot.ly/~research.bazaar/38.embed"></iframe>

**After**

<iframe scrolling="no" style="border:none;" seamless="seamless" frameborder='0' src="https://plot.ly/~research.bazaar/46.embed" height="450" width="100%"></iframe>

<!--endsec-->

