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





### Create your ERDDAP dataset URL programmatically:

```Python
#Import erddap package into 
from erddapy import ERDDAP

# Create your ERDDAP dataset URL in python: 
server = 'https://erddap.bco-dmo.org/erddap/tabledap'

dataset_id = 'tabledapbcodmo_dataset_712367'

constraints = {
    'time>=': '2017-10-11T00:00:00Z',
    'time<=': '2017-10-18T08:16:57Z',
    'latitude>=': 38.0,
    'latitude<=': 41.0,
    'longitude>=': -72.0,
    'longitude<=': -69.0,
}

depth = 'ctdgv_m_glider_instrument_sci_water_pressure_dbar'
salinity = 'ctdgv_m_glider_instrument_practical_salinity'
temperature = 'ctdgv_m_glider_instrument_sci_water_temp'

variables = [
  depth,
 'latitude',
 'longitude',
  salinity,
  temperature,
 'time',
]
```

```Python
e = ERDDAP(
    server=server,
    dataset_id=dataset_id,
    constraints=constraints,
    variables=variables,
    protocol='tabledap',
    response='mat',
)

print(e.get_download_url())
```



#### RERRDAP: package for R users to work directly with erddap servers

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
