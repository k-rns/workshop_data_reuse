---
title: "Data requests using an ERDDAP URL"
teaching: 20
exercises: 0
questions:
- "How do a download an ERDDAP table dataset to my local computer using python?"
objectives:
- "Creating the ERDDAP download URL"
- "Downloading an ERRDAP table dataset with Python"
keypoints:
- "Tabledap request URLs are in the form: server/protocol/datasetID.fileType{?query}"
- "urllib library works with https protocols"

---



We have just seen that we can search erddap for datsets. The main takeaways were:

* ERDDAP is a tool and many repositories can have an ERDDAP server, which means that there are **many erddap servers** around. 

* You can search 2 types of data, also called **protocols**: tabledap & griddap 
* A dataset in ERDDAP can be downloaded in many **different file types**, based on what you need.
* You can **subset a dataset** based on constrainting the variables.

In the next chapter, we'll see that an ERDDAP can not only be used in the web interface like we did, but also as a URL that computer programs can use  (in this case, to get data, graphs, and information about datasets).

# The ERDDAP REST API Service

What is an API? API is the acronym for Application Programming Interface, which is a  software intermediary that allows two applications to talk to each  other. Each time you use an app like Facebook, send an instant message,  or check the weather on your phone, you’re using an API.

ERDDAP REST API Service = Requesting data using a URL. All information about every ERDAPP request is contained in the URL of each request, which  makes it easy to automate searching for and using data in other  applications. Proficient users can build their own custom interfaces.  

**Tabledap request URLs must be in the form** 

* server/protocol/datasetID.fileType{?query }
*  https://coastwatch.pfeg.noaa.gov/erddap/tabledap/pmelTaoDySst.htmlTable?longitude,latitude,time,station,wmo_platform_code,T_25&time%3E=2015-05-23T12:00:00Z&time%3C=2015-05-31T12:00:00Z 

Thus, the query is often a comma-separated list of desired variable names, followed by a collection of  constraints (e.g., *variable*<*value*),  each preceded by '&' (which is interpreted as "AND").

**Details:**

- Requests must not have any internal spaces.

- Requests are case sensitive.

- {} is notation to denote an optional part of the request.  
  
- [**datasetID**](http://www.neracoos.org/erddap/tabledap/documentation.html#datasetID) identifies the name that ERDDAP  assigned to the source web site and dataset  (for example, pmelTaoDySst). You can see a list of    [datasetID options available via tabledap](http://www.neracoos.org/erddap/tabledap/index.html).  
  
  
  



# Building the URL of a dataset
Example dataset that we will be using: https://www.bco-dmo.org/dataset/815732




### 1. ERDDAP server you want to get data
https://erddap.bco-dmo.org/erddap

### 2. Protocol

Protocols are the standards which specify how to request data.  Different protocols are appropriate for different types of data and for different client applications.

**griddap** lets you request a data subset, graph, or map from a  gridded dataset (for example, sea surface temperature data from a satellite), via a specially formed URL

ets you request a data subset, a graph, or a map from  a tabular dataset (for example, buoy data), via a specially formed URL

tabledap / griddap

### 3. Choose your file type

Specifies the type of table data file that you  want to download. You can use different filetype based on your specific needs and your community, you can download files for matlab binary file, netcdf, .csv (for R and Python), GIS, etc. The column below gives all the formats available:   

| Data fileTypes                                               | Description                                                  |
| ------------------------------------------------------------ | :----------------------------------------------------------- |
| [.asc](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_asc) | View OPeNDAP-style ISO-8859-1 comma-separated text.          |
| [.csv](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_csv) | Download a ISO-8859-1 comma-separated text table (line 1: names; line 2: units; ISO 8601 times). |
| [.csvp](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_csvp) | Download a ISO-8859-1 .csv file with line 1: name (units). Times are ISO 8601 strings. |
| [.csv0](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_csv0) | Download a ISO-8859-1 .csv file without column names or units. Times are ISO 8601 strings. |
| [.dataTable](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_dataTable) | A JSON file formatted for use with the Google Visualization client library (Google Charts). |
| [.das](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_das) | View the dataset's metadata via an ISO-8859-1 OPeNDAP Dataset Attribute Structure (DAS). |
| [.dds](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_dds) | View the dataset's structure via an ISO-8859-1 OPeNDAP Dataset Descriptor Structure (DDS). |
| [.dods](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_dods) | OPeNDAP clients use this to download the data in the DODS binary format. |
| [.esriCsv](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_esriCsv) | Download a ISO_8859_1 .csv file for ESRI's ArcGIS 9.x and below (separate date and time columns). |
| [.fgdc](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_fgdc) | View the dataset's UTF-8 FGDC .xml metadata.                 |
| [.geoJson](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_geoJson) | Download longitude,latitude,otherColumns data as a UTF-8 GeoJSON .json file. |
| [.graph](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_graph) | View a Make A Graph web page.                                |
| [.help](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_help) | View a web page with a description of tabledap.              |
| [.html](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_html) | View an OPeNDAP-style HTML Data Access Form.                 |
| [.htmlTable](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_htmlTable) | View a UTF-8 .html web page with the data in a table. Times are ISO 8601 strings. |
| [.iso19115](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_iso19115) | View the dataset's ISO 19115-2/19139 UTF-8 .xml metadata.    |
| [.itx](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_itx) | Download an ISO-8859-1 Igor Text File. Each response column becomes a wave. |
| [.json](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_json) | View a table-like UTF-8 JSON file (missing value = 'null'; times are ISO 8601 strings). |
| [.jsonlCSV1](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_jsonlCSV1) | View a UTF-8 JSON Lines CSV file with column names on line 1 (mv = 'null'; times are ISO 8601 strings). |
| [.jsonlCSV](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_jsonlCSV) | View a UTF-8 JSON Lines CSV file without column names (mv = 'null'; times are ISO 8601 strings). |
| [.jsonlKVP](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_jsonlKVP) | View a UTF-8 JSON Lines file with Key:Value pairs (missing value = 'null'; times are ISO 8601 strings). |
| [.mat](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_mat) | Download a MATLAB binary file.                               |
| [.nc](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_nc) | Download a flat, table-like, NetCDF-3 binary file with COARDS/CF/ACDD metadata. |
| [.ncHeader](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncHeader) | View the UTF-8 header (the metadata) for the NetCDF-3 .nc file. |
| [.ncCF](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncCF) | Download a NetCDF-3 CF Discrete Sampling Geometries file (Contiguous Ragged Array). |
| [.ncCFHeader](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncCFHeader) | View the UTF-8 header (the metadata) for the .ncCF file.     |
| [.ncCFMA](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncCFMA) | Download a NetCDF-3 CF Discrete Sampling Geometries file (Multidimensional Array). |
| [.ncCFMAHeader](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncCFMAHeader) | View the UTF-8 header (the metadata) for the .ncCFMA file.   |
| [.nccsv](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_nccsv) | Download a NetCDF-3-like 7-bit ASCII NCCSV .csv file with COARDS/CF/ACDD metadata. |
| [.nccsvMetadata](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_nccsvMetadata) | View the dataset's metadata as the top half of a 7-bit ASCII NCCSV .csv file. |
| [.ncoJson](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_ncoJson) | Download a UTF-8 NCO lvl=2 JSON file with COARDS/CF/ACDD metadata. |
| [.odvTxt](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_odvTxt) | Download longitude,latitude,time,otherColumns as an ISO-8859-1 ODV Generic Spreadsheet File (.txt). |
| [.subset](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_subset) | View an HTML form which uses faceted search to simplify picking subsets of the data. |
| [.tsv](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_tsv) | Download a ISO-8859-1 tab-separated text table (line 1: names; line 2: units; ISO 8601 times). |
| [.tsvp](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_tsvp) | Download a ISO-8859-1 .tsv file with line 1: name (units). Times are ISO 8601 strings. |
| [.tsv0](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_tsv0) | Download a ISO-8859-1 .tsv file without column names or units. Times are ISO 8601 strings. |
| [.wav](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_wav) | Download a .wav audio file. All columns must be numeric and of the same type. |
| [.xhtml](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/documentation.html#fileType_xhtml) | View a UTF-8 XHTML (XML) file with the data in a table. Times are ISO 8601 strings. |

In this lesson we will use the .csv file type to import it in Jupyter Notebook and work with the Pandas library. 

IMPORTANT NOTE: The actual extension of the resulting file may be slightly different than the fileType (for example,  .htmlTable returns an .html file).  **To get a .csv file with the header names in the first row the file type is .csvp.** 



## 4. Data request

The data request in the URL starts with `?`

Then add the variables of interest: all variables

* Cruise_ID
* Cast_ID
* Station_ID
* UTC_Date
* UTC_Time
* time
* latitude
* longitude
* depth
* Strain_Gauge_Pressure
* Conductivity
* Salinity
* Temperature
* Potential_Temp
* Density
* Sigma_theta
* Oxygen_MLL
* Oxygen_pcnt
* PAR_Irradiance
* ISUS
* flag



NOTE: Just generate the URL: 

Erddap table: https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_815732.csv?Cruise_ID,Cast_ID,Station_ID,UTC_Date,UTC_Time,time,latitude,longitude,depth,Strain_Gauge_Pressure,Conductivity,Salinity,Temperature,Potential_Temp,Density,Sigma_theta,Oxygen_mLL,Oxygen_pcnt,PAR_Irradiance,ISUS,flag



# Download the dataset with Python

Download/import the **urllib package** into the Python environment  to work with url's in your environment:  [Python Documentation](https://docs.python.org/3/library/urllib.html)

```python
# Import the urllib library
import urllib.request

#define the url you want to download
download_url = https://erddap.bco-dmo.org/erddap/tabledap/bcodmo_dataset_815732.csv?Cruise_ID,Cast_ID,Station_ID,UTC_Date,UTC_Time,time,latitude,longitude,depth,Strain_Gauge_Pressure,Conductivity,Salinity,Temperature,Potential_Temp,Density,Sigma_theta,Oxygen_mLL,Oxygen_pcnt,PAR_Irradiance,ISUS,flag
    
# Define where you want to save the file on your computer
path_to_save = 

# download the dataset   
urllib.request.urlretrieve(url, "path to save")
```


## Resources

* NOAA satellite training: https://coastwatch.pfeg.noaa.gov/projects/erddap/
* Work with satellite data in python (extract data from erddap): https://coastwatch.gitbook.io/satellite-course/tutorials/python-tutorial/1.-how-to-work-with-satellite-data-in-python 

* pangeo data access (Rich Signell): http://gallery.pangeo.io/repos/rsignell-usgs/esip-gallery/05_ERDDAP_access.html 
