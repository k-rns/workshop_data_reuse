---
title: "Exploring the ERDDAP data catalog"
teaching: 10
exercises: 0
questions:
- "What is open data?"
- "What is ERDDAP?"
- "Why is ERDDAP important for data reuse?"
objectives:
- "Understand all the different factors for reusing online data with ERDDAP"
keypoints:
- "Open data is documentation and sharing research data openly for re-use:"
- "Reusing data from another source can be challenging"
- "ERDDAP provides the ability to download data in common file formats :"
---
{% include links.md %}

# Exploring an ERDDAP data catalog

There are many ERDDAP servers to chose from. For this example, we will use the ERDDAP operated by BCO-DMO: ```https://erddap.bco-dmo.org/erddap/index.html ```

To view all the available datasets on this erddap server click "View a List of all 1095 datasets"

![image-20211026150350923](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211026150350923.png)



# Gather information about a dataset

Within the search results you have access to information about each dataset to help you decide with which dataset is useful for your application.  

* Add “ostia” in the search box (e.g. sst global ostia) and click the “Search’ button.

* In the results you should several datasets, including the one displayed below.

![image-20211026152204792](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211026152204792.png)

* The listing (pictured above) gives access to a lot of information about the dataset. In a browser, try the following:
  * Mouse over the question mark `?` under `"Summary"` to get an overview of the dataset.
  * Click `"background"` to get more complete information from the data provider about the dataset. Now go back to the search results page.
  * Click the `"M"` under `"ISO,Metadata"` to see all of the dataset metadata. A lot of information is displayed. Some important fields are:
    * `"geospatial_lat_min"`, `"geospatial_lat_max"`, `"geospatial_lon_min"`, and `"geospatial_lon_max"` for the spatial coverage
    * `"geospatial_lat_resolution"` and `"geospatial_lon_resolution"` for the size of each pixel
    * `"references"` for citing the dataset in publications
    * `"license"` for restrictions on using the data
    * `"acknowledgement"` often used to describe how to acknowledge use of the dataset
    * `"creator_name"` for the entity that created the dataset

These standardised variables is important for the dataset to be able to be "read" by other end-users and machines.

For example Google dataset search:

* open google dataset search: https://datasetsearch.research.google.com/

* search for the dataset id of the dataset above: bcodmo_dataset_3358

  ![image-20211026155703527](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211026155703527.png)









## Exercise:

Search for a dataset on their specific servers via the web application. Inspect the metadata, can you understand the dataset enought to be able to use it? : 

* ERDDAP metadata
* Searching erddap

How does a data package look? Metadata structure

\- **Accessing and visualizing data through ERDDAP**

1. ERDDAP Introduction
2. Finding datasets on ERDDAP, Gather information about a dataset
3. Visualization and download data
4. Automating ERDDAP requests
5. Timeseries and Hovmoller diagrams
6. Mapping Hurricane Jose with winds
7. Tabular Datasets, BGC-Argo data



