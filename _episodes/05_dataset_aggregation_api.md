---
title: "Aggregating multiple datasets"
teaching: 20
exercises: 25
questions:
- "How can I work with different datasets?"
objectives:
- "Importing data from different ERDDAP servers into your Python environment "
- "Compare different datasets"
- "Map spatial datasets together"
keypoints:
- "There are keypackages necessary to import data from ERDDAP into Python: pandas, urllib"
- "Data can be downloaded locally or be interacted with directly using erddapy"
- "You can asses your data package in Python"
---





# Aggregating data

Work with data from different servers & different between tabledap and griddap

* download satellite data : explain griddap as basemap
* download an area boundary
* download a bco-dmo dataset
* download an ooi dataset
* put everything on a map.







Datasets to aggregate, the variable to use is temperature data. 

Goni - BCO-DMO: https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_817952.graph?longitude%2Clatitude%2CTemperature&time%3E=2017-01-10T00%3A00Z&time%3C=2017-01-17T00%3A00Z&.draw=markers&.marker=5%7C5&.color=0x000000&.colorBar=%7C%7C%7C%7C%7C&.bgColor=0xffccccff

OOI: find data about this mooring:  https://erddap.dataexplorer.oceanobservatories.org/erddap/tabledap/ooi-ce01issm-rid16-03-ctdbpc000.graph?longitude%2Clatitude%2Cz&time%3E=2017-01-10T00%3A00%3A00Z&time%3C=2017-01-10T00%3A00%3A00Z&longitude%3E=-124.563&longitude%3C=-123.563&latitude%3E=44.136&latitude%3C=45.136&.draw=markers&.marker=5%7C5&.color=0xFF00FF&.colorBar=%7C%7C%7C%7C%7C&.bgColor=0xffccccff

Satellite data NASA? sea surface temperature : **GHRSST Global 1-km Sea Surface Temperature (G1SST), Global, 0.01 Degree, 2010-
2017, Daily**

https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplG1SST.graph?SST%5B(2017-09-13T00:00:00Z)%5D%5B(-79.995):(79.995)%5D%5B(-179.995):(179.995)%5D&.draw=surface&.vars=longitude%7Clatitude%7CSST&.colorBar=%7C%7C%7C%7C%7C&.bgColor=0xffccccff

boundaries 





# Exercise

* 1 dataset
* multiple datasets

# ERDDAP Exercise

From this repo: https://github.com/CoastWatch-PolarWatch/EDMW_2021_python_code number 1

Describe the exercise: i.e "In this exercise, you will use Python to download data from ERDDAP using an irregular boundary."

### The exercise demonstrates the following skills:

- Using Python to retrieve information about a dataset from ERDDAP
- Getting boundary data from a local CSV file
- Downloading satellite data from ERDDAP in netCDF format
- Extracting data within an irregular boundary with Python

*The scripts in this exercise are written in Python 3.7.*



About the dataset used in this exercise

Install the correct python modules



## What to do with the ERDDAP file

1. Access data and metadata from erddap / get information about a dataset from erddap

   1. We will use the xarray `open_dataset` function to access data and metadata from ERDDAP. 

      Here we describe how to create the url for the `open_dataset` function and demonstrate a function to generate the ERDDAP url.

      Open a pointer to an ERDDAP dataset, using the xarray `open_dataset` function

      > xr.open_dataset('full_url_to_erddap_dataset')

      Where, the `full_url_to_erddap_dataset` is the base url to the ERDDAP you are using and the ERDDAP dataset id. So, for our dataset:

      - base_URL = 'https://coastwatch.pfeg.noaa.gov/erddap/griddap'
      - dataset_id = 'nesdisGeoPolarSSTN5SQNRT'
      - full_URL = 'https://coastwatch.pfeg.noaa.gov/erddap/griddap/nesdisGeoPolarSSTN5SQNRT'

2. Examine the metadata

   1. coordinate variables and dimensions
   2. look at the data variables
   3. Examine Global attributes: global attributes provide information about a dataset as a whole. 

3. Download data from erddap

   1. Subsetting data

4. Visualizing data

