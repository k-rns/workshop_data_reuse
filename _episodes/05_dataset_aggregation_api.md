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

[Link](https://github.com/k-rns/workshop_data_reuse/blob/gh-pages/_episodes/05_dataset_aggregation.ipynb) to static Jupyter Notebook. Copy/Paste the code blocks into your own Jupyter Notebook

## OOI temperature dataset - Oregon Coast 2017

Import an OOI dataset. Background on the dataset we are importing [here](https://ooinet.oceanobservatories.org/data_access/?search=CE01ISSM-RID16-03-CTDBPC000) and [here](https://sensors.ioos.us/#metadata/103705/station) :

* Coastal endurance Array
* Platform: Oregon Inshore Surface Monitoring
* Instrument CTD. 

```python
#Import erddap package
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
df_ooi_2017 = e.to_pandas( 
    parse_dates=True,
).dropna()

df_ooi_2017.head()
df_ooi_2017
```

Plot the data 

```python
df_ooi_2017.plot (x='longitude (degrees_east)', 
                    y='latitude (degrees_north)', 
                    kind = 'scatter',
                    c='sea_water_temperature (degree_Celsius)', 
                    colormap="YlOrRd")
```

## OOI temperature dataset 2018 - Oregon Coast

```python
#Import erddap package into 
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
    "time>=": "2018-01-13T00:00:00Z",
    "time<=": "2018-01-13T23:59:59Z",}
print ('done')
```

```python
# Print the URL - check
url = e.get_download_url()
print(url)
```

```python
# Convert URL to pandas dataframe
df_ooi_2018 = e.to_pandas( 
    parse_dates=True,
).dropna()

df_ooi_2018.head()
print (df_ooi_2018)

```

# Combining the datasets

averaging the datasets

Convert the objects to datetime objects

```python
import pandas as pd
print (df_ooi_2017.dtypes)
df_ooi_2017["time (UTC)"] = pd.to_datetime (df_ooi_2017["time (UTC)"], format = "%Y-%m-%dT%H:%M:%S")

print (df_ooi_2017.dtypes)
```



```python
import pandas as pd
print (df_ooi_2018.dtypes)
df_ooi_2018["time (UTC)"] = pd.to_datetime (df_ooi_2018["time (UTC)"], format = "%Y-%m-%dT%H:%M:%S")

print (df_ooi_2017.dtypes)
```

```python
df_ooi_2017_average = df_ooi_2017.groupby(df_ooi_2017["time (UTC)"].dt.hour)['sea_water_temperature (degree_Celsius)'].mean().reset_index()
print (df_ooi_2017_average)
```

```python
df_ooi_2018_average = df_ooi_2018.groupby(df_ooi_2018["time (UTC)"].dt.hour)['sea_water_temperature (degree_Celsius)'].mean().reset_index()
print (df_ooi_2018_average)
```



```python
%matplotlib inline

import matplotlib.pyplot as plt

plt.figure(figsize=(12,5)) 
plt.plot(df_ooi_2017_average["time (UTC)"],df_ooi_2017_average["sea_water_temperature (degree_Celsius)"],label='2017',c='red',marker='.',linestyle='-') 
plt.plot(df_ooi_2018_average["time (UTC)"],df_ooi_2018_average["sea_water_temperature (degree_Celsius)"],label='2018',c='blue',marker='.',linestyle='-') 
plt.ylabel('degrees celsius')
plt.title("January 13th")
plt.legend()
plt.yticks(rotation=90)


#fig, (ax1, ax2) = plt.subplots(2)
#fig.suptitle('Vertically stacked subplots')
#ax1.plot(df_bcodmo["time (UTC)"],df_bcodmo['temperature'],label='bcodmo',c='red',marker='.',linestyle='-')
#ax2.plot(df_ooi["time (UTC)"],df_ooi["sea_water_temperature (degree_Celsius)"],label='OOI',c='blue',marker='.',linestyle='-')
#ax1.set(ylabel='degrees celsius')
#ax2.set(ylabel='degrees celsius')
```




