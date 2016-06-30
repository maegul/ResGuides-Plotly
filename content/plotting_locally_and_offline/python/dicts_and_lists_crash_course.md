**Table of Contents**
<!-- toc -->
---

# Dicts and Lists, a crash course

** This is a quick introduction to lists and dictionaries in python.  If you are familiar with these python objects, please, help your fellow participants out, check out the exercises or skip to the next section [DNA of a plot.ly graph](./dna_of_a_plotly_graph.md)**

<br>
## Dictionaries and lists are containers.

The most common kind of variable, or *thing* in python is either a number or string variable.

```python
height = 180.31
name = 'Errol'
age = 30
gender = 'male'
```

As we often have many such variables, there fortunately exist varaibles that are capable of containing other variables within them.  We can call these *containers*.  Dictionaries and lists are *containers*.

<br><br>
## Lists are ordered containers

### Creating Lists
Lists are defined using square brackets: ```myList = []```.  This would be an empty list.

The elements of a list - that is, the other variables *contained* within it - are placed in the list by being between the square brackets and separated by a comma:

```python
myDetails = [height, name, age, gender]
```
<br>
### Ordering
Lists remember the order in which elements are put into them.  So, when I call on the first element in the list, with the index zero, I will get my height, ```180.31```, back.

```python
myDetails[0]
```
returns ...
```
180.31
```

If you were to go through the elements of the list in a for loop, you would go through them in this same order.

```python
for detail in myDetails:
  print(detail)
```
returns ...
```python
180.31
Errol
30
male
```

<br><br>
## Dictionaries are named containers

### Names, not orders

Dictionaries contain other variables just like lists.  But they don't care about or keep track of the order in which they are added.

Instead, each variable added to a dictionary must have a unique name, known as a ```key```.  That variable is then retrievable by using the name or ```key``` given to it.  It is *not* retrievable by the order in which it was put into the dictionary.

<br>
### Creating a dictionary

Dictionaries are defined by using curly brackets: ```myDict = {}```.

The elements of a dictionary are given a ```key```, that is a string, such as ```'height'```, which is followed by a colon and then the variable that will be this particular element.  Each element is separated by a comma as with lists.

So, the dictionary equivalent of the ```myDetails``` list above would be made as follows:

```python
myDetailsDict = {'height':180.31, 'name':'Errol', 'age':30, 'gender':'male'}
```
<br>
### A more user friendly way

**However**, making each ```key``` a string, and typing all of the quotation marks, can be cumbersome.  An **alternative** that will be used in this course is to use the function ```dict()```, which helps in making the creation of dictionaries easier.

When using the function ```dict()```, the ```keys``` don't need to be strings, you can simply type in what you want the key to be and the function will convert it to a string automatically.  Also, instead of using a colon, the equals sign is used.

```python
myDetailsDict = dict(height=180.31, name='Errol', age=30, gender='male')
```

Both methods create the same thing.  Generally though, using ```dict()``` is easier to identify amongst a block of code. 

<br>
### Accessing elements of a dictionary

Much like an element of a list is accessed by placing its position in square brackets after the name of the list (eg ```myList[0]```), a dictionary element is placed by placing not its position but its ```key``` in the square brackets:
```python
myDetailsDict['name']
```
*returns ...*
```
'Errol'
```
<br><br>
### Looping Dictionaries

#### Introduction
Dictionaries are not ordered.  And so looping through all of the elements of a dictionary is not usually the reason we use them, at least in dealing with plotly.  

Usually, you will manipulate particular elements of a dictionary according to what its ```key``` is.  

Nonetheless, looping can be done and can be useful or powerful.

Because each element in a dictionary is made up of two 'bits' — a ```key``` and the variable we've attached to it, there are more options for the way in which you loop through the dictionary.

<br>
#### Setting up a Dictionary for loops
Either way, though, the way you loop through a dictionary is by creating a *list* of all of the elements of the dictionary.

Soooo ... if you wanted to get all the keys of the dictionary, with out their corresponding variables, you would do the following:

```python
myDetailsDict.keys()
```
*returns ...*
```python
['gender', 'age', 'name', 'height']
```

To get all of the elements into a list, where the keys and their corresponding variables are paired together ...

```python
myDetailsDict.items()
```
*returns ...*
```python
[('gender', 'male'), ('age', 30), ('name', 'Errol'), ('height', 180.31)]
```
<br>
#### Using a Dictionary in a loop

