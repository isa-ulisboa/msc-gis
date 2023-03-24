# Geographic Information Systems 2022-2023

# Exercise 8 - Spatial interpolation

## Introduction

> **GOALS OF THE EXERCISE**
>
> - Introduction to the raster data structure
> - Estimate a continuous surface based on a sample of values (points). 

## Source data

- The files for this exercise are in the course web page (FENIX). [Download](https://fenix.isa.ulisboa.pt/downloadFile/844497944595944/Ex08_Interpolation.zip) to your working area the file `Ex08_Interpolation.zip`

Layers:

The geopackage `DataIn.gpkg` contains 3 vector data sets and 3 tables: 

**Vector data**
- `Boundary` - represents the boundary of a phreatic aquifer.
- `Wells` - represents well locations on the aquifer and its concentration of nitrate (unit is mg/l).
- `Soil` - describes the soil type. The code attribute uses the codes of soil type listed in table SoilTypeDescr.

**Tables**

- `Freguesias` - freguesias in the study area
- `SoilTypeDescr` - soil type description
- `Soiluse` - soil use description


**Raster**

- `Freguesias` - represents the civil parishes of the study area (raster data set). The code description for every freguesia is in table Freguesias.
- `Use1990`, `Use2002` and `Use2003` - describes the soil use in 1990, 2002 and 2003 (raster data sets). The soil use codes are listed in table SoilUse.


## 1. Get familiar with your data and your problem

1. Make a preliminary analyses of the characteristics of raster data sets
    
     – using Layer properties > Source tab, analyse the raster file characteristics: number of rows and columns, cell size, pixel type, raster extent and CRS.

2. Always start by creating a diagram of operations before implementing a solution for the next problems.

## 2. Problem 1: legends

Create legends for Soil, Freguesias, Use1990, Use2002 and Use2003. 

- Use the appropriate symbology to represent the unique categories

- In ArcGIS, after the creation of unique categories, it is possible to create a join to a non-spatial table, using a numeric field. In this case, you can join to the table `Freguesias`, to have their names represented in the legend.

## 3. Problem 2: conversion (vector to raster), boolean reclassification and overlay operations

Identify the zones of civil parish Estela (code=4) with soil use Horticulture in 2003 (code=9) and soil type arenosol (code=1). 

Tools needed:
- Reclassify (Spatial Analysis tools)
- Feature to Raster (Conversion tools) - **Note**: you can use an existing raster to provide the *environment* (extent, cell size, snap raster) to the new raster created
- Raster Calculator

## 4. Problem 3: conversion (raster to vector)

Create a vector gds representing the regions the civil parish Estela (code=4) with soil use Horticulture in 2003 (code=9) and soil type arenosol (code=1).

Tools needed:
- Raster to Polygon

## 5. Problem 4: create a continuous surface from a sample of points

Based on the NO3 concentration values observed in the wells (layer Wells), estimate the NO3 concentration in the groundwater using the IDW method.

The IDW method generates a raster gds. The estimated value (the pixel value v) is a convex linear combination of the sample values: v=∑ci´vi with ci´= ci/∑ci (so ∑ ci´=1), ci=(1/di)p and di are the distances to the sample points. The power p allows to adjust the distance weight.

1. Explore your data:
- In the layer Wells, calculate the basic statistics for the attribute NO3conc: min, max, mean, median, std. dev., count
- On the attribute table, use the context menu on the field name
create a symbology with proportional symbols to represent the concentration of NO3

2. Create a continuous surface estimated by the IDW method

    Tools needed:
    - IDW or Geostatistical Wizard

    Parameters needed:
    - Max neighbors - max number of samples to be used
    - Min neighbors - min number of samples to be used
    - Sector type - defines how will the method search for the closest samples
    - Angle - if an anisotropy is present, this is the orientation of the major axis

    The values of these parameters need to be decided based on the preliminary statistical analysis. Additionally, the Geostatistical Wizard provided the cross-validation method to assess your model results.

## 6. Problem 5: create a continuous surface from a sample of points

Based on the NO3 concentration values observed in the wells, estimate the NO3 concentration in the groundwater using the IDW method but changing some of the parameter values. Try to interpret the differences between the two gds.

## 7. Problem 6: reclassification

Reclassify the raster created on problem 4 in order to create a new raster gds with pixel values 1, 2, …, 5 representing the 5 classes of NO3 concentration: ]0 – 25]; ]25 – 50]; ]50 – 100]; ]100 – 150]; > 150.

## 8. Additional problem:

Build a raster gds representing the variation on forest use between 1990 and 2002.
