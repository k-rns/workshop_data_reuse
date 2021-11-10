---
title: "Online data to your Python environment"
teaching: 25
exercises: 0
questions:
- "How do I import an ERDDAP dataset into Python?"
- "How do I interact with the dataset in Python"
objectives:
- "Importing data from an ERDDAP server into your Python environment "
- "Interact with data"
keypoints:
- "There are keypackages necessary to import data from ERDDAP into Python: pandas"
- "Data can be downloaded locally or be interacted with directly using erddapy"
- "You can asses your data package in Python"
---

# ERDDAPY library

In the previous lesson, we downloaded our dataset file to our local machine. Now we will not download it to your local machine, but use in in your python environment directly. 

Erddapy is a package that  takes advantage of ERDDAP's RESTful web services and creates the ERDDAP URL for any request, like searching for datasets, acquiring metadata, downloading the data, etc.You can create virtually any request like, searching for datasets, acquiring metadata, downloading data, etc.

[Link]( https://github.com/k-rns/workshop_data_reuse/blob/gh-pages/_episodes/04_dataset_directly.ipynb) to static Jupyter Notebook. Copy/Paste the code blocks into your own Jupyter Notebook

## Searching datasets using erddapy
Step 1: Initiate the ERDDAP URL constructor for a server ( erddapy server object).

```python
#searching datasets based on words
from erddapy import ERDDAP
e = ERDDAP(
    server="https://erddap.bco-dmo.org/erddap", 
    protocol="tabledap", 
    response="csv")
```

Search with keywords:

```python
import pandas as pd
url = e.get_search_url(search_for="Temperature OC1603B", response="csv")

print (url)
pd.read_csv(url)["Dataset ID"]
```

Inspect the metadata of dataset with id bcodmo_dataset_817952:

```python
#find the variables
info_url = e.get_info_url(dataset_id="bcodmo_dataset_817952")
pd.read_csv(info_url)

pd.set_option('display.max_rows', None) #make sure that jupyter notebook shows all rows
dataframe = pd.read_csv(info_url)
print (dataframe)
```

```python
#get the unique variable names with pandas
dataframe["Variable Name"].unique()

```

Exercise:  

- What are the units of POC?

- Who is the Principal Investigator on this dataset?

- What is the start and end time of this dataset?

  

Exercise: What are the unique variables for "bcodmo_dataset_807119"?

\#find the variables info_url = e.get_info_url(dataset_id="bcodmo_dataset_807119") pd.read_csv(info_url)

pd.set_option('display.max_rows', None) #make sure that jupyter notebook shows all rows dataframe = pd.read_csv(info_url) dataframe

\#get the unique variable names with pandas dataframe["Variable Name"].unique()

## Import BCO-DMO temperature dataset - Oregon Coast

### Part 1: Create the URL

From the dataset above, we are going to import the variables  longitude, latitude, time and Temperature. The time constraints will be  netween January 13th and January 16th. 

Step 1: Initiate the ERDDAP URL constructor for a server ( erddapy server object).

```python
#Import erddap package into 
from erddapy import ERDDAP

e = ERDDAP(
    server= "https://erddap.bco-dmo.org/erddap/",
    protocol="tabledap",
    response="csv",
)
```

Step 2: Populate the object with a dataset id, variables of interest,  and its constraints. We can download the csvp response with the  .to_pandas method.

```
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
```

Check the URL

```
# Print the URL - check
url = e.get_download_url()
print(url)
```

### Part 2: Import your dataset into pandas

We can import the csv response using the erddapy the .to_pandas method.

```python
# Convert URL to pandas dataframe
df_bcodmo = e.to_pandas(  
    parse_dates=True,
).dropna()
```

Check out your dataset in pandas

```python
# print the dataframe to check what data is in there specifically. 
df_bcodmo.head()
```

```python
# print the column names
print (df_bcodmo.columns)
```

There is a weird name in the title, rename the column to correct this

```python
df_bcodmo.rename(columns={df_bcodmo.columns.values[3]: 'Temperature (degrees Celsius)'}, inplace=True)
print (df_bcodmo.columns)
```

Subset the tabular data further in pandas based on the time
Step 1: convert the time to a datetime object to take out the time

```python
import pandas as pd
# convert to datetime object to be able to work with it in pandas
print (df_bcodmo.dtypes)

df_bcodmo["time (UTC)"] = pd.to_datetime (df_bcodmo["time (UTC)"], format = "%Y-%m-%dT%H:%M:%S")
print (df_bcodmo.dtypes)
```

Only select the rows for January 13th

```python
df_bcodmo_13 =  df_bcodmo[df_bcodmo["time (UTC)"].dt.day == 13]
df_bcodmo_13
```

When you inspect the dataset, you can see that some hours have multiple data points, while others have only 1 data point. Let's average the dataset  over every hour using the groupby function

```python
df_bcodmo_13_average = df_bcodmo_13.groupby(df_bcodmo["time (UTC)"].dt.hour)[['Temperature (degrees Celsius)','longitude (degrees_east)','latitude (degrees_north)']].mean().reset_index()
df_bcodmo_13_average
```

Plot your averaged dataset in pandas

```python
df_bcodmo_13_average.plot (
    x='longitude (degrees_east)',
    y='latitude (degrees_north)', 
    kind = 'scatter',
    c='Temperature (degrees Celsius)',
    colormap="YlOrRd")
```

Exercise:  Create the URL for this dataset with the variable POC instead of temperature

\#Import erddap package into  from erddapy import ERDDAP

e = ERDDAP(    server= "https://erddap.bco-dmo.org/erddap/",    protocol="tabledap",    response="csv", )

e.dataset_id = "bcodmo_dataset_817952" e.variables = [    "longitude",    "latitude",    "time",    "POC" ] e.constraints = {    "time>=": "2017-01-13T00:00:00Z",    "time<=": "2017-01-16T23:59:59Z",}

\#Print the URL - check url = e.get_download_url() print(url



#### NOTE:  RERRDAP: package for R users to work directly with erddap servers

Information an using erddap: https://docs.ropensci.org/rerddap/articles/Using_rerddap.html  

Example from the following page: [OOI Glider Data](https://docs.ropensci.org/rerddap/articles/Using_rerddap.html#ioos-glider-data) (accessed October 11, 2021):

*The mission of the IOOS Glider DAC is to provide glider operators with a simple process for submitting glider data sets to a centralized  location, enabling the data to be visualized, analyzed, widely  distributed via existing web services and the Global Telecommunications  System (GTS) and archived at the National Centers for Environmental  Information (NCEI). The IOOS Glider Dac is accessible through `rerddap` (http://data.ioos.us/gliders/erddap/). Extracting and plotting salinity from part of the path of one glider deployed by the Scripps Institution of Oceanography:*

```R
urlBase <- "https://data.ioos.us/gliders/erddap/"
gliderInfo <- info("sp064-20161214T1913",  url = urlBase)
glider <- tabledap(gliderInfo, fields = c("longitude", "latitude", "depth", "salinity"), 'time>=2016-12-14', 'time<=2016-12-23', url = urlBase)
glider$longitude <- as.numeric(glider$longitude)
glider$latitude <- as.numeric(glider$latitude)
glider$depth <- as.numeric(glider$depth)
```

``` R
require("plot3D")
scatter3D(x = glider$longitude , y = glider$latitude , z = -glider$depth, colvar = glider$salinity, col = colors$salinity, phi = 40, theta = 25, bty = "g", type = "p",
           ticktype = "detailed", pch = 10, clim = c(33.2,34.31), clab = 'Salinity',
           xlab = "longitude", ylab = "latitude", zlab = "depth",
           cex = c(0.5, 1, 1.5))
```

![outcome_R_example](https://docs.ropensci.org/rerddap/man/figures/glider-1.png)

## Resources: 

* erddapy quick intro: https://ioos.github.io/erddapy/00-quick_intro-output.html
* erddapy use with gliders rich signel: https://notebook.community/rsignell-usgs/notebook/ERDDAP/ERDDAP_advanced_search_test
* notebook community: https://notebook.community/pyoceans/erddapy/notebooks/quick_intro 
* Awesome erddap: global" searches of all erddap servers
* unpacking the matplotlib function: https://towardsdatascience.com/clearing-the-confusion-once-and-for-all-fig-ax-plt-subplots-b122bb7783ca 
* ERDDAP class API: https://ioos.github.io/erddapy/erddapy.html

