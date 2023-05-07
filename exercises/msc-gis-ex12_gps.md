# Geographic Information Systems 2022-2023

# Exercise 12 - Collect and represent GPS data on a GPS project

## Introduction

> **GOALS OF THE EXERCISE**
>
> - Learn how to record a GPS track file and add it to a GIS project
> - Create a Map Layout and identify the essential Map Elements to include

## Source data

For this exercise, we will use the final GIS project you created in Exercise 07 - Editing. Create a copy of your project and rename the main folder and project file as `Ex12`.

Additionaly, you will create a track record with a GPS app on your mobile and add it to your GIS project.

# 1. Obtain GPS data

1. Prepare your mobile phone to acquire GPS data. Install an application with the capability of recording GPS tracks. It should also allow to export/save track records as *GPX file format*.

    - Android - one of the tested applications is [A-GPS Tracker](https://play.google.com/store/apps/details?id=com.giobat.troviamoci&hl=en&gl=US).

    - iOS - one possibility is Open GPX tracker (not tested). Check your apps store for other possibilities.

    The OpenStreetMap project maintains a wiki page with a list of apps for [Android](https://wiki.openstreetmap.org/wiki/Comparison_of_Android_applications) and [iOS](https://wiki.openstreetmap.org/wiki/Comparison_of_iOS_applications).

2. Go outside and record a ~200 m track on the roads around the ISA main building. Take note of the route, to compare the GPS acquired data with the digitized roads performed in exercise 7

# 2. Add GPS data to your GIS project

1. Transfer your GPX file exported from you mobile GPS app to your computer

2. Add the track to your GIS project

    - in ArcGIS, use the tool *GPX to Feature*
    - in QGIS, add it as a vector layer

3. Assess the precision of the route provided by the GPS data in comparison to the background data and the layer you digitized. Spot and justify any errors you might find.

# 3. Create a ready-to-publish map layout

In order to include your spatial data into a publication or report, you need to create a map layout. That should include the essential elements that allow the reader to fully interpret and analyze the information you want ot convey. Several map elements can be included, some of the are a requirement. The final composition will depend on the goals and audience of the figure.

The elements to include are:

- **data frame** - displays the map layers you set visible in your project.
- **map legend** - contains the symbology of the data layers, as defined in your project
- **map title** - identifies the subject of your data.
- **compass rose** - represents the orientation of the map. The simplest representation can be an arrow indicating the north direction, but it can vary to include a full compass. 
- **scale bar** - indicates the relation between the data frame extent and the real world. It can be represented graphically as a ruler, or in a numeric format. In any case, it should include the units (m, km, feet, ...) 
- **inset map** - if justified, a map with lower scale can be included as an inset, to provide spatial context to your area of interest. The area represented in the map can be highlighted with a colour or a frame.
- **graticule** - a representation of a grid based on the CRS of the project, or in measured distances. It facilitates reading and identification of locations, and distance measures.
- **citation** - a recommended citation in text to be used by the map users. 

The fists five elements are considered to be a requirement in any map layout.

1. Create a map layout to represent roads, maps and the GPS track of the *Tapada da Ajuda* map:
    - in ArcGIS Pro, use the tool *Insert --> New layout*
    - in QGIS, use Project --> New Print Layout
    - Select the page size of the output.
        - in ArcGIS, this is defined at the moment of the insertion of the layout
        - in QGIS right-click on the page, and select *Page Properties*. A new tab appear on the right with the definitions of the page size.

2. After saving and closing your GIS project, to reopen the layout:
    - in ArcGIS, it appears as a tab in your main content pane
    - In QGIS, select *Project --> Layout manager*, and select your layout by the name you gave
       
3. Compose your map with the elements:
    - Map frame
    - North arrow
    - Legend
    - Scale bar
    - Title (as a text or label box)

In ArcGIS, the ribbon tools bar as buttons for each element.

In QGIS, the toolbar on the left contains the buttons, or add them from the menu item *Add item* 