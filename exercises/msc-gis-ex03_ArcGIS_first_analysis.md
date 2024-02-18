# Geographic Information Systems 2023-2024

# Exercise 3 - ArcGIS Pro  - Perform you first analysis with ArcGIS

## Introduction

The goals of these exercise are:

- To create a geographic data set (gds), in a folder named DataOut, representing 
locations from the gds COS2007l2 that simultaneously verify the following requirements:

>    - have a water stream within a distance less than or equal to 1 km
>    - have a 1st level of the CLC (Corine Land Cover project) classification as 
>    “Agricultural areas” or “Forest and semi natural areas”

 - To calculate:

>    - The areas of “Agriculture” or “Forest and semi natural areas”, in ha
>    - The areas per administrative region "freguesia" of “Agriculture” or 
“Forest and semi natural areas”, in ha

**What do you need:**

For this exercise, you should use the same project as saved in the final of the exercise 02.
It includes:

- the input data for the exercise 01, also available from Fenix → SIGeo → 
Exercises → ArcGIS Pro → [ex1CLC.zip](https://fenix.isa.ulisboa.pt/downloadFile/844497944593813/ex1CLC.zip). It contains three spatial layers, and a csv table:
>    - gds COS2007l2 (geometry: polygons) – land coverage according to the 2nd 
    level classification of the project CORINE Land Cover
>    - gds WaterLines (geometry: lines) – waterlines (rivers but not only)
>    - gds Portalegre (geometry: polygons) – administrative boundaries (freguesias)
>    - table CLC1 (table) – the 1st level classification of the project CORINE Land Cover

**Expected output**

You should prepare your environment to save the output layers, using the Catalog Pane:
> - create a folder under “DataOut”
> - create a new geopackage inside the new folder named "ex03_out.gpkg”. This geopackage 
will store new layers. Details on how to create the geopackage later in the exercise.


**Requirements**

> You will use ArcGIS Pro to perform this exercise. You are expected to have already 
previous knowledge about the fundamentals of GIS, and spatial analysis workflows,
which should help to identify and use the tools of ArcGIS in an autonomous way.

> You should also be able to use ArcGIS Pro documentation, search, learn and solve questions 
on how to use the tools. The documentation is available, either from the **Help** 
of the software, or [online](https://pro.arcgis.com/en/pro-app/2.9/help/main/welcome-to-the-arcgis-pro-app-help.htm). 


**Quality control**
> You are required to make quality assessment steps through out the workflow. 
This involves:
> - check the if the results of each spatial operation make sense. 
>      - this may require additional calculations by hand, for example, to 
cross-check area values in square meters with hectares
>      - spatial operations may results in outdated data in the attribute tables 
of the outputted gds. This requires review, clean and update these tables
> - ensure that data inputs and data outputs are correctly managed
>     - imported datasets do not contain errors (in the attribute values)
>     - file names are correctly spelled and file location is the expected (cross-check 
using the file explorer of your system)
>     - the project is frequently saved, and can be closed and open without issues

<br>
<br>

## Task 1 - Create a geographic data set (gds) in a folder named DataOut representing locations from the gds COS2007l2 that simultaneously verify the following requirements:


**A. There is a waterline within a distance less than or equal to 1 km**

**B. The 1st level of the CLC (Corine Land Cover project) classification is 
“Agricultural areas” or “Forest and semi natural areas”**


**One solution:**

1. Clip the gds **Waterlines** (7589 lines), in order to reduce these data to 
the **COS2007l2** polygon layer (only 62 lines):
    
    - use the Clip spatial operation (in tab *Analysis → Tools → Clip*) and 
    create a new gds named `WlinCOS`, in file geodatabase **ex02_project.gdb**.

    **IMPORTANT NOTE: Clipping is not a commutative operation. The order on which
    you define the layers as input or clip features is important.**

    - update the attribute field **LENGTH** with correct values:
        - open the Attribute table of the newly created layer
        - right-click on the name of field **LENGTH** and select `Calculate 
        Geometry`. Select *Length* as property and *meters* as unit
        - Add a new field **LENGHT_KM**, with type *double*, and save. Calculate 
        the values of this field using `Calculate Field` by dividing the values 
        in field LENGTH by 1000

2. To find out *regions within a distance less than or equal to 1 km from the 
clipped waterlines* (layer **WlinCos**), do the following:
    - use the **Buffer** spatial operation (Tab *Analysis → Tools → Buffer*) 
    operation on the layer **WlinCOS** and create a new gds named `WlinCOSB1000` 
    (in file geodatabase **ex02_project.gdb**). Remember to dissolve the result.

3. Find the regions from **COS2007l2** that are within a distance less than or 
equal to 1 km from the clipped waterlines:
    - use (again) the Clip spatial operation on **COS2007l2** to clip it with 
    **WlinCosB1000**, and create a new gds named `CosL2WlB` (in file geodatabase 
    **ex02_project.gdb**)
    - add an attribute field **areaHa** of type *double* and calculate values 
    using `Calculate Geometry` (area unit in ha)
    - add an attribute field **perimKm** and calculate the perimeter in km

4. Perform a join operation to append the 1st level of the CORINE Land Cover 
(table **CLC1.csv**) to the **CosL2WlB** layer
    - use the **Join** function, available on the context menu of the layer 
    **CosL2WlB**. The join field column is CLCl1code   
        - the join table is **CLC1.csv**, and the join table field is `l1code`. 
        Verify in the attribute table that the fields of the CLC1 table were appended

5. On this layer, select the polygons classified as **“Agricultural areas” or 
“Forest and semi natural areas”** using the **l1description** attribute
    - use the **Select By Attribute** tool (available on the Map tab) and logical 
    conditions (logical operators: AND, OR)

6. Save the previously selected polygon as a new gds:
    - use the tool **Data → Export features** (or the context menu of the 
        layer) to save the selection as **AgricForInWlB1000**. Since a selection 
        is active, only the selected features will be included in the export.
        
7. To ensure interoperability with other systems, it is a good practice to save 
the final output of our analysis in an open format. We will use *Geopackage* for 
this purpose.
    - create a new geopackage geodatabase to hold the exported data
        - in **DataOut** folder, right-click and select New → GeoPackage. Set 
        the name of the file as `ex03_out.gpkg`
        - right-click on the layer **AgricForInWlB1000** and select export features.
        Define as output location the geopackage geodatabase just created
        - set the output name as `AgricForInWlB1000` and execute.
        - To verify the interoperability of the standard geopackage database, save 
        your ArcGIS project and close the application. Open QGIS and add the 
        layer **AgricForInWlB1000** in the **ex03_out.gpkg** geopackage.

## Task 2 - Calculate:

**A. The areas of “Agriculture” or “Forest and semi natural areas”, in ha**

**B. The areas per administrative region "freguesia" of “Agriculture” or 
“Forest and semi natural areas”, in ha**

**One solution:**

*To answer to question A:*

1. Dissolve the gds AgricForInWlB1000 in order to create one polygon representing 
    land classified as “agricultural areas” and one polygon representing land 
    classified as “Forest and semi natural areas”
        - use the **Dissolve** spatial operation by attribute `l1description` and create 
        a new gds in a file named `AgricForDiss` (in file geodatabase **ex02_project.gdb**)

2. Create and calculate values for the following attributes using calculate geometry as before:
    - area in sq meters: `areaM2`
    - area in hectares: `areaHa`
    - perimeter in kilometers: `perimKm` 

*To answer to question B:*

1. Create polygons by the 1st class of land coverage classification (“agricultural 
areas” or “Forest and semi natural areas”) subdivided by “freguesia”
    - use the **Intersect** spatial operation to intersect **AgricForDiss** 
    with **Portalegre** and create a new gds named `AgricForFreg`
    - update the **Symbology** to display the combination of land cover and freguesias
        - use the **Expression Builder** tool and build the expression 
        ```
        $feature.l1description + “ - “ + $feature.Desc_Simpli
        ````

2. Update the values of attributes **areaM2**, **areaHa** and **perimKm**

## Task 3 - Describe quality control measures

Describe which quality control measures did you take during the analysis workflow:
- ...
- ...
- ...

...

## Summary and wrap up – Intro do ArcGIS Pro

This is what you leaned during the first three exercise:

- ArcGIS support documentation
- Opening a ArcGIS project
- The ArcGIS Pro interface
    - Terminology
    - Identify and reset panes
    - Zooming and panning
    - Viewing and hiding toolbars
    - Understand file geodatabases
    - Connecting to Google Satellite Imagery
    - Other buttons of the standard toolbar
        - Open Attribute Table
        - Identify Features
        - Select Features
        - Deselect Features from All Layers
    - Saving a ArcGIS project
        - Save
        - Save As …
    - Exiting a ArcGIS project
- Some basic ArcGIS Pro functions
    - Active Layer Context Menu / Properties / Symbology
        - Single symbol
        - Unique values (categorical legend)
        - Graduate colors (numerical legend
    - Active Layer Context Menu / Properties / Labels
    - Active Layer Context Menu / Properties / Joins
    - Active Layer Context Menu / Export / Save Selected Features As …
    - Calculate Geometry
    - Calculate Field
        - Creating a new attribute filled with values
        - Functions: $length, $area and $perimeter
    - Selecting features using a logical expression (condition)
    - Vector menu / Analysis Tools
        - Buffer
        - Clip
        - Dissolve
        - Intersect        
- Map legends (categorical and numerical)
- Map labels
- Non-spatial operations
    - Select By Attribute
    - Join of 2 tables (associations 1:n)
- Spatial operations
    - Clip
    - Buffer
    - Dissolve
    - Intersect


