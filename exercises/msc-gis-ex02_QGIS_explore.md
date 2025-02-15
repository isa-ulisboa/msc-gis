# Geographic Information Systems 2023-2024

# Exercise 2 - QGIS  - Explore your first QGIS project

## Introduction

In this exercise, you will have an overview of very basic and generic QGIS functions 
of QGIS interface. You will also learn to identify the different components of the 
interface of the software and the workflow to manage data and perform analysis.


## 1. Download and open a QGIS project

To prepare your environment for this first exercise using QGIS, do the following:

- Create a working folder for your course exercises named `GIS` 
- Inside, create a folder for the current exercise named `Ex02`
- Download from Fenix (menu Exercises -> QGIS) the file 
[Ex1CLC.zip](https://fenix.isa.ulisboa.pt/downloadFile/844497944593813/ex1CLC.zip) 
for the Exercise 02, to your folder Ex02 (you need to be logged-in in Fenix)
- Unzip the file Ex1CLC.zip. This should create a new folder containing a QGIS project 
file `CLC.qgz` and a folder `DataIn` containing 3 geographic data sets (files `Waterlines.gpkg`, `Portalegre.gpkg`, `COS2007l2.gpkg`). The file format is gpkg, 
meaning GeoPackage file format. It also contains a csv table named `CLC1`. 
The meaning of these datasets is:
    - water streams for Portugal (line features)
    - freguesia (smaller administrative unit in Portugal) of the municipality 
    Portalegre (polygon features)
    - land cover for some freguesias of Portalegre (polygon features)
    - csv table with the classification of some categories of land use 

- Create a folder named DataOut in the same folder where already is the folder DataIn
- launch the QGIS project by double-clicking on the file `CLC.qgz`. This should 
open a new window of QGIS.


## 2. Get familiar with QGIS 3.28 Interface

### 2.1. Interface - Terminology

The default interface of QGIS is composed by:
- main menu
- standard toolbar
- main visualization panel
- browser panel - access to data sources
- Layer panel - list of data layers added to the project 
- Processing toolbox - right panel with tools

![QGIS Interface](./images/ex01_qgis_img01.png)

### 2.2. Interface - Customization

All panels can be rearranged in the window, and resized. Other panels and toolbars 
can be added. Right-click on a empty area of the toolbar to display a list of 
available **Panels** and **Toolbars**, and activate or deactivate their display.

In alternative, you can activate/deactivate through the menu *View → Panel* or 
*View → Toolbar* 

![View Panels/Toolbars](./images/ex01_qgis_img02.png)

### 2.3. Interface and language - reset to the original configuration

Sometimes, it is convenient to reset the QGIS interface to the original default 
settings, including original panels. You can do this by going to the menu 
*Settings → Options → System* and select *Reset user interface to default settings 
(restart required)*.

It is also better to use the original english language in QGIS interface. To set 
QGIS to use english, go to menu *Settings → Options → General*, check the checkbox 
*Override System Locale* and select `American English` in the *User interface 
translation*.

### 2.4. Change basemap

By defaults, QGIS already includes *OpenStreetMap* to be used as a basemap. You 
can add it to your project selected in the **Browser panel**, *XYZ Tiles* and 
double-clicking `OpenStreetMap`. Remember to reorder the layers in the 
**Layers panel**, so that it shows in the back.

You can, however, add other tiled service layers. On the Browse 
panel, right-click on *XYZ Tyles* to add a new connection (see image). Give it the 
name `Google Satellite`, and add the URL value:
```
http://mt0.google.com/vt/lyrs=s&hl=en&x={x}&y={y}&z={z}
```

![XYZ Tyles](./images/ex01_qgis_img03.png)

Try additional XYZ tiles, as different backgrounds may fit better your GIS projects:

| Service | Connection URL |
|---|---|
| Google Satellite | http://mt0.google.com/vt/lyrs=s&hl=en&x={x}&y={y}&z={z} |
| Google Map | https://mt1.google.com/vt/lyrs=r&x={x}&y={y}&z={z} |
| Bing Satellite | http://ecn.t3.tiles.virtualearth.net/tiles/a{q}.jpeg?g=1 |
| Esri Satellite | https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x} |
| Esri World Topo | https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x} |
| CartoDB | https://cartodb-basemaps-a.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png | 
| Russian Topos| http://88.99.52.155/cgi-bin/tapp/tilecache.py/1.0.0/topomapper_v2/%7Bz%7D/%7Bx%7D/%7By%7D.jpg | 
| OpenStreetMap | https://tile.openstreetmap.org/{z}/{x}/{y}.png |
| GBIF Bird data | https://api.gbif.org/v2/map/occurrence/density/{z}/{x}/{y}@1x.png?taxonKey=212&bin=hex&hexPerTile=30&style=classic-noborder.poly |

The last link, for GBIF, serves to demonstrate how you can access different types of 
data from a web service. The GBIF URL contains the parameter `taxonKey` with the 
value `212`, which is the identifier code for the taxonomic group **Aves** in GBIF.
The map corresponds to the occurrences of birds in GBIF (hotter colors correspond
to highest number of records).

If, instead of birds, you want to have a map background for 
[pine trees](https://en.wikipedia.org/wiki/Pine) (genus *Pinus*),you just need 
to find the ID for it at GBIF, and use it on the URL:
- go to [GBIF.ORG](https://www.gbif.org) and search for *Pinus*
- click on the first result, corresponding to *Pinus* L. This will open a page
dedicated to the genus *Pinus*
- notice the URL address in your browser, which is `https://www.gbif.org/species/2684241`. 
The last figure `2684241` corresponds to the ID for this taxon.
- replace in the URL of above the value of the parameter `taxonKey` with this new value:
```
https://api.gbif.org/v2/map/occurrence/density/{z}/{x}/{y}@1x.png?taxonKey=2684241&bin=hex&hexPerTile=30&style=classic-noborder.poly
```
You may combine this GBIF map with OpenStreetMap to create an interesting effect:
 - Activate both the GBIF map and OpenStreetMap for visualization in the layers 
 panel, but make sure that GBIF is on top of OpenStreetMap
 - Increase the transparency of the GBIF layer. Right-click on the name of the 
 layer, open *Properties → Transparency* and set a value of 50%

 The result should be similar to the following:

 ![GBIF Tiles](./images/ex01_qgis_img13.png)

Navigate to your country of origin, and verify the availability of records of pine 
trees. Does it contain a good coverage? Do pine trees occur in your country,
but it is not sufficiently represented in GBIF data?

Check more about [GBIF](https://www.gbif.org/).

### 2.5. Zooming and panning

Explore the Zoom and Pane toolbar buttons to navigate and see different detail 
levels of your spatial data

![Zoom and Pane](./images/ex01_qgis_img04.png)

### 2.6. Identify project and layer metric units

Identify the current project reference system in the bottom right side of the 
status bar, in the bottom-right corner of your window. Click on the projection 
to obtain more details about the *coordinate reference system* of the QGIS 
project. This will tell also if the coordinate system as geographic or metric coordinates. 

![Project CRS](./images/ex01_qgis_img05.png)

To obtain the same information for a layer, you will right-click on the layer 
name (in the Layers panel), and select `Properties` from the context menu. 
Then, select `Source`.

### 2.7. The Identify Features tool

The Identify tool allows to click on a specific feature, to see the associated 
attributes.

![identity tool](./images/ex01_qgis_img06.png)

### 2.8. The Select Features tool

The Select tools allows to select one or more features, on which you can do 
subsequent operations. Note the *Deselect features* button.

![select tool](./images/ex01_qgis_img07.png)

### 2.9. Context menus

The context menu displays a menu with different options, specific for the item 
on which it was activated.

![context menu](./images/ex01_qgis_img08.png)

### 2.10. Create a legend/key

You can create a legend based on the attribute data of a layer. Follow the 
steps in the image to create a legend for the layer `COS200712`.

![legend](./images/ex01_qgis_img09.png)

Repeat the procedure on the same layer, but select a numeric attribute.

![legend](./images/ex01_qgis_img10.png)

### 2.11. Add labels to the spatial features

You can create add labels to the features based on the attribute data of a layer. Follow the 
steps in the image add labels to the layer `COS200712`.

![labels](./images/ex01_qgis_img11.png)

### 2.12. Save or Save as

You can save all the changes you made to your project (legend, labels, visible layers and order, etc.). 
Please note that the files of the geographic layers are not saved inside the project file. Instead, 
what the project saves is the relative path to the storage location of the geographic files in your disk.

For this reason, it is very important to save the project with the final location of the files, and 
not to move them, or change the name of the folder where these are stored, after closing the project.

The ideal structure of a QGIS project should be, for the present example:

```
Project item                Description

ex1CLC                      (project folder)
│   CLC.qgz                 (project file)
│
└───DataIn (folder)         (subfolder)
│   │   CLC1.xls            (data file)
│   │   COS200712.gpkg      (data file, geopackage)
│   │   Portalegre.gpkg     (data file, geopackage)
│   │   Waterlines.gpkg     (data file, geopackage)
│   │   ...
│   
└───DataOut (folder)
    │   ...
```

You can also save the project with a new name:

![labels](./images/ex01_qgis_img12.png)
