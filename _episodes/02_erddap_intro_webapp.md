---
title: "ERDDAP, API, REST, URL: Acronym to data reuse"
teaching: 45
exercises: 0
questions:

- "What is ERDDAP"
- "Why is ERDDAP important for data reuse?"
objectives:
- "Understand all the different factors for reusing online data with ERDDAP"
keypoints:
- "ERDDAP:"
- "API:"
- "URL:"
---
{% include links.md %}



# Open Data

Open data has the potential to accelerate science. If we don't have to re-invent the wheel, we can move forward in a faster way.

When applying for grants nowadays, often there is a requirement that as a scientist you need to share your data with the public:

* **NSF-OCE**: [Sample and Data Policy NSF Division of Ocean Sciences](https://www.nsf.gov/pubs/2017/nsf17037/nsf17037.jsp): *"PIs are expected to **share with other researchers and the public,** ..., the data,  samples, physical collections, and other supporting materials created or gathered in the course of work under NSF grants."*
* **Ocean Observatory Initiative**: [OOI Data Policy](https://ooi-website.whoi.edu/wp-content/uploads/2010/05/1102-00010_Data_Use_Policy_OOI.pdf): In principle, *all OOI data will be made **publicly available**, free of charge, to anyone.*
* **Biogeochemical Argo**: [data management rules](https://biogeochemical-argo.org/data-management.php): *data are made **publicly available***



When working with Open Data it is important that end-users reusing data have all the knowledge necessary to be able to trust and understand the data they want to re-use.  End-users can be both humans and computers

Domain-specific repositories and have the role to make sure the data they receive have the correct domain- specific, standardized metadata and make them publicly available. Metrics to see if a package is truly "Open Data" are the  F.A.I.R principles. 

Researcher (data acquisition & analysis) -> Data Repository ->  Data Reuse (multiple researchers)



# Aligning data sources 

Reusing data from another source is often difficult:

* different way of requesting data
* different formats: you work with R while colleague is working with Matlab and the other one with python
* Need for standardised metadata

Example Dryad (without naming the repo): excel file or matlab file. 

**This is where ERDDAP comes in.** It gives repo's the ability to, in a consistent way, download  subsets of gridded and tabular scientific datasets in common file formats and make graphs and maps. 

Many repositories use an erddap server to distributing data to end users who can request data and get data out in various file formats.  



# Repo specific ERDDAP servers

Many organizations (including NOAA, NASA, and USGS) run ERDDAP servers  to serve their data. Because of its widespread use and accessibility,  the ERDDAP principal developer and user community have created **[user guides](http://erddap.dataexplorer.oceanobservatories.org/erddap/index.html)**, **[instruction videos](https://youtu.be/RPIM5nFlNNY)**, and code examples to facilitate access by new users.



**BCO-DMO ERDDAP** 

* Domain:

* BCO-DMO only has tabular data files on its ERDDAP server, but other repositories like OOI have netcdf files online. 
* Server: https://erddap.bco-dmo.org/erddap/index.html 



**OOI**

* Domain: 

* OOI’s ERDDAP server has ~600 datasets listed in alphabetical order by  source (OOI array). Datasets can be searched using full text, by  metadata category or protocol, with an additional option of advanced  search. All OOI ERDDAP datasets have been uploaded on OOI’s Data  Explorer so users can access ERDDAP data there then use this amazing  tool to compare, combine, and visualize datasets

* Server: https://erddap.dataexplorer.oceanobservatories.org/erddap/index.html 



BGC-Argo: Do they have an erddap server?  

* Domain: 
* Description
* Server



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

