# What you can do after this course
* **Online** Plotting
  * Use an online plotting tool.
  * That generates attractive and interactive plots.
  * As easily as with MS Excell or equivalent.
  * Host your plots (and their underlying data) on the web.
* Easy interactive **offline** plotting
  * Generate the same attractive and interactive plots offline using either *Matlab*, *Python*, *R* or *Javascript*.
  * Easily host your offline generated plots online
* Learn and use **fundamental website building tools** to -
  * Enhance the interactivity of your plots.
  * Host them on your own websites or blogs.



# What is Plot.ly
##Plotly is web based  

-> example gif of using it

It is a plotting library that is written to work on the web (and inside web browsers).  Using it is much like using any other plotting tool, such as MS Excel or the standard plotting tools in *Matlab*, *Python* or *R*.  The main difference is that Plotly is web based.  The plot that is generated is built to work on the web, using *javascript*, the programming language of the web.  As you would have noticed, web sites are almost always interactive in some way - the web is designed to be interactive - and so plotting using a web based tool gives all of the possibilities of the interactivity and dynamics you have seen on the internet.

##Plotly is universal
Plotly is designed so that every plot can be described with a simple text file that defines all of the data and characteristics of the plot.  An example is below.

```JSON
layout:
{
  yaxis:{type:"linear", range:[-1.415939217588103,38.415939217588104]},
  xaxis:{type:"linear",range:[0.695666029318037,6.304333970681963]},
height:532,
width:1040
}
```
*You don't write these descriptions* — plotly does that for you.  But, because it is easy for computers to write these text descriptions, it is easy for other software packages to use plotly too.  Essentially, plotly speaks a universal language.  

This means that you can use plotly with *Matlab*, *Python*, *R*, *javascript* or with their *web editor*.  The essentially functionality of plotly will not be affected by your choice of tool.  The plots will look the same no matter which language you are using.  The way you make the plots will be the same.  And you can easily convert your code for using plotly in one lanugage to another.  **It is the same plotly engine underneath.**

## Plotly is free and open
All of the functions and services described above are free.  The source code of the plotly library and its implementations in *Matlab*, *Python* and *R* are open and available on GitHub.

Additional advanced features are available through a paid subscription.



# How to use this course

This course is modular.  Each section is independent.  You can pick and choose from them. 

###Section 1 — Plotting Online
Plotly's online plotting tool and hosting service.

###Section 2 - Plotting Offline
Plotly's offline plotting with *Matlab*, *Python* or *R*.

