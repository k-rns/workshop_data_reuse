---
title: "Introduction to serving datasets online"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
{% include links.md %}

Resources: https://coastwatch.pfeg.noaa.gov/erddapinfo/index.html 

# Why ERDDAP?

[Sample and Data Policy NSF Division of Ocean Sciences](https://www.nsf.gov/pubs/2017/nsf17037/nsf17037.jsp): "PIs are expected to **share with other researchers and the public,** ..., the data,  samples, physical collections, and other supporting materials created or gathered in the course of work under NSF grants."

[OOI Data Policy](https://ooi-website.whoi.edu/wp-content/uploads/2010/05/1102-00010_Data_Use_Policy_OOI.pdf): In principle, all OOI data will be made **publicly available**, free of charge, to anyone. 



Data acquisition -> Data Analysis -> Repository -> **Reusing**



Reusing data from another source is often difficult:

* different way of requesting data
* different formats: you work with R while colleague is working with Matlab and the other one with python
* Need for standardised metadata



ERDDAP helps with this:

*  RDDAP makes it easy to access data: ERDDAP is a data server  that gives you a simple, consistent way to download data in the format  and the spatial and temporal coverage that you want.

* Humans and machines can use ERDDAP:ERDDAP is a web application  with an interface for people to use.  It is also a RESTful web service  that allows data access directly from any computer program (e.g. Matlab, R, or  webpages).              

* Make customized maps and graphs: Use ERRDAP to generate .png and .pdf files on-the-fly from gridded and tabular scientific datasets  and insert them directly into webpages.

* Search for datasets



Whn

Reusing data: using ERDDAP as a tool

What is erddap 

what are api's and how does it work with erddap?

\- **Accessing and visualizing data through ERDDAP**



1. ERDDAP Introduction
2. Finding datasets on ERDDAP, Gather information about a dataset
3. Visualization and download data
4. Automating ERDDAP requests
5. Timeseries and Hovmoller diagrams
6. Mapping Hurricane Jose with winds
7. Tabular Datasets, BGC-Argo data

# Why use erddap?

ERDDAP is a web applications and helps you distributing data to end users who can request data and get data out in various file formats.

This is not a course on how to install data, but very much a course on how to extract and re-use data.



[ERDDAP](https://coastwatch.pfeg.noaa.gov/erddap/information.html) is a data server that gives you a simple, consistent way to download  subsets of gridded and tabular scientific datasets in common file  formats and make graphs and maps.

erddap-python is a python client for the ERDDAP Restful API, it can  obtain server status metrics, provides search methods, gives tabledap  and griddap class objects for metadata and data access.

This library was initially built for [CICESE](https://cicese.edu.mx), [CIGOM](https://cigom.org), [OORCO](https://oorco.org), and [CEMIEOceano](https://cemieoceano.mx/) projects for the automation of reports, interactive custom  visualizations and data analysis.  Most of the functionality was  inspired on the work of [erddapy](https://github.com/ioos/erddapy) library, but designed more for a more flexible backend service construction in mind.

Full API reference can be found [here](https://hmedrano.github.io/erddap-python/).

2. 

**BCO-DMO ERDDAP**

From https://oceanobservatories.org/erddap-server/

The OOI ERDDAP (National Ocean and Atmospheric Administration’s  Environmental Research Division’s Data Access Program) Server provides a simple, consistent way to access and download OOI data. Datasets can be downloaded in common file formats (e.g, CSV, NetCDF, or JSON), with the capability of creating graphs and maps, and used in several different  applications and utilities such as Python, R, Javascript, and MATLAB.

All information about every ERDAPP request is contained in the URL of each request, which  makes it easy to automate searching for and using data in other  applications. Proficient users can build their own custom interfaces.  

Many organizations (including NOAA, NASA, and USGS) run ERDDAP servers  to serve their data. Because of its widespread use and accessibility,  the ERDDAP principal developer and user community have created **[user guides](http://erddap.dataexplorer.oceanobservatories.org/erddap/index.html)**, **[instruction videos](https://youtu.be/RPIM5nFlNNY)**, and code examples to facilitate access by new users.

**What is available on the BCO-DMO server?**

OOI’s ERDDAP server has ~600 datasets listed in alphabetical order by  source (OOI array). Datasets can be searched using full text, by  metadata category or protocol, with an additional option of advanced  search. All OOI ERDDAP datasets have been uploaded on OOI’s Data  Explorer so users can access ERDDAP data there then use this amazing  tool to compare, combine, and visualize datasets.

BCO-DMO only has tabular data files on its ERDDAP server, but other repositories like OOI have netcdf files online. 

Additionally, BCO-DMO is transitioning from another server called jgofs to this more m



file is completely specified by URL

You can use the GUI, but the URL can be used and updated without having to use that GUI

## BCO-DMO data - OOI data - Repository - EDI: Data packages

How does a data package look

* Metadata structure

Examples of other data packages: 

* ECI: https://portal.edirepository.org/nis/mapbrowse?packageid=knb-lter-gce.141.30

Go over a dataset landing page -> metadata

Subsetting data

* Make sure to talk about the API



# API

API is the acronym for Application Programming Interface, which is a  software intermediary that allows two applications to talk to each  other. Each time you use an app like Facebook, send an instant message,  or check the weather on your phone, you’re using an API.

ERDDAP is both:

* Web application = webpage 

Fhttps://coastwatch.pfeg.noaa.gov/erddap/rest.html



# Searching different erddap servers

Missing: finding a dataset of interest? Maybe later in the topic aggregating data. 

* ERDDAP metadata
* Searching erddap

