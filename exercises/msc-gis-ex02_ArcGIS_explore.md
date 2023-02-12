# Geographic Information Systems 2022-2023

# Exercise 2 - ArcGIS Pro  - Explore your first GIS project

## Introduction

In this first project you will practice:

- create a project and a new map
- add data to the map, from a geopackage and convert to file geodatabase
- see attribute data
- change symbology and add labels
- change base maps adding external data

**What do you need:**

- data for the exercise, available from Fenix → SIGeo → Exercises → ArcGIS Pro → ex1CLC.zip
- lab documentation: this document

**Tasks:**

1.  Download the zip file and extract the data packages to a working folder in your computer.

2. Create a new ArcGIS project named `ex1CLC_project`, from a blank Map template located inside the 
working folder. A new folder will be created by ArcGIS with the name of the project.

3. Using the file explorer of your operating system, navigate to the folder in your computer, 
and observe the structure and files of the newly created project folder:

- **ex1CLC_project.gdb** - file folder, will contain files of the projects’ file geodatabase
- **ex1CLC_project.tbx** - will contain new tools (e.g. models) of the toolbox created for the project
- **ex1CLC_project.aprx** - project file. This file does not contain data, it is a wrapper of 
the projects’ information and properties
- **index** - folder that contains indexes for the project

4. Copy the folder `DataIn` from the unziped file to inside the `ex1CLC_project` folder created by ArcGIS.

5. Create a new folder `DataOut` inside `ex1CLC_project` folder.

6. Convert the geopackage files of the downloaded files to file geodatabase format:
    - in the *Catalog* panel of ArcGIS, right-click on *Folders* to add a new folder connection. 
    Select the `DataIn` folder created from the zip extracted.
    - add the layers `COS2007l2`, `Portalegre` and `Waterlines` from the respective geodatabases, 
    and the table CLC1.csv. To do that, drag and drop the files from the **Catalog** 
    pane to the **Contents** pane.

5. Convert the geopackage data to file geodatabase. You can do this in two ways:
	- in the **Catalog** Pane, drag and drop layers from the geopackages to `ex1CLC_project.gdb` geodatabase
    - In the Content pane, right-click on the layer you want to convert and select 
    Data → Export features. Ensure that the Output location is the **ex1CLC_project.gdb**

6. Identify the Coordinate System of the project and layers, using Properties in the context 
menu of your Map.

7. See the attribute values of a feature, by zooming in and clicking on a specific feature.

8. Open the attribute table of this layer, with the context menu in the Contents pane, or 
using the Attribute Table tool in the tab Feature Layer → Data.

9. Select features (rows) from the Attribute table, and confirm that selected ones are highlighted 
on the map (double click the row, or click the zooming glass in the bar of the View).

10. Change the symbology of this layer (use the context menu), using Unique Values 
of the `CLCl2descr` field.

11. Add labels to the layer. You can use the context menu, or the tool on the tab 
Feature Layer → Labeling.

12. Change the base map of your view, to a tiled service layer: 
    
    - In Map tab, select **Add data** tool --> Data from Path and then 
    enter `https://www.google.cn/maps/vt?lyrs=s@189&gl=cn&x={x}&y={y}&z={z}`

13. Save your project. By default, the extension will be “.aprx”.

You can save all the changes you made to your project (legend, labels, visible layers and order, etc.). 
Please note that the files of the geographic layers are not saved inside the project file. Instead, 
what the project saves is the relative path to the storage location of the geographic files in your disk.

For this reason, it is very important to save the project with the final location of the files, and 
not to move them, or change the name of the folder where these are stored, after closing the project.

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
