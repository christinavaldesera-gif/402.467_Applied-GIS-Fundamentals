# Lab 04: Handling Vector Data ~ Network Analysis

## Introduction  

Network analysis in QGIS uses spatial data to model networks, such as roads or pathways. This allows for the calculation of routes and accessibility. It helps identify the best paths between locations by considering factors like distances and speed limits. This functionality supports transportation planning, navigation and solving geographic problems in urban areas. Check QGIS official documentation [QGIS network analysis documentation](https://docs.qgis.org/3.40/en/docs/user_manual/processing_algs/qgis/networkanalysis.html)

---
## 🎯Learning Objectives
  
- **Apply network analysis tools to model spatial movement**
- **Compare distance and time routing strategies in QGIS**
- **Critically evaluate cartographic visualization of network outputs**

---
## Data  

For access to the data follow this link: [Network_Analysis](https://drive.google.com/drive/folders/13WLpeKqzRLIn5P_BFIgyD9MovJgBhDVM?usp=sharing)

The folder `NetworkAnalysis_Data` contains two shapefiles:  
- `graz_districs_31287.shp`: 17 districts of Graz  
- `roads_31287.shp`: road network 

Additionally, a `max_speed_style` file that helps you see speed limits. 

The coordinate reference system (CRS) used for the layers is `EPSG:31287 - MGI / Austria Lambert`.

---
## Steps

1️⃣ **Launch QGIS**
- Launch QGIS  
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab04_<YourName>`
  
2️⃣ **Add Layers**   
From `Layer Menu`, add the following vector layers:
- Add road network 
- Add district polygon
- Add OSM basemap by selecting `Web` > `QuickMapServices` > `OSM` > `OSM Standard`

3️⃣ **Create two point layers (student home and department)**
- `Layer` > `Create Layer` > `New Shapefile Layer`
- Set geometry to `Point`, CRS to `EPSG:31287` and file encoding to `UTF-8`
- Name your layer (`start_point`, `end_point`)
- Toggle editing mode, then use `Add Point Feature` to mark your home and the Geography Department
- Once points are added save edits and check both points are close to the road network

4️⃣ **Run Network analysis**

**Shortest path (distance)**
- Open the `Processing Toolbox` and type `Network analysis`
  - Firstly, select the `Shortest path (point to point)`
  - Select the roads layer and check that the coordinate system is the `EPSG:31287`
  - For the path type to calculate, select `Shortest`
  - Set the `Start Point` to be your home by clicking `...` and the `End Point` to be the Department of Geography
  - In the `Advanced Parameters`, select `oneway` for the `Direction Field`
  - `Value for forward direction` set `F`
  - `Value for backward direction` set `T`
  - `Value for both directions` set `B`
  - Run the tool
  - Inspect the result and adjust the symbology 

> [!tip]
> Enable the snapping tool from the `Toolbar` to select your start and end points. Right-click and select `Snapping Toolbar`

**Fastest path (time)**
- Load the `max_speed_style` layer by selecting the `roads_31287` layer. Right click `Properties` > `Symbology` > `Style` > `Load Style`
- As before, open the `Processing Toolbox` and type `Network analysis`
  - Repeat `Shortest path (point to point)`
  - Select the roads layer and check that the coordinate system is the `EPSG:31287`
  - For the path type to calculate, select `Fastest`
  - Keep the same start & end points from the previous step
  - In the `Advanced Parameters`, select `oneway` for the `Direction Field`
  - `Value for forward direction` set `F`
  - `Value for backward direction` set `T`
  - `Value for both directions` set `B`
  - For `Speed field` select `maxspeed`
  - Test which value for the `Topology Tolerance` works best for your route. Start from 0 and increase if necessary. The tested route worked with 8 meters of tolerance
  - Run the tool
  - Inspect the result and adjust the symbology 

> ❓**Question:** Click to see the answer    
<details>
  <summary>What are the "cost" units created after running the tool?</summary>
  
  They are calculations of distance in meters for the shortest path, and estimated travel time in hours for the fastest path. 
  </details>

5️⃣ **Create a Map Layout for Presentation**  
- Save both route outputs 
- Open the **Print Layout** with **Project > New Print Layout**  
- Give your layout a name like `Network_Analysis_Map`  
- In the layout window, add your map with **Add Map** tool and draw a rectangle for it  
- Use the **Add Label** tool to add a big, clear title like *“Network Paths”*  
- Add a legend, scale bar and north arrow
  
6️⃣ **Export Your Map**  
- Once happy with the layout, export your map as an image:  
  - Click **Layout > Export as Image**  
  - Save the file in your project folder

---
## 🚀Independently
- **Run the above network analysis tasks. Report the cost value and its units for each calculation, together with the topology tolerance used. Calculate the length of both routes in kilometres. Which route is shorter, and by how much? Convert the fastest route’s estimated travel time to minutes.**
- **Write a brief report with your findings and discuss whether your routes are plausible. Identify limitations of the network data and speed assumptions.**
- **Save your results into a PDF file (include text and screenshots from your steps) and send it by email till next week.**

---
## Data Source

- Geofabrik Download Server ([Data source](https://download.geofabrik.de/))  
- OpenStreetMap ([Data source](https://www.openstreetmap.org/#map=17/50.030136/14.526469&layers=S/))  

