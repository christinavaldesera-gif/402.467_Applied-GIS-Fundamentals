# Lab 05: Vector Digitization & Spatial Queries

## 🎯 Learning Objectives

- **Create vector layers with appropriate geometry types** (points, lines, polygons)
- **Populate attributes meaningfully** to enable spatial queries
- **Perform buffer analysis** and spatial selection
- **Answer geographic questions** using queries

---
## Information of the Data 🗺️

- **Description:** Franziszeischer Kataster — Historical map of Villach, Austria
- **Date:** ~1800s
- **Resolution:** 0.5 meters/pixel 
- **Coordinate System:** EPSG:31258 (MGI / Austria GK M31 - Projected)
- **Dimensions:** 18,461 × 9,753 pixels
- **File Size:** 686 MB

---
## Data

For access to the data follow this link: [Digitizing](https://drive.google.com/drive/folders/1XSOCRE-oNlL-nyUumY5hwLEkK1mRC8Az?usp=sharing)

The folder contains:
- Franziszeischer_Kataster.tif (a clipped extract of the historical Franziszeischer Kataster, focusing on the Villach area)
- Optional_Features_List.pdf (a guide for further exploration)

---
## Steps

1️⃣ **Launch QGIS & Add your Data**
- Launch QGIS
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab05_<YourName>`
- Load the TIFF: `Layer` > `Add Layer` > `Add Raster Layer...`. Select the `Franziszeischer_kataster.tif`

---
2️⃣ **Create Landmarks shp (points)**
- `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Point
- **CRS:** EPSG:31258
- **Filename:** `Villach_landmarks.shp`
- **Add 2 fields:**
  - `Name` (String, length 50)
  - `Type` (String, length 30)
- Click OK

---
3️⃣ **Digitize Point Landmarks**
- Select `Villach_landmarks` layer
- Right-click > `Toggle Editing`
- Choose **Add Point Tool** from toolbar
- **Digitize 3 landmarks:**

_Example_

| # | Name | Type | 
|---|------|------|
| 1 | St. Jakob Church | church |  

**For each landmark:**
- Zoom in to the location 
- Click at the center of the building
- Fill attributes: `Name` and `Type`
- Click OK

---
4️⃣ **Create River shp (line)**
- `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Line
- **CRS:** EPSG:31258
- **Filename:** `Villach_river.shp`
- **Add 2 fields:**
  - `Name` (String, 50)
  - `Type` (String, 30)
- Click OK

---
5️⃣ **Digitize River Segment (line)**
- Select `Villach_river` layer
- Right-click > `Toggle Editing`
- Choose **Add Line Tool**
- **Digitize 1 line, the Drau River**
  
> [!tip]
> To create smooth curves when tracing features like rivers, click more frequently around the bends. The more points (vertices) you add, the more detailed and accurate your line will be.
  - Right-click to finish the line
  - Fill: `Name` = "Drau River", `Type` = "water"

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why is it better to create seperate layers for points, lines and polygons rather than putting them all in one file?</summary>
  
  A single vector layer can only contain one type of geometry. This seperation is fundamental to how GIS data is structured, ensuring that tools for analyses designed for points, or polygons work correctly.
  </details>

---
6️⃣ **Create Areas shp (polygons)**
- `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Polygon
- **CRS:** EPSG:31258
- **Filename:** `Villach_areas.shp`
- **Add 2 fields:**
  - `Name` (String, 50)
  - `Type` (String, 30)
- Click OK

> [!tip]
> To ensure your polygons connect perfectly without gaps, enable snapping! Go to Project > Snapping Options. Click the magnet icon to enable snapping, select All Layers, and set the tolerance to something like 10-15 pixels. This will make your new points 'snap' to the vertices or edges of existing features.

---
7️⃣ **Digitize Polygon Features (water bodies & main square)**
- Select `Villach_areas` layer
- Right-click > `Toggle Editing`
- Choose **Add Polygon Tool**
- **Digitize 3 polygons:** Hauptplatz (main square), water bodies visible on the map

> ❓**Question:** Click to see the answer    
<details>
  <summary>What challenges might you face when trying to define the exact boundary of a natural feature like a water body from a historical map?</summary>
  
  Historical maps often have less precise, more artistic boundaries for natural features compared to modern surveys. The edge of a water body or a forest may be ambiguous, requiring interpretation from the person digitizing.
</details>

---
8️⃣ **Save All Layers**
- For each layer, right-click > `Toggle Editing`
- Click "Save changes" 
- Verify files exist: `Villach_landmarks.shp`, `Villach_rivers.shp`, `Villach_areas.shp`

---
9️⃣ **Select Only the Water Bodies**
- Before creating the buffer, open the attribute table for Villach_areas. Select the rows corresponding to your water bodies. Later, in the Buffer tool, check the box that says 'Selected features only'. You can do this by using the `Select by Expression tool`.

🔟 **Create Buffers**
- 1st Buffer Around Water Areas:
  - Right-click `Villach_areas` layer
  - Select `Vector` > `Geoprocessing Tools` > `Buffer`
  - **Distance:** 100 meters
  - **Output:** `Villach_areas_100m_buffer.shp`
  - Click Run
- 2nd Buffer Around Hauptplatz:
  - Right-click `Villach_areas` layer
  - Check that no layer is selected
  - Go to `Vector` > `Geoprocessing Tools` > `Buffer`
  - **Distance:** 400 meters
  - **Output:** `Villach_areas_400m_buffer.shp`
- Click Run

---
1️⃣1️⃣**Run Spatial Query: Churches Near Hauptplatz**
- `Vector` > `Research Tools` > `Select by Location`
- **Select features from:** `Villach_landmarks`
- **By comparing to:** `Villach_areas_400m_buffer`
- **Where features:** are within
- Click Run

**Count results:**
- Open `Villach_landmarks` attribute table
- Note: "X features selected" at the bottom
- **Record:** How many churches are within 400m of water areas?

---
## 🚀 Independently
- Use the document _Optional Features List for Further Exploration_ to help you digitize the features on the map extent. Feel free to use other feautures too that might not be in the provided list. The total features to digitize are 7. 3 point features, 3 polygon features and 1 line feature. 
- Provide your results in a short report reflecting on your results.
- Optionally, find the location where the modern Silbersee is located. Is there anything there on the 1826 map? Digitize the historical land use for that area (e.g., as a polygon with Type = 'farmland').