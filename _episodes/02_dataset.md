---
title: "From the ERDDAP data server to your Python environment"
teaching: 20
exercises: 30
questions:
- "How do I import an ERDDAP dataset into Python?"
- "How do I interact with the dataset in Python"
objectives:
- "Importing data from an ERDDAP server into your Python environment "
- "Interact with data"
keypoints:
- "There are keypackages necessary to import data from ERDDAP into Python: pandas, urllib"
- "Data can be downloaded locally or be interacted with directly using erddapy"
- "You can asses your data package in Python"
---


# Sections To Do

* Opening Jupyter Notebook
* Find a dataset in ERDDAP that you would like to use (using python notebook or erddap self)
* Using ERDDAP with R resources: https://docs.ropensci.org/rerddap/articles/Using_rerddap.html  using the package rerrdap. 
* Missing: finding a dataset of interest? Maybe later in the topic aggregating data. 
* Packages to install: pandas, urllib, erddapy
* ERDDAP metadata
* Searching erddap

# The ERDDAP REST API Services

We'll import data in the notebook

Requesting data using a URL. 

**Tabledap request URLs must be in the form** 
https://coastwatch.pfeg.noaa.gov/erddap/tabledap/*[datasetID](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#datasetID)*.*[fileType](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType)*{?*[query](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#query)*}

**Tabledap request URLs must be in the form** 
https://coastwatch.pfeg.noaa.gov/erddap/tabledap/*[datasetID](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#datasetID)*.*[fileType](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType)*{?*[query](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#query)*} 
For example, 
https://coastwatch.pfeg.noaa.gov/erddap/tabledap/pmelTaoDySst.htmlTable?longitude,latitude,time,station,wmo_platform_code,T_25&time%3E=2015-05-23T12:00:00Z&time%3C=2015-05-31T12:00:00Z 
Thus, the query is often a comma-separated list of desired variable names, followed by a collection of  constraints (e.g., *variable*<*value*),  each preceded by '&' (which is interpreted as "AND").

**Details:**

- Requests must not have any internal spaces.

- Requests are case sensitive.

- {} is notation to denote an optional part of the request.  
  
- [**datasetID**](http://www.neracoos.org/erddap/tabledap/documentation.html#datasetID) identifies the name that ERDDAP  assigned to the source web site and dataset  (for example, pmelTaoDySst). You can see a list of    [datasetID options available via tabledap](http://www.neracoos.org/erddap/tabledap/index.html).  
  
- **fileType**

   specifies the type of table data file that you   want to download (for example, 

  .htmlTable

  ).  The actual extension of the resulting file may be slightly different than the fileType (for example,  .htmlTable returns an .html file).  

  Which fileType should I use?  
  It's entirely up to you. In general, pick the fileType which meets your needs and is easiest to use. You will  use different fileTypes in different situations, e.g., viewing a graph in a browser (.png) vs. viewing the data  in a browser (.htmlTable) vs. downloading a data file (e.g., .nc or .csv) vs. working with some software tool  (e.g., .nc or .odv). If you are going to download lots of large files, you might also want to give some weight  to fileTypes that are more compact and so can be downloaded faster.  

  The fileType options for downloading tabular data are:  





BCO-DMO example dataset: https://www.bco-dmo.org/dataset/712367 

Just generate the URL: 

https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_712367.htmlTable?tank%2CpH%2CTemp%2Cgenotype%2CJuly_mass%2CAugust_mass%2CSeptember_mass

# Open Jupyter notebook 

Make sure that you open Jupyter notebook at the same location you want your data to reside.



STEP 1. Start Jupyter Notebook

Anaconda prompt -> Direct to location -> Start Jupyter Notebook 

![image-20211008061129812](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211008061129812.png)



STEP 2: Open new notebook in the location

![image-20211008061300970](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211008061300970.png)

Reminder [Python Notebook Basics](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

### Edit mode

Edit mode is indicated by a green cell border and a prompt showing in the editor area:

![Jupyter cell with green border](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/images/edit_mode.png)

When a cell is in edit mode, you can type into the cell, like a normal text editor.

Enter edit mode by pressing `Enter` or using the mouse to click on a cell's editor area.

### Command mode

Command mode is indicated by a grey cell border with a blue left margin:

![Jupyter cell with blue & grey border](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/images/command_mode.png)

The most important keyboard shortcuts are `Enter`, which enters edit mode, and `Esc`, which enters command mode.

In edit mode, most of the keyboard is dedicated to typing into the  cell's editor. Thus, in edit mode there are relatively few shortcuts.   In command mode, the entire keyboard is available for shortcuts, so  there are many more.  The `Help`->`Keyboard Shortcuts` dialog lists the available shortcuts.

We recommend learning the command mode shortcuts in the following rough order:

1. Basic navigation: `enter`, `shift-enter`, `up/k`, `down/j`
2. Saving the notebook: `s`
3. Change Cell types: `y`, `m`, `1-6`, `t`
4. Cell creation: `a`, `b`
5. Cell editing: `x`, `c`, `v`, `d`, `z`
6. Kernel operations: `i`, `0` (press twice)

# Downloading a dataset of interest

Download your dataset to your local machine in the file type you need.

Example repo: https://coastwatch.gitbook.io/satellite-course/tutorials/python-tutorial/1.-how-to-work-with-satellite-data-in-python 



```python
# Download the data locally
# Choose the File type of choice - we'll work with tables in .csv
import urllib.request 
https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_712367.csvp?tank%2CpH%2CTemp%2Cgenotype%2CJuly_mass%2CAugust_mass%2CSeptember_mass

# Enter the path to save the .csv file to    
urllib.request.urlretrieve(url, "path to save")
```

```Python
# Import the downloaded .csv data into jupyter notebooks with the package Pandas
import pandas as pd

```

```python
# Examine data structure		
```





# Subsetting datasets

Subset your data of interest by adjusting the URL. 

```python
```



# Make a map

```Python
```





# Work directly with your dataset in python 

Use the library erddapy to work directly with your dataset in python. 

Alternative in R: rerrdap

Example repo: https://github.com/rsignell-usgs/notebook/blob/master/ERDDAP/ERDDAPY_Intro_OOI.ipynb

```python
# Install the package erddapy 
```











# Aggregating data

