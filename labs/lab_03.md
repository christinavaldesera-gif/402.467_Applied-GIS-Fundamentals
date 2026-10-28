# Lab 03: Vector Digitization & Spatial Queries

## 🎯 Learning Objectives

- **Create vector layers with appropriate geometry types**: points, lines and polygons
- **Populate attributes** and use them to select features
- **Perform buffer analysis** and spatial selection
- **Interpret results and recognize limitations of historical map data**

---
## Data

- Your georeferenced raster from Lab_02
- [Optional features list for further exploration](https://drive.google.com/file/d/1mB3AK3XHbwWF7fubf6gURem44gmaPHfZ/view?usp=sharing)

---
## Steps

1️⃣ **Launch QGIS & Add your Data**
- Launch QGIS
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab03_<YourName>`
- Load the TIFF: `Layer` > `Add Layer` > `Add Raster Layer...`. Select your georeferenced TIFF layer

---
2️⃣ **Create a Landmarks Layer (points)**
- Go to `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Point
- **CRS:** EPSG:31258
- **Filename:** `Villach_landmarks.shp`
- **Add 2 fields:**
  - `Name` (String, length 50)
  - `Type` (String, length 30)
- Click OK

---
3️⃣ **Digitize Point Landmarks**
- Select `Villach_landmarks`
- Right-click > `Toggle Editing`
- Choose **Add Point Feature** from toolbar
- Choose building landmarks in and around the historical town center, at different distances from Hauptplatz:

_Example_

| # | Name | Type | 
|---|------|------|
| 1 | St. Jakob Church | church |  

**For each landmark:**
- Zoom in to the location and place a point approximately at the center of the building as drawn 
- Fill attributes: `Name` and `Type`
- Click OK

---
4️⃣ **Create River Layer (line)**
- Go to `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Line
- **CRS:** EPSG:31258
- **Filename:** `Villach_river.shp`
- **Add 2 fields:**
  - `Name` (String, 50)
  - `Type` (String, 30)
- Click OK

---
5️⃣ **Digitize the Drau River**
- Select `Villach_river` layer
- Right-click > `Toggle Editing`
- Choose **Add Line Feature**
- **Digitize 1 line, the Drau River**
- Right-click to finish the line
- Fill: `Name` = "Drau River", `Type` = "water"

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why do we create separate layers for points, lines and polygons?</summary>
  
  A single vector layer can only contain one type of geometry. This separation is fundamental to how GIS data is structured, ensuring that tools for analyses designed for points or polygons work correctly.
  </details>

---
6️⃣ **Create an Areas Layer (polygons)**
- Go to `Layer` > `Create Layer` > `New Shapefile Layer...`
- **Geometry type:** Polygon
- **CRS:** EPSG:31258
- **Filename:** `Villach_areas.shp`
- **Add 2 fields:**
  - `Name` (String, 50)
  - `Type` (String, 30)
- Click OK

> [!tip]
> To ensure connections to existing vector geometries, enable snapping! Go to Project > Snapping Options. Click the magnet icon to enable snapping, select All Layers, and set the tolerance to something like 10-15 pixels. Snapping helps connect new vertices to existing vector vertices or edges. Check that you are snapping to the intended feature.

---
7️⃣ **Digitize Polygon Features**
- Select `Villach_areas`
- Right-click > `Toggle Editing`
- Choose **Add Polygon Feature**
- **Digitize 3 polygons:** Hauptplatz and two water bodies shown on the historical map
- Follow the historical map's outlines
- Right click to finish each polygon and enter its attributes
- For Hauptplatz, enter `Name = Hauptplatz` and `Type = square`. For each water body, enter a descriptive `Name` and `Type = water`

> ❓**Question:** Click to see the answer    
<details>
  <summary>What challenges might you face when trying to define the exact boundary of a natural feature like a water body from a historical map?</summary>
  
  Historical maps often have less precise boundaries for natural features compared to modern surveys. The edge of a water body or a forest may be ambiguous, requiring interpretation from the person digitizing.
</details>

---
8️⃣ **Save All Layers**
- For each layer, right-click > `Toggle Editing`
- Click "Save changes" 
- Verify files exist: `Villach_landmarks.shp`, `Villach_river.shp`, `Villach_areas.shp`

---
9️⃣ **Select Hauptplatz Using Its Attributes**
- Open the attribute table of `Villach_areas`
- Use **Select by Expression** with `"Name" = 'Hauptplatz'`
- Confirm that **only the Hauptplatz polygon is selected**

🔟 **Create a 400 m Buffer Around Hauptplatz**
- Go to `Vector` > `Geoprocessing Tools` > `Buffer`
- **Input layer:** `Villach_areas`
- Enable **Selected features only**
- **Distance:** 400 meters
- **Output:** `Villach_Hauptplatz_400m_buffer.shp`
- Click Run

---
1️⃣1️⃣ **Select Landmarks Near Hauptplatz**
- Go to `Vector` > `Research Tools` > `Select by Location`
- **Select features from:** `Villach_landmarks`
- **Where features:** are within
- **By comparing to:** `Villach_Hauptplatz_400m_buffer`
- **Modify current selection by:** creating new selection
- Click Run

Open the landmarks attribute table and identify the selected features. **Record:** Which of your digitized landmarks lie within the 400 m buffer around Hauptplatz? How many are selected? Save your QGIS project.

---
## 🚀 Independently
- Complete **7 features in total**, including those digitized during the guided exercise: **3 points, 1 line and 3 polygons**. Choose at least one point and one polygon independently. Use the Optional Features List for Further Exploration for ideas.
- Provide a short report showing your digitized features and an example of their attributes. Include the Hauptplatz spatial selection result, name the selected landmarks, and briefly describe one limitation affecting your results.
- Locate **Silbersee and Villach Hauptbahnhof** on a current basemap, then find the same locations on the historical map. What is shown at each location on the two maps? Describe the differences and what they suggest about how Villach’s landscape has changed. Include screenshots and a few sentences in your report.
- **Optional:** Select the water polygons using `"Type" = 'water'`. Create a **100 m buffer** with **Selected features only** enabled and save it as `Villach_water_100m_buffer.shp`. Repeat the spatial selection using this buffer. Which of your digitized landmarks are within 100 m of the mapped water bodies?
