# Geographic Information Systems 2023-2024

# Exercise 10 - Analysis with DTM

## Introduction

> **GOALS OF THE EXERCISE**
>
> - create a Digital Terrain Model for the region of Esposende (North of Portugal)

## Source data

- The files for this exercise are in the course web page (FENIX). [Download](https://fenix.isa.ulisboa.pt/downloadFile/281547991171489/Ex10_DTM.zip) to your working area the file `Ex10_DTM.zip`

The geopackage file `EspTopography_TM06` contains 5 gds containing:
- `RegionBoundary` - the region boundary
- `PointHeights` - a set of point heights
- `ContourLines` - a set of contour lines, with an attribute *elevation*
- `Streams` - a set of lines representing the main surface streams
- `RidgeLines` - a set of lines representing ridgelines located in the study area

The gds representing point heights, streams and ridgelines are 3D (they include the z coordinate values)

## 1. Create a DEM using the points, ridgelines, streams and contour gds

1. Create a TIN, using only the `PointHeights` and `ContourLines` layers
    - in ArcGIS, use the Create TIN (3D Analyst Tool) tool
    - in QGIS, use the TIN interpolation tool, in Processing tools

2. Export the tin as a raster surface, with 10 m pixel resolution
    - in ArcGIS, use TIN to Raster (3D Analyst Tool)
    - in QGIS, a raster is already created in the previous step. 

3. Export the created raster as a tif image, using the context menu of the layer.

4. Repeat the previous steps 1-3, but using additionally `Streams` and `RidgeLines` as Hard/Break lines 

## 2. Create a raster gds representing slope in the study area

1. Use as parameters the pixel resolution 10 m and CRS ETRS89 / Portugal TM06 (EPSG: 3763, and the following tool:

    - in ArcGIS, use Slope (3D Analyst) tool or the Surface Parameters (3D Analyst) tool. Check the help of each tool, identify the main difference between them and discuss which is more appropriate for your case.

    - in QGIS, use Raster -> Analysis -> Slope

2.  On this gds legend use the following seven intervals:

    - 1 - [0%; 0.5%]
    - 2 - ]0.5% ; 2%]
    - 3 - ]2% ; 5%]
    - 4 - ]5% ; 9%]
    - 5 - ]9% ; 16%]
    - 6 - ]16% ; 30%]
    - 7 - > 30%

## 3. Create a raster gds representing aspect in the study area

1. Use as parameters the pixel resolution 10 m and CRS ETRS89 / Portugal TM06 (EPSG: 3763, and the following tool:
    - in ArcGIS, you can use the Aspect (3D Analyst) tool or the Surface Parameters (3D Analyst) tool. 
    - in QGIS, use Raster -> Analysis -> Aspect

2. Build a suitable legend for this gds