Using conditional statements about the nature or content of a key or its corresponding variable, we can start to intelligently manipulate our dictionary.

<!--sec data-title="Demo: Looping Dicts" data-id="section0" data-show=true data-collapse=true ces-->

Let's say that we want to get out of our dictionary only the variables that are strings.  We would use the ```type()``` function, built into python, which returns what type of variable a variable is.  For a string, this is ```str```.

```python
type('hello world')
```
*returns ...*
```python
str
```

---


We can use this to filter out the elements of the dictionary that are strings.

```python
# this will cycle through each key, encoded as 'k'
for k in myDetailsDict.keys(): 
    # check if variable is a string
    if type(myDetailsDict[k]) == str: 
        # if it's a string, print!
        print myDetailsDict[k] 

```
*returns ...*

```python
male
Errol
```


---

Or, because python is awesome with strings, we could get out every variable that has a key that ends in 'e'.

We can do this by using the fact that strings in python are ordered and behave like lists when given indices in square brackets.  Also very useful, is that negative indices start at the end, not the beginning.

```python
text = 'python'
print([text[-1], text[-2], text[-3], text[-4], text[-5], text[-6]])
```
*returns ...*
```python
['n', 'o', 'h', 't', 'y', 'p']
```
Soooo ... modifying our loop from above:

```python
# this will cycle through each key, encoded as 'k'
for k in myDetailsDict.keys(): 
    # check if last letter of key is 'e'
    if k[-1] == 'e': 
        # if the key ends in 'e', print the key and its variable
        print k, myDetailsDict[k] 
```
*returns ...*
```python
age 30
name Errol
```

<!--endsec-->

---
<br><br>
## What can containers contain

Containers, that is both lists and dictionaries, as you've seen from the examples above, can contain strings and numbers.

Very usefully, both lists and dictionaries can contain any kind of variable, **including other containers**.  **Containers can be nested in other containers**.

---

<!--sec data-title="Demo: Lists in lists" data-id="listnests" data-show=true data-collapse=true ces-->
A list can contain have lists as its elements:

```python
data = [ # opens the main list
  [1, 2, 3, 4, 5], # one to five
  [1, 4, 9, 16, 5] # the squares of one to five

] # closes the main list
```

Indexing for the second element will return the second list ...
```python
print(data[1])
```
*returns ...*
```python
[1, 4, 9, 16, 5]
```
<!--endsec-->
---
<!--sec data-title="Demo: Lists in Dictionaries" data-id="nestdicts" data-show=true data-collapse=true ces-->
Dictionaries can have lists too.  Generally, and especially with plot.ly, this is what is very useful about dictionaries: the ability to bundle up different sets of data into a single object, the dictionary, with each bit of the data having an informative and unique name.

```python
dataSet = dict(   # opens the dict function
  # names of the team members
  names = ['Errol', 'The Queen', 'Dan', 'Alistair', 'Nikki'],  
  # ages of the team members
  ages = [30, 143, 18, 63, 12]    
)  # closes the dict function
```

... now we can string the data set however we want to ...

```python
# print appropriate headings for the data we're about to spit out
print( 'Name, Age')

# we have five team members (this can be calculated as: len(dataSet['names']))
for i in range(5):
  # for each team member, pull out the name from 'names' and the age from 'ages'
  # notice how the use of keys makes it more obvious what's going on in the code
  print( dataSet['names'][i], dataSet['ages'][i] )
```
*returns ...*
```python
Name, Age
('Errol', 30)
('The Queen', 143)
('Dan', 18)
('Alistair', 63)
('Nikki', 12)
```
<!--endsec-->


---

<!--sec data-title="Exercises" data-id="ex" data-show=true data-collapse=false ces-->
# Exercises


1. Make a list called ```x``` that contains a set of numbers of your own making
  * Make a similar list called ```y```.
2. Make a dictionary containing both of the above lists, with the names/keys ```xdata``` and ```ydata```.
3. Presume that the ```xdata``` and ```ydata``` are paired, such that the first element of each form a pair, and the second element of each form another pair; ie ```[[x1,y1], [x2, y2], ...]```.  Now print out all of these pairs.
4. Now add another element to your dictionary.  This element should be a string that gives your dictionary a title.  Give it the name/key 'title'.
5. Come up with new ```x``` and ```y``` lists.  Now replace the ```xdata``` and ```ydata``` elements of your dictionary with these new lists.

<!--endsec-->


