---
title: "Gridded dataset"
teaching: 20
exercises: 0
questions:
- "How can I work with gridded datasets"
objectives:
- "Downloading satellite data from ERDDAP in netCDF format "
- "Extracting data with Python"
- "Map spatial datasets "

keypoints:
- "There are key packages necessary to import data from ERDDAP into Python: xarray"
- "xarray works similar to Pandas"
- "xarray has a build in plotter for gridded datasets"
---

# Working with gridded data
Gridded data works with a different protocol called griddap. Instead of using the erddapy library. It is easier to import the data in .netcdf using the package xarray and netcdf.

Setting the constraints with this packageg is a bit more straightforward

**griddap request URLs must be in the form** 
https://coastwatch.pfeg.noaa.gov/erddap/griddap/*[datasetID](https://coastwatch.pfeg.noaa.gov/erddap/griddap/documentation.html#datasetID)*.*[fileType](https://coastwatch.pfeg.noaa.gov/erddap/griddap/documentation.html#fileType)*{?*[query](https://coastwatch.pfeg.noaa.gov/erddap/griddap/documentation.html#query)*} 

For example, 
https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplMURSST41.htmlTable?analysed_sst[(2002-06-01T09:00:00Z)][(-89.99):1000:(89.99)][(-179.99):1000:(180.0)] 

The query is often a data variable name (e.g., analysed_sst), followed by [(*start*):*stride*:(*stop*)] (or a shorter variation of that) for each of the variable's dimensions (for example, [time][latitude][longitude]). 

[Link]( https://github.com/k-rns/workshop_data_reuse/blob/gh-pages/_episodes/06_gridded_data.ipynb) to static Jupyter Notebook. Copy/Paste the code blocks into your own Jupyter Notebook

xarray works similarly as the pandas data package. 

```python
import xarray as xr
import netCDF4 as nc
```

Satellite data NASA sea surface temperature : **GHRSST Global 1-km Sea Surface Temperature (G1SST), Global, 0.01 Degree, 2010-2017, Daily** The data contains daily composites of SST with 1 km resolution

Importing the downloaded data in Python.  Now that we've downloaded the data locally, we can import it and extract our variables of interest:

```python
import xarray as xr

server = 'https://coastwatch.pfeg.noaa.gov/erddap'
protocol = 'griddap'
dataset_id = "jplG1SST"
full_URL = '/'.join([server,protocol,dataset_id])
print(full_URL)
da = xr.open_dataset(full_URL)
```

Inspect the dataframe:

```python
print (da)
```

Getting the dataset without subsetting it creates an error -> the data set is too large to be downloaded completely.

```python
sst = da['SST']
sst
```

Create subsets of your netcdf file:

For this exercise, the area we are interested in includes Monterey Bay, CA:

- Latitude range: 44.0N, 48.0N
- Longitude range: -128E, -121E
- Time range 2017-01-13T00:00:00Z to 2017-01-16T23:59:59Z

Xarray supports:

- label-based indexing using .sel
- position-based indexing using .isel

slice() function can take three parameters:

- start (optional) - Starting integer where the slicing of the object starts. Default to None if not provided.
- stop - Integer until which the slicing takes place. The slicing stops at index stop -1 (last element)

```python
import xarray as xr

server = 'https://coastwatch.pfeg.noaa.gov/erddap'
protocol = 'griddap'
dataset_id = "jplG1SST"
full_URL = '/'.join([server,protocol,dataset_id])
print(full_URL)
da = xr.open_dataset(full_URL)


sst = da['SST'].sel(  
                  latitude=slice(44., 48.),  
                  longitude=slice(-128, -121), 
                  time='2017-01-13T00:00:00'
                 )
sst


```

```python
%matplotlib inline
sst.isel(time=0).plot.imshow()
```



