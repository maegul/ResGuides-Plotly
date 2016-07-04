

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


# Structure

## Basic Rules
1. Everything in is a container, either a dictionary or a list
2. If a bunch variables are of the same kind and not generally unique, they go together into a **list**.  
  3. Eg - multiple traces for a single plot go into a list
3. If a bunch of variables are unique and/or require a unique identifier, they go together into a **dictionary** with a name or a key.  
  4. Eg - styling variables like ```width``` and ```color``` go into a dictionary.