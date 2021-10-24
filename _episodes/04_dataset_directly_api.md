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
- "There are keypackages necessary to import data from ERDDAP into Python: pandas, urllib"
- "Data can be downloaded locally or be interacted with directly using erddapy"
- "You can asses your data package in Python"
---



# ERDDAPY library

In the previous lesson, we downloaded our dataset file to our local machine. Now we will not download it to your local machine, but use in in your python environment directly. 

erddapy is a package that helps



## Create the URL

First we need to instantiate the ERDDAP URL constructor for a server ( erddapy server object). 

```python
#Import erddap package into 
from erddapy import ERDDAP

# Initiate the ERDDAP URL constructor for a server. 
e = ERDDAP(
    server= "https://erddap.bco-dmo.org/erddap/",
    protocol="tabledap",
    response="csv",
)
```



Now we can populate the object a dataset id, variables of interest,  and its constraints ( populate the object with constraints, the variables of interest, and the dataset id.) We can download the csvp response with the `.to_pandas` method.

```python
e.dataset_id = "bcodmo_dataset_815732"

e.variables = [
    "Cruise_ID",
    "latitude",
    "longitude",
    "Date_Time_PST",
    "Temperature",
    "Salinity",
    "Chlorophyll",
    "time"
]

e.constraints = {
    "time>=": "2016-01-26T09:45Z",
    "time<=": "2016-12-07T04:40Z",
}
```

```python
# Print the URL - check
url = e.get_download_url()
print(url)
```

## Import it into a pandas 
```
# Convert URL to pandas dataframe
df = e.to_pandas(
    index_col="time (UTC)",
    parse_dates=True,
).dropna()

df.head()
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

