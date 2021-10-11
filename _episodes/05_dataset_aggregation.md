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



# Work directly with your dataset in python 

Use the library erddapy to work directly with your dataset in python. 

Alternative in R: rerrdap

Example repo: https://github.com/rsignell-usgs/notebook/blob/master/ERDDAP/ERDDAPY_Intro_OOI.ipynb

```python
# Install the package erddapy 
```



# Aggregating data

Work with data from different servers & different between tabledap and griddap

* download satellite data : explain griddap as basemap
* download an area boundary
* download a bco-dmo dataset
* download an ooi dataset
* put everything on a map.
