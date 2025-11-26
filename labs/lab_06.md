# Lab 06: Urban Terrain Analysis & Land Cover in NYC

## 🎯Learning Objectives

- **Load and explore DEM raster data in QGIS**
- **Generate hillshade and slope rasters from a DEM**
- **Visualize and interpret land cover classes using the NYC land cover dataset**

---
## Data

For this exercise you will be working on the area of New York and specifically on Manhattan borough. The initial data has been pre-processed and downsampled according to the lab's needs. Following the link below, you can find the layers reprojected to EPSG:2263 coordinate system and the corresponding DEM and Land Cover datasets clipped to the Manhattan borough.
  
Please download the ZIP folder for your assigned borough from the link below:  

- [Download Manhattan Dataset](https://drive.google.com/file/d/19uwBKDzdKGBvUvO9NRLkES6POaDumYdI/view?usp=sharing)  

The folder contains 3 layers:
- _Manhattan_borough_2263.gpkg_ (Manhattan's border outline). A geopackage (.gpkg) contains multiple GIS datasets, including vector, raster and attribute data.
- _Manhattan_DEM.tif_ (Manhattan's Digital Elevation Model) and the complementary .aux file
- _Manhattan_land_cover_2017.tif_ (Manhattan's Land Cover) and the complementary .aux file
 
---
## Steps

1️⃣ **Launch QGIS & Add your Data**
- Launch QGIS
- Start a new project. `Project` > `New` and save it. `Project` > `Save as` in your working folder. Give it a name like `Lab06_<YourName>`
- Load the data 

---
2️⃣ **Terrain Analysis**
**Calculate Hillshade from DEM**
- Go to `Raster` > `Analysis` > `Hillshade`
- Input your loaded DEM raster
- Save the hillshade in your directory and name it e.g. `Manhattan_hillshade.tif`
- Click the `Run` button

> ❓**Question:** Click to see the answer    
<details>
  <summary>What is a hillshade?</summary>
  
  A hillshade function produces a grayscale 3D representation of the terrain surface, with the sun's relative position taken into account for shading the image. It is a qualitative method for visualising topography and does not give absolute elevation levels (ArcGIS Pro documentation).
  </details>

**Calculate Slope Raster from DEM**
- Select the _Manhattan_DEM_ layer
- Go to `Raster` > `Analysis` > `Slope`
- Input your loaded DEM raster
- Save the slope raster in your working directory and give it a name e.g.`Manhattan_slope.tif`
- Right click on the produced slope layer and go to `Properties` > `Symbology`
- Select `Singleband pseudocolor` for `Render Type`. Choose from the `Color ramp` a `RdYlGn` representation and `Invert Color Ramp` for the highest slope to be in red colour
- Press `Apply` and `OK`
- Turn off the DEM layer and position the slope layer at the top and the hillshade at the bottom of the `Layers Panel`
- Select the slope layer, go to `Properties` > `Transparency` and adjust the `Global Opacity` to 60% and assess your area

> ❓**Question:** Click to see the answer    
<details>
  <summary>How does slope works?</summary>
  
  The slope tool identifies the steepness at each cell of a raster surface. The lower the slope value, the flatter the terrain; the higher the slope value, the steeper the terrain (ArcGIS Pro documentation).
  </details>

---
3️⃣ **Create a 3D view**
- Go to `View` > `3D Map Views` > `New 3D Map View`
- Select `Configure` and go to `Terrain`. Select `DEM (Raster Layer)` for the `Type` and `Manhattan_DEM` for `Elevation`
- Select `Apply` and `OK`

4️⃣ **Corine Land Cover**
- Select the _Manhattan_land_cover_2017_ layer
- Right click and go to `Properties`
- Select `Symbology`. For `Render Type` select `Paletted/Unique values`
- Press `Classify`. You should be able to see the eight land cover classes mapped
- Set the symbology to the different classes according to the data's source. Find the dataset's land cover classes here --> [Land cover raster data](https://data.cityofnewyork.us/Environment/Land-Cover-Raster-Data-2017-6in-Resolution/he6d-2qns/about_data) 
- Select `Apply` and `OK`

---
🚀Independently
- Get familiar with the above raster data. We will use them for the next lab exercise
- Form groups and complete the following excel spreadsheet [NYC_boroughs](https://docs.google.com/spreadsheets/d/1DqHz-t5fDokLLvODb0c3RSqHBD3ykC7j/edit?usp=sharing&ouid=117699182598422702770&rtpof=true&sd=true)
- Each group should find one open GIS data source, sent to me by email and present it orally at the next lab

---
## Data Source

NYC OpenData ([https://opendata.cityofnewyork.us/](https://opendata.cityofnewyork.us/)) 