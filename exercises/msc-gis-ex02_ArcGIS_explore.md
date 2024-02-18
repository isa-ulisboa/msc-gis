# Geographic Information Systems 2023-2024

# Exercise 2 - ArcGIS Pro  - Explore your first GIS project

## Introduction

In this first project you will practice:

- create a project and a new map
- add data to the map, from a geopackage and convert to file geodatabase
- see attribute data
- change symbology and add labels
- change base maps adding external data

**What do you need:**

- data for the exercise, available from Fenix → SIGeo → Exercises → ArcGIS Pro → [ex1CLC.zip](https://fenix.isa.ulisboa.pt/downloadFile/844497944593813/ex1CLC.zip). This package 
contains three spatial layers, and a csv table:
    - water streams for Portugal (line features)
    - freguesia (smaller administrative unit in Portugal) of the municipality 
    Portalegre (polygon features)
    - land use for some freguesias of Portalegre (polygon features)
    - csv table with the classification of some categories of land use 
- lab documentation: this document

**Tasks:**

1. Download the [zip file](https://fenix.isa.ulisboa.pt/downloadFile/844497944593813/ex1CLC.zip) 
with data for the exercise and extract it to a working folder in your computer.

2. Create a new ArcGIS project named `ex02_project`, from a blank Map template, 
located inside the working folder. A new folder will be created by ArcGIS with 
the name of the project.

3. Using the file explorer of your operating system, navigate to the folder in 
your computer, and observe the structure and files of the newly created project folder:

- **ex02_project.gdb** - file folder, will contain files of the projects’ file 
geodatabase
- **ex02_project.tbx** - will contain new tools (e.g. models) of the toolbox 
created for the project
- **ex02_project.aprx** - project file. This file does not contain data, it is 
a wrapper of the projects’ information and properties
- **index** - folder that contains indexes for the project

4. Copy the folder `DataIn` from the unziped file to inside the `ex02_project` 
folder created by ArcGIS.

5. Create a new folder `DataOut` inside `ex02_project` folder.

6. Convert the geopackage files of the downloaded files to file geodatabase format by 
doing the following:
    - in the *Catalog* panel of ArcGIS, right-click on *Folders* to add a new 
    folder connection. Select the `DataIn` folder created from the zip extracted.
    - add the layers `COS2007l2`, `Portalegre` and `Waterlines` from the respective 
    geodatabases, and the table CLC1.csv. To do that, drag and drop the files 
    from the **Catalog** pane to the **Contents** pane.

7. Convert the geopackage data to file geodatabase format. You can do this in 
two ways:
	- in the **Catalog** Pane, drag and drop layers from the geopackages to 
    `ex02_project.gdb` geodatabase
    - In the Content pane, right-click on the layer you want to convert and select 
    Data → Export features. Ensure that the Output location is the `ex02_project.gdb`

8. Identify the Coordinate System of the project and layers, using *Properties* in 
the context menu of your **Map**, in the **Contents pane**.

9. See the attribute values of a feature of the `COS200712` layer, by zooming in 
and clicking on a specific feature.

10. Open the attribute table of this layer, with the context menu in the **Contents pane**, 
or using the **Attribute Table** tool in the tab Feature Layer → Data.

11. Select features (rows) from the Attribute table, and confirm that selected ones 
are highlighted on the map (double click the row, or click the zooming glass in the 
bar of the View).

12. Change the symbology of this layer, by opening Symbology from the layer's context menu.
This will open a **Symbology pane** on the right-had side. Select Unique Values 
on the `CLCl2descr` field.

13. Add labels to the layer. You can use the context menu, or the tool on the tab 
Feature Layer → Labeling.

14. Change the base map of your view, to a tiled service layer: 
    
    - In Map tab, select **Add data** tool --> Data from Path and then enter 
    ```
    http://mt0.google.com/vt/lyrs=s&hl=en&x={x}&y={y}&z={z}
    ```

    Rename the name of the layer from `Tiled service layer` to `Google Satellite` (click on the name layer to change).

15. Try additional XYZ tiles, as different backgrounds may fit better your GIS projects:

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
You may combine this GBIF map with another base map to create an interesting effect:
 - Activate both the GBIF map and, for example, Google Map for visualization in the layers 
 panel, but make sure that GBIF is on top of Google Map
 - Increase the transparency of the GBIF layer: click on the layers' name in the Contents 
 pane, and on the toolbar **Layer → Appearance**, change the value of the **Transparency** to 50%


13. Save your project. By default, the extension will be “.aprx”.

You can save all the changes you made to your project (legend, labels, visible 
layers and order, etc.). Please note that the files of the geographic layers are 
not saved inside the project file. Instead, what the project saves is the relative 
path to the storage location of the geographic files in your disk.

For this reason, it is very important to save the project with the final location 
of the files, and not to move them, or change the name of the folder where these 
are stored, after closing the project.

The ideal structure of a ArcGIS project should be, for the present example:

```
Project item                    Description

ex1CLC_project                  (project folder)
│   ex1CLC_project.aprx         (project file)
│   ex1CLC_project.gdb          (filegeodatabase file)
│   ex1CLC_project.tbx          (project tools file)
│   index                       (folder containing index files)
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
