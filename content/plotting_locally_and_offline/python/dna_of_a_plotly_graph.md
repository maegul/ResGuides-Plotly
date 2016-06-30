# DNA of a plot.ly graph

## The basic idea

The two container type of variables in python, *lists and dictionaries*, can have within them other variables, including more lists and/or dictionaries.  For review, see [the crash course in this material](./dicts_and_lists_crash_course.md).

Plotly is universal.  Your plot will be exactly the same in python, on the web, in javascript or R.  Which it makes it easy to port or move around if necessary.  This is because each plot is defined by a single dictionary.  And this dictionary, which contains further lists and dictionaries, contains all the information needed to make that plot.  The dictionary you were asked to make in the exercises in [the crash course on lists and dicts](./dicts_and_lists_crash_course.md) is very much like the kind used by ploly.

<br>
## Importance

Though there are user friendly python functions that generate plotly graphs for us, sometimes it will be necessary to interact with these figure dictionaries in order to make adjustments.  So, it is useful for us to know our way around them.
This dictionary has two elements, one with the key ```data```, the other with the key ```layout```.  
