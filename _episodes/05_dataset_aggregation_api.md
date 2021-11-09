---
title: "Aggregating multiple datasets"
teaching: 10
exercises: 30
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

# Aggregating datasets

Exercise: We want to plot surface temperature of different datasets with each other. 

Note; We will be importing datasets from different servers, bear in mind that the granularity (time interval, sensor types) are different and needs to be taken into account when actually comparing these dataset. 

* Location: Location: Oregon Coast. 

* Date range: [2017-01-13 till 2017-01-16], UTC time. 

* Variable: Surface temperature



```python
#Import erddap package into 
from erddapy import ERDDAP
```



## OOI temperature dataset - Oregon Coast

Import an OOI dataset. Background on the dataset we are importing [here](https://ooinet.oceanobservatories.org/data_access/?search=CE01ISSM-RID16-03-CTDBPC000) and [here](https://sensors.ioos.us/#metadata/103705/station) :

* Coastal endurance Array
* Platform: Oregon Inshore Surface Monitoring
* Instrument CTD. 

```python
from erddapy import ERDDAP

# ooi constructor:

e = ERDDAP(
    server= " https://erddap.dataexplorer.oceanobservatories.org/erddap/",
    protocol="tabledap",
    response="csv",
)

e.dataset_id = "ooi-ce01issm-rid16-03-ctdbpc000"
e.variables = [
    "longitude",
    "latitude",
    "time",
    "sea_water_temperature"
]
e.constraints = {
    "time>=": "2017-01-13T00:00:00Z",
    "time<=": "2017-01-16T23:59:59Z",}
```

Check the URL
```python
# Print the URL - check
url = e.get_download_url()
print(url)
```

Import the dataset into the pandas dataframe and check the lay-out
```python
# Convert URL to pandas dataframe
df_ooi = e.to_pandas( 
    parse_dates=True,
).dropna()

df_ooi.head()
```



## BCO-DMO temperature dataset - Oregon Coast


```python
# bco-dmo constructor
url_bcodmo = "https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_817952.graph?longitude%2Clatitude%2CTemperature&time%3E=2017-01-10T00%3A00Z&time%3C=2017-01-17T00%3A00Z&.draw=markers&.marker=5%7C5&.color=0x000000&.colorBar=%7C%7C%7C%7C%7C&.bgColor=0xffccccff" 


e = ERDDAP(
    server= "https://erddap.bco-dmo.org/erddap/",
    protocol="tabledap",
    response="csv",
)

e.dataset_id = "bcodmo_dataset_817952"
e.variables = [
    "longitude",
    "latitude",
    "time",
    "Temperature"
]
e.constraints = {
    "time>=": "2017-01-13T00:00:00Z",
    "time<=": "2017-01-16T23:59:59Z",}


# Print the URL - check
url = e.get_download_url()
print(url)
# Convert URL to pandas dataframe
df_bcodmo = e.to_pandas(
    
    parse_dates=True,
).dropna()

# print the dataframe to check what data is in there specifically. 
df_bcodmo.head()

# index_col="time (UTC)",

print (df_bcodmo.columns)

df_bcodmo.rename(columns={df_bcodmo.columns.values[3]: 'temperature'}, inplace=True)
print (df_bcodmo.columns)

```
Check your dataset in Pandas
```python
# print the dataframe to check what data is in there specifically. 
df_bcodmo.head()

# index_col="time (UTC)",
print (df_bcodmo.columns)
```

Rename the columns to be able to use them in a graph together
```python
df_bcodmo.rename(columns={df_bcodmo.columns.values[3]: 'temperature'}, inplace=True)
print (df_bcodmo.columns)
```



## plotting the data

```python
%matplotlib inline

import matplotlib.pyplot as plt

plt.figure(figsize=(12,5)) 
plt.plot(df_bcodmo["time (UTC)"],df_bcodmo['temperature'],label='bcodmo',c='red',marker='.',linestyle='-') 
plt.plot(df_ooi["time (UTC)"],df_ooi["sea_water_temperature (degree_Celsius)"],label='OOI',c='blue',marker='.',linestyle='-') 
plt.ylabel('degrees celsius')
plt.legend()
# plt.yticks(rotation=90)


fig, (ax1, ax2) = plt.subplots(2)
fig.suptitle('Vertically stacked subplots')
ax1.plot(df_bcodmo["time (UTC)"],df_bcodmo['temperature'],label='bcodmo',c='red',marker='.',linestyle='-')
ax2.plot(df_ooi["time (UTC)"],df_ooi["sea_water_temperature (degree_Celsius)"],label='OOI',c='blue',marker='.',linestyle='-')
ax1.set(ylabel='degrees celsius')
ax2.set(ylabel='degrees celsius')
```



# Working with gridded data:

Example from: https://coastwatch.gitbook.io/satellite-course/tutorials/python-tutorial/1.-how-to-work-with-satellite-data-in-python 

Satellite data NASA? sea surface temperature : **GHRSST Global 1-km Sea Surface Temperature (G1SST), Global, 0.01 Degree, 2010-
2017, Daily**

https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplG1SST.graph?SST%5B(2017-09-13T00:00:00Z)%5D%5B(-79.995):(79.995)%5D%5B(-179.995):(179.995)%5D&.draw=surface&.vars=longitude%7Clatitude%7CSST&.colorBar=%7C%7C%7C%7C%7C&.bgColor=0xffccccff



# Exercise: Aggregating data

Work with data from different servers & different between tabledap and griddap

* download satellite data : explain griddap as basemap
* download an area boundary
* download a bco-dmo dataset
* download an ooi dataset
* put everything on a map.



From this repo: https://github.com/CoastWatch-PolarWatch/EDMW_2021_python_code number 1

Describe the exercise: i.e "In this exercise, you will use Python to download data from ERDDAP using an irregular boundary."

### The exercise demonstrates the following skills:

- Using Python to retrieve information about a dataset from ERDDAP
- Getting boundary data from a local CSV file
- Downloading satellite data from ERDDAP in netCDF format
- Extracting data within an irregular boundary with Python

*The scripts in this exercise are written in Python 3.7.*





