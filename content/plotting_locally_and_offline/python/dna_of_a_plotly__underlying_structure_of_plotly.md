# DNA of plot.ly — underlying structure of a plot.ly graph

## Introduction
Behind every plot.ly graph, there is a comprehensive description of every feature of that graph, a "**DNA**" so to speak.  This was addressed briefly in *Fundamental Workings* in the [Python Introduction](./intro.md). 

One of the major strengths of plot.ly is that this "**DNA**" is the same whether you are using plot.ly online, or with matlab, R or javascript.



---


Here, we will —
1. Learn/Refresh ourselves on lists and dictionaries in python.  Plot.ly's DNA is made up of both of these
2. Learn the structure of plot.ly's DNA.
3. Make a plot entirely by writing a complete description, or "genome" for that plot.



---

## Dicts and Lists

** This is a quick introduction to lists and dictionaries in python.  If you are familiar with these python objects, you may skip to the next section**

### Dictionaries and lists are containers.

The most common kind of variable, or *thing* in python is either a number or string variable.

```python
height = 180.31
name = 'Errol'
age = 30
gender = 'male'
```

As we often have many such variables, there fortunately exist varaibles that are capable of containing other variables within them.  We can call these *containers*.  Dictionaries and lists are *containers*.

### Lists — ordered containers

#### Creating Lists
Lists are defined using square brackets: ```myList = []```.  This would be an empty list.

The elements of a list - that is, the other variables *contained* within it - are placed in the list by being between the square brackets and separated by a comma:

```python
myDetails = [height, name, age, gender]
```

#### Ordering
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

### Dictionaries - named containers

#### Names, not orders

Dictionaries contain other variables just like lists.  But they don't care about or keep track of the order in which they are added.

Instead, each variable added to a dictionary must have a unique name, known as a ```key```.  That variable is then retrievable by using the name or ```key``` given to it.  It is *not* retrievable by the order in which it was put into the dictionary.


#### Creating a dictionary

Dictionaries are defined by using curly brackets: ```myDict = {}```.

The elements of a dictionary are given a ```key```, that is a string, such as ```'height'```, which is followed by a colon and then the variable that will be this particular element.  Each element is separated by a comma as with lists.

So, the dictionary equivalent of the ```myDetails``` list above would be made as follows:

```python
myDetailsDict = {'height':180.31, 'name':'Errol', 'age':30, 'gender':'male'}
```

#### A more user-friendly way

**However**, making each ```key``` a string, and typing all of the quotation marks, can be cumbersome.  An **alternative** that will be used in this course is to use the function ```dict()```, which helps in making the creation of dictionaries easier.

When using the function ```dict()```, the ```keys``` don't need to be strings, you can simply type in what you want the key to be and the function will convert it to a string automatically.  Also, instead of using a colon, the equals sign is used.

```python
myDetailsDict = dict(height=180.31, name='Errol', age=30, gender='male')
```

Both methods create the same thing.  Generally though, using ```dict()``` is easier to identify amongst a block of code. 

#### Accessing elements of a dictionary

Much like an element of a list is accessed by placing its position in square brackets after the name of the list (eg ```myList[0]```), a dictionary element is placed by placing not its position but its ```key``` in the square brackets:
```python
myDetailsDict['name']
```
*returns ...*
```
'Errol'
```

#### Looping

Dictionaries are not ordered.  And so looping through all of the elements of a dictionary is not usually the reason we use them, at least in dealing with plotly.  

Usually, you will manipulate particular elements of a dictionary according to what its ```key``` is.  

Nonetheless, looping can be done and can be useful or powerful.

Because each element in a dictionary is made up of two 'bits' — a ```key``` and the variable we've attached to it, there are more options for the way in which you loop through the dictionary.

Either way, though, the way you loop through a dictionary is by creating a *list* of all of the elements of the dictionary.

Soooo ... if you wanted to get all the keys of the dictionary, with out their corresponding variables, you would do the following:




