# Setup

## Installation

* If you haven't already, install python and all the useful libraries you will need from [Anaconda](https://www.continuum.io/downloads).
  * Either version 2.7 or 3.4 are fine for this course.
* Then, from your command line, run:
```
> pip install plotly 
```
* Check your installation:
  * From your commandline, run python:
```
> python
```
  * Then, into your python console, to import plotly and check the version, type the following commands:
```
>>> import plotly
>>> plotly.__version__
```

You should have a version that is 1.12.0 or higher.



## What to Import
The plot.ly python library allows for both completely offline and private work as well as integration with an online plot.ly account.

For this course, the offline mode will be used.  

Apart from the offline v online distinction, there are no other differences between the modes; everything in this course is interchangeable.

Later in the course, on-line integration will be dealt with.


### Offline usage

* The main library
```python
import plotly
```
* The off-line plotting tools, ```iplot``` for the Jupyter Notebook and ```plot``` for ordinary usage.
```python
from plotly.offline import iplot, plot
```
* A function to allow embedding plots into notebooks, 
```python
from plotly.offline import init_notebook_mode
init_notebook_mode()
```

### Online integration

* The main library
```python
import plotly
```
* The on-line plotting tools, ```iplot``` for the Jupyter Notebook and ```plot``` for ordinary usage.  Notice that they come not from the offline library but the plotly library.
```python
from plotly.plotly import iplot, plot
```
* A function for linking to your on line account, 
```python
import plotly.tools as tls
tls.set_credentials_file(username='My_User_Name', api_key='My_API_Key')
```

You will find your api_key in the settings page of your on-line account.  [This link should take you there](https://plot.ly/settings/api).  Otherwise, when logged in, you will find it accessible from the top left of your screen.