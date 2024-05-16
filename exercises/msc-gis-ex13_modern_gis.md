# Geographic Information Systems 2023-2024

# Exercise 13 - Modern GIS

## Introduction

> **GOALS OF THE EXERCISE**
>
> - Obtain a sneak preview of the current advances on GIS
> - Identify trends and determinant technologies

In this exercise, we will try other ways, complementary to the GIS desktop software, 
to perform spatial analysis, in order to get insights on the subject under analysis. 

With the advent of multiple data sources, including open data (e.g. satellite 
imagery, citizen science, data from government and administration, etc), there 
is an increase of data, that are available at different:
- formats:
    - geopackage (gpgk)
    - geojson 
    - shapefile (shp)
    - csv
    - tiff
    - ...
- sources:
    - downloads 
    - webservices Application Programming Interfaces (API)
    - web applications
    - devices (sensors, mobile phones, cameras, Internet of Things (IoT), GPS)

In addition, data gathering, processing and analysis can use multiple technologies, 
computational platforms. Often, the combination of these in a workflow is the 
most efficient way of performing a complex task.

As a result, as a modern GIS practitioner, you need to be prepared to work and 
combine different tools and resources. Often, you will perform part of your work 
using:
- a web portal, to get insight on the data and identification of problems and 
challenges
- for example, Google Earth Engine, which is particularly powerful to facilitate 
access and process raster data
- a scripting or programming tool, for example, a Jupyter Notebook in python, to
perform data processing or analysis
- a web cloud service, like ArcGIS Online to publish your data, and enable 
additional data services.

THis exercise contains two parts:

- Use web applications to consult and analyze spatial data
- Use a python script to analyze land cover / land use

## Part 1. Use web applications

*(You should use 20 min for this part)*

In this part of the exercise, you should visit several web applications, in 
different subjects, in order to identify multiple types of data visualization methods
and data access and use. Click on the links suggested, or browse for more examples.

**ESRI's Living Atlas**

The [ArcGIS Living Atlas](https://livingatlas.arcgis.com/en/home/) is a spatial 
data repository and aggregator of data developed by ESRI and others that 
compiles data on multiple domains. The resources has different visualization 
and analysis tools, including:
- map viewer (online)
- scene viewer (online, for 3D, e.g. [OpenStreetMap 3D Buildings](https://ulisboa.maps.arcgis.com/home/item.html?id=ca0470dbbddb4db28bad74ed39949e25))
- open in ArcGIS (requires an active license of ArcGIS Pro)
- Dashboards (e.g. [Coral Bleaching Locations](https://www.arcgis.com/apps/dashboards/84ba9c03786e462d960e3172bc1b2204))
- blog entries with dynamic data (e.g. [USDA Census of Agriculture updates](https://www.esri.com/arcgis-blog/products/arcgis-living-atlas/mapping/dig-into-2022-ag-census/))
- Web applications (e.g [Sentinel-2 Land Cover Explorer](https://livingatlas.arcgis.com/landcoverexplorer))
- source code (e.g. [Imagery Explorer Apps](https://github.com/Esri/imagery-explorer-apps)),
which you can use to combine with your own code.


Please check the examples linked above, or browse to the 
[ArcGIS Living Atlas](https://livingatlas.arcgis.com/en/home/)
and find other examples. Note that most of the data layers can me directly 
accessed from your GIS desktop (ArcGIS Pro or QGIS), if you identify the URL of the 
layer.

**Other Web GIS Viewers**

Many other online platforms provide domain specific spatial visualization and 
data access