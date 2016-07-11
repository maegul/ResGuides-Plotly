**Table of Contents**
<!-- toc -->
---

# 3D Data - bubbles and heatmaps

* Using data with three dimensions to make heatmaps
* Using similar data to enhance scatter plots to make 'bubble' plots
* Making genuine 3D plots

<!--sec data-title="Summary" data-id="s1" data-show=true data-collapse=false ces-->

<!--endsec-->

<br>


#Introduction

Three dimensional plots are often overused and redundant.  

**But**, data that is richer than having two dimensions; that has some sort of '*third dimension*', that is meaningful and informative, is quite common.  Here we will use two dimensional plots in a way that brings in that third dimension of data in an effective way.


# Heatmaps

## For what kind of data
**Note** - if you're comfortable with two dimensional arrays in python, feel free to move onto the next section.

Heatmaps are for when you have a full table of data.  That is, when you have a data point for every point along both the x and y axes, and that data point is a value along another third axis.

For instance, lets say you have your own wakefulness for every hour for every day.  Your x axis is the day of the week, your y axis the time of the day, and your third dimension of data is how wakeful you are, on a scale between zero and one.  Your data would be structured like this ...

|  | Mond | Tue | Wed | Thur | Fri |
| -- | -- | -- | -- | -- | -- |
| Morning |  |  |  |  |  |
| Midday |  |  |  |  |  |
| Afternoon |  |  |  |  |  |


<br>
## Structuring the data for plotly

This table like format above is the way in which plotly like to receive its data.

For python, this means that we want our data to be stored as a list of lists, or, an array of arrays in a 2D numpy array.  The rows of the table is one of the second lists within the first main list.  

Essentially, plotly expects of list of rows.  And this is the way plotly will will plot your data.  The first row/list in your list of lists will be the top most row of the plot, the second list will the second from the top row in the plot etc. 

For instance:

```python
data = [      # opening the first list that contains the other lists
          [1, 0.5, 0.7, ...],  # morning data for each day
          [0.5, 0.3, 0.2, ...], # MIdday data for each day
          [0.6, 0.3, 0.8, ...]  # Afternoon data for each day
]
```

If your data is arranged in the wrong way - let's say you have lists of wakefulness for each day - plotly lets you easily transpose your data.


life+gdp + pop as color

life+gdp+pop in a bubble

life+gdp + pop as color

text for hover over - can have anything

grouping as separate traces