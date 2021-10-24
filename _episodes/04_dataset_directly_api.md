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

Erddapy is a package that helps create the ERDDAP URLs. You can create virtually any request like, searching for datasets, acquiring metadata, downloading data, etc.



## Create the URL

Step 1: Instantiate the ERDDAP URL constructor for a server ( erddapy server object). 

```python
#Import erddap package into 
from erddapy import ERDDAP

# Initiate the ERDDAP URL constructor for a server. 
e = ERDDAP(
    server= "https://erddap.bco-dmo.org/erddap/",
    protocol="tabledap",
    response="csv",
)
print ("Initiation done")
```

Step 2: Populate the object with  a dataset id, variables of interest,  and its constraints. We can download the csvp response with the `.to_pandas` method.

```python
e.dataset_id = "bcodmo_dataset_817952"

e.variables = [
    "Cruise",
    "latitude",
    "longitude",
    "Date_Time_PST",
    "Temperature",
    "Salinity",
    "PN",
    "POC",
    "time"
]

e.constraints = {
    "time>=": "2016-01-26T09:45Z",
    "time<=": "2016-12-07T04:40Z",
}

print ("setting variables done")

```

Check the full URL

```python
# Print the URL - check
url = e.get_download_url()
print(url)
```

## Import into Python Pandas

Import the dataset into a pandas dataframe. Import the csvp response with the `.to_pandas` method.

```python
# Convert URL to pandas dataframe
df = e.to_pandas(
    index_col="time (UTC)",
    parse_dates=True,
).dropna()

df.head()
```

Check the dataframe and start using it into your pythin environment

```python
print(df.info())
```

```python
print (df.columns)
```

```python
%matplotlib inline

import matplotlib.pyplot as plt
import matplotlib.dates as mdates

fig, ax = plt.subplots(figsize=(17, 10))
cs = ax.scatter(
    x=df["longitude (degrees_east)"],
    y=df["latitude (degrees_north)"],
    s=15,
    c=df["PN (micromoles N per liter of water (um/L))"],
    marker="o",
    edgecolor="none"
)

cbar = fig.colorbar(cs, orientation="vertical", extend="both")
cbar.ax.set_ylabel("PN (micromoles N per liter of water (um/L))")
ax.set_ylabel("latitude");
ax.set_xlabel("longitude");
```






### RERRDAP: package for R users to work directly with erddap servers

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
* erddapy use with gliders rich signel: 
* notebook community: https://notebook.community/pyoceans/erddapy/notebooks/quick_intro 
* Awesome erddap: global" searches of all erddap servers
* unpacking the matplotlib function: https://towardsdatascience.com/clearing-the-confusion-once-and-for-all-fig-ax-plt-subplots-b122bb7783ca 

