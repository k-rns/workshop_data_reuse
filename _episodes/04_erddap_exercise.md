---
title: "Reuse an ERDDAP served dataset"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

{% include links.md %}



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
