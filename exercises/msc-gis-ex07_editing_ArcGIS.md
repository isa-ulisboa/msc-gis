# Geographic Information Systems 2023-2024

# Exercise 7 - Editing - ArcGIS

## Introduction

> **GOALS OF THE EXERCISE**
>
> - Learn how to create or modify new vector geographic data set (gds)
> - Learn how to edit data in attribute tables
> - Learn how to create feature templates to speed up data creation


## Source data

We will use the area of Tapada da Ajuda for the exercise. 

- The files for this exercise are in the course web page (FENIX). [Download](https://fenix.isa.ulisboa.pt/downloadFile/844497944595574/Ex07_Editing.zip) to your working area the file `Ex07_Editing.zip`

- ArcGIS tool Basemap - Imagery (alternatively, use the provided tiff image)

## Practical goals

The aims of this exercise are: 

1. to modify the shape of an existing feature, 
2. to create a line layer with roads using a template, and
3. to create a polygon layer with land parcels classified by its land use

## 1. Set up your working environment:

Start by setting up your exercise environment:

1. Create a new ArcGIS project file and folder;

2. Add the provided gds Boundary (GeoPackage format, CRS: ETRS89 / Portugal TM06, EPSG: 3763) to the map. In this case, it is not important to convert to file geodatabase format.

3. Add **Basemap → Imagery** as the background. If there is no internet access, add the ISA.tif file provided

4. Set the Boundary transparency to 60% in **Feature Layer → Appearance → Transparency**

5. Confirm that the ArcGIS map CRS is ETRS89 / Portugal TM06 (EPSG: 3763), and this is the same CRS of the Boundary layer;

6. Create an empty folder named `DataOut` to store the new gds to be created.

7. Create a new geopackage inside `DataOut` folder named `Tapada.gpkg`, to store all new final layers of the project

## 2. Modify an existing feature

The shape of the polygn in the layer Boundary needs to be adjusted in its limits, because its boundary overrides several areas. Edit the shape to adjust it to the limits in red shown in the figure.

![area](./images/ex07_arcgis_img01.jpg)

1. Make a copy of the boundary layer called `Boundary_correct` to the `Tapada.gpkg` geopackage in the `DataOut` folder. Add it to the map, if necessary.

2. Start an editing session by selecting the tab Edit

3. In the Contents pane, make sure only Boundary_correct is selected for editing

![area](./images/ex07_arcgis_img02.jpg)

4. In the Edit toolbar, select **Modify**, and then **Edit Vertices** in the right pane that was open

5. Click on **Select a feature** in this pane, and then select the feature you want to change on the map. You will notice that vertices became visible, and a new toolbar appeared on the bottom of the view pane 

![area](./images/ex07_arcgis_img03.jpg)

6. Move the vertices to adjust the shape of the polygon. If necessary, add or remove vertices selecting the appropriate tool in the toolbar.

    - It is important to make all edits at the same scale. If you change the scale between different parts of the layer, for example zooming in in one part and zooming out in another, the level of accuracy will not be consistent. 

7. If needed, you can **undo** (Ctrl+Z) or **redo** (Ctrl+Y) your edits

8. Some of the modifications are easier to do with the **Reshape** tool, which you can select on the **Modify Features** pane on the right. The next toolbar appears:

![area](./images/ex07_arcgis_img04.jpg)

9. For example, use it to reshape, in the bottom left corner, around the building. Start tracing outside the polygon, go around the building, and finish the trace again outside the polygon.

10. Save your edits frequently, and after finishing the edits.

## 3. Create a new feature class and define a template

We will create a new feature class of type line to create a layer with the roads of Tapada da Ajuda. These will be classified by the condition of the surface, as *Good*, *Fair* or *Bad*. This information will be stored in an attribute called `Status`.

Roads will be represented by lines. Every line is defined by an ordered set of vertexes (also called nodes). A straight line only requires a starting and an ending vertex (two vertexes). Vertexes between the starting and ending vertexes are required for shaping a line that is not a straight line. The line segments defined by two sequential vertexes (considering the ordered set of vertexes) are assumed to be straight line segments. 

Actually, a GIS only stores vertex coordinates and their order within the set of vertexes shaping the line. This may imply a simplification of the geographic object representation concerning its location, the so-called *feature generalization*. The allowed level of feature generalization should be fixed for every gds, stated before its creation and evaluated for conformance before the gds is delivered. It should be included in the gds metadata as well.


**QUESTION**. Could they be represented by points? Or by polygons? If yes, for any of the cases, in which situations? 

Because we know beforehand that the attribute `Status` will only have three values, we can create a template of the feature class with these values, which will speed up data insertion, and improve consistency and data quality.

1. On the **Catalog** pane, create a **New Feature Class** in the context menu of the file geodatabase of the project:

    - Provide the name `Roads` and a feature type. Click Next

    - Create a new field named `Status`, of type text, with 10 characters of length. Click Next

    - Make sure the CRS is **ETRS 1989 Portugal TM06 (EPSG: 3763)**. Click Next

    - Verify the **Tolerance**, and its meaning. This parameter is important to determine the precision of our layer. Click Next

    - Accept all the rest of the values and click Finish.
    

2. Now, let’s create the template with the predefined values Good, Fair and Bad.

    - Open the **Symbology** pane of the layer

    - Select **Unique values** for the Primary Symbology

    - Select the field `Status` for the classes. The classes table will be empty, with no categories listed.
    
    - Click on the **green plus sign**, to add unlisted values. A new pane will open
    
    - Click **Options → Add new value**, and enter the three values *Good*, *Fair* and *Bad*

    - To make all line symbols thicker, select all while holding the Shift key, and click on **More → Format** all symbols

3. Before starting to digitize, it is important to set up and activate **Snapping**. This ensures that close vertices are overlaid, ensuring lines and polygons to be connected with each other. A road must always connect to other road(s), by sharing the same vertex. This is important to ensure a correct topology between features.

   Common digitizing errors – supposing the two lines should actually intersect, the so-called error of omission and error of commission occur in the following situations:

   ![area](./images/ex07_qgis_img01.jpg)

   Unless appropriate search radius and snapping (mode and tolerance) are set, these kind of errors will always occur; to detect them, sometimes, it is necessary to zoom in to a very large scale of visualization The search radius and snapping option usage can help on avoiding to have to correct digitizing errors later on.

- In the Edit menu, click on **Snapping** group, and select the snapping options

![area](./images/ex07_arcgis_img05.jpg)
   
   - Click on **Snapping settings**, and define a value for XY tolerance. This can be set as a pixel or a map units value. Set is as 3 meters (map units)

   - You can also define the snapping tolerance by drawing a circle in the map with Se snapping tolerance, in which the radius of a drawn circle will be set as snapping distance. 
    
   - You can also try to define snapping with other values, to get the feeling how this will influence your precision in digitizing.

4. Let’s start to digitize your `Roads` layer

   - Make sure the layer is selected for editing in the Content pane

   - Click on **Edit → Create**. The right pane should open the Create Feature, with the Templates tab showing the three categories

   - Select the type of category of the road you will digitize.

   - Add the first vertex in the starting position of your road, and digitize placing vertices as needed. You can always undo.

   - Make wise decisions. If you digitize a long unique road, this will be classified as only one condition type. What happens if in the future one part of the road changes its status (is repaired or damaged)?

   - Save your edits regularly. You should have a result similar to the following

![area](./images/ex07_arcgis_img06.jpg)

   - Open the attribute table of the newly digitized layer and verify that the attribute field `Status` contains the expected values

   - Add a new field with the name `Length`, which values should be the length of each feature

   - Calculate the total length of each type of road
        - in the attribute table, right click on the name of the field `Status`, and select **Summarize**
        - Set the output location the geopackage `Tapada.gpkg`, and the name name of the output table `road_type_length`
        - Select as **Statistics Field** the field `Shape_Length` and **Statistics type** the `Sum`
        - As **Case field**, it should be selected the field `Status`

5. Finally, export your `Roads` layer to `Tapada.gpkg`, for compatibility reasons with other platforms.

**Remarks:**

- It will be necessary to decide where to start and to end a line 
   - 1. the starting or/and the ending vertexes of a line must be located on a road intersection – *an arc-node topological rule*
   - 2. start a new line whenever the road status changes

- Insert a vertex on every (foreseen) road intersection – *an arc-node topological rule*

- Save your edits often


## 4. Create a polygon layer

In this part of the exercise we will create a polygon layer with the parcels of Tapada da Ajuda, classified by its type of land use. 

Land use must be classified into two levels. First level includes 3 classes: Social area (code S), Forest (code FO) and Agriculture (code A).

Agriculture areas are further classified into: Wheat (code W), Corn (code C), Orchards (code O), Vineyard (code V), Olive (code L), Pastures (code P) and Fallow land (code F).

The following is an example of the land use classification:

![area](./images/ex07_arcgis_img07.jpg)

After creating your classification of the land use, it will be possible to determine the total economic performance of the study area, considering the following data concerning the economic performance of crops:

| Code | Crop | Yield €/ha |
|------|------|------------|
| W    | wheat | 900 |
| C | corn | 1800 |
| P | pasture | 300 |
| V | vineyard | 17000 |
| O | orchard | 8000 |

In this kind of problem, all polygons are required to be adjacent (without overlapping and without gaps – empty regions or holes – between neighboring polygons) – the set of polygons must constitute a so-called coverage of the study area.

1. Create a new feature class in the file geodatabase of the project, of type polygon, with the name `Parcels`. 
   - It should have two fields in the attribute table - `SoilUseL1`, `SoilUseL2` - of type text, with length of 2 characters. 

   - Ensure that the CRS is **ETRS 1989 Portugal TM06 (EPSG: 3763)**. 

   - Add the layer to the map.

2. Make your outline of the Boundary layer visible, but not editable (verify the pencil option of the content pane).

3. Start editing the Parcels layer, adding polygons.

   - Make sure that snapping is active
  
   - In this case, we will not use a template. We will fill in the attribute table after the polygons are created
  
   - Create your first polygon. Click on the tool Create, and polygon, on the Create Feature pane, on the right

![area](./images/ex07_arcgis_img08.jpg)

   - Start with a polygon near the `Tapada` boundary. When drawing the border of the polygon  that overlays the boundary, make sure to follow the vertices to make the two lines to completely overlay.
  
   - For the next polygon, which should be contiguous with the first one, it can share one the sides. You can use the tool 2 - **Autocomplete Polygon** - which can use one of the sides of the first polygon to autocomplete.
  
   - The tool 3 - **Trace** - is useful when you want to reuse a border of an existing feature. It will snap automatically to that line, to autocomplete a polygon.

   - To avoid open spaces between polygons, you can start by digitizing a large polygon of the whole area (or make a copy of the boundary layer), and then use the split tool to divide it into several parcels. Take a look at the series of tools available for feature modification at the **Editor tool** gallery.

  ![area](./images/ex07_arcgis_img09.jpg)

   - Notice the **Edit vertices** tool, which you can use to move vertices as with line features

   - Another useful tool is **Align Edges**, which allows you to close gaps between edges that should overlay. Do use it, you need to activate **Map Topology**

  ![area](./images/ex07_arcgis_img10.jpg)

   - Activating the Map Topology is also useful if you want to move vertices of an edge shared by two polygons. In that case, the edges of both polygons will move together.

   - Save your edits

4. Open the attribute table and fill in the values for the fields SoilUseL1 and SoilUseL2 for each feature. You may select each polygon with the Selection tool.

5. Verify any geometry problems with the tool Check Geometry (Data Management). A new table will be created with the problems detected. See online the help of the tool to see the list of problems it can identify. If problems are identified, you can use the Repair Geometry (Data Management).

6. Create a legend for the Parcels layer based on the Soil Use level 1 classification name.

7. Create a legend for the Parcels layer based on the Soil Use level 2 classification name.

8. Calculate the total economic performance of the study area, using the values for each crop in the table presented before.

9. Export your `Parcels` layer to `Tapada.gpkg`, for compatibility reasons with other platforms.