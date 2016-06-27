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
Returns
```
180.31
```