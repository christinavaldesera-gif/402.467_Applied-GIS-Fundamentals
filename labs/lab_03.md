# Lab_03: Handling Vector Data ~ Network Analysis

## Introduction  

Network analysis in QGIS uses spatial data to model networks, such as roads or pathways. This allows for the calculation of routes and accessibility. It helps identify the best paths between locations by considering factors like distances and speed limits. This functionality supports transportation planning, navigation and solving geographic problems in urban areas. Check QGIS official documentation [QGIS network analysis documentation](https://docs.qgis.org/3.40/en/docs/user_manual/processing_algs/qgis/networkanalysis.html)

---
## 🎯Learning Objectives
  
- **Apply network analysis tools to model spatial movement**
- **Differentiate between the shortest and fastest path algorithms in QGIS**
- **Critically evaluate cartographic visualization of network outputs**

---
## Data  

For access to the data follow this link: [Network_Analysis](https://drive.google.com/drive/folders/13WLpeKqzRLIn5P_BFIgyD9MovJgBhDVM?usp=sharing)

The folder `NetworkAnalysis_Data` contains two shapefiles:  
- `graz_districs_31287.shp`: 17 districts of Graz  
- `roads_31287.shp`: road network 

Additionally, a `max_speed_style` layer.  

The coordinate reference system (CRS) used for the layers is `EPSG:31287 - MGI / Austria Lambert`.

---
## Steps

1️⃣ **Launch QGIS**
- Launch QGIS  
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab03_<YourName>`
  
2️⃣ **Add Layers**
From `Layer Menu`, add the following vector layers:
- Add road network 
- Add district polygon
- Add OSM basemap

3️⃣ **Create two point layers**
- Start point, the place where you live
- End point, the Department of Geography
- Create a .shp for each point 
- Add fields `x_coord` and `y_coord` to each point layer accordingly, using knowledge from Lab_02 
- Zoom into the area, check the road network is connected and the start/end points lie close to the network

4️⃣ **Run Network analysis**

**Shortest path (by foot)**
- Open the `Processing Toolbox` and type `Network analysis`
  - Firstly, select the `shortest path (point to point)
  - Select the roads layer and check that the coordinate system is the `EPSG:31287`
  - For the path type to calculate, select `Shortest`
  - Set the `Start Point` to be the place where you currently live in Graz and the `End Point` to be the university and specifically the Deparment of Geography
  - Set `Default Speed` as 5 km/h and leave everything else to default
  - Run the tool
  - Inspect the result and adjust the symbology 

> [!tip]
> Enable the snapping tool from the `toolbar` to select your start and end points. Right-click and select `Snapping Toolbar`

**Fastest path (by car)**
- As before, open the `Processing Toolbox` and type `Network analysis`
  - Select the `shortest path (point to point)`
  - Select the roads layer and check that the coordinate system is the `EPSG:31287`
  - For the path type to calculate, select `Fastest`
  - Keep the same start & end points from the previous step
  - In the `Advanced Parameters`, select `oneway` for the `Direction Field`
  - `Value for forward direction` set `F`
  - `Value for backward direction` set `T`
  - `Value for both directions` set `B`
  - For `Speed field` set the `maxspeed` and set the speed at 50 km/h
  - Set the `Topology Tolerance` to a value of `1 meter`
  - Run the tool
  - Inspect the result and adjust the symbology 

> ❓**Question:** Click to see the answer    
<details>
  <summary>Did the fastest and shortest routes follow the same path?</summary>
  
  Often, they are different because speed limits and road types affect the fastest route. 
  </details>

5️⃣ **Create a Map Layout for Presentation**  
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
- **Run the above network analysis tasks and try to experiment by running network analysis for the fastest route between your points filtering the roads for cycling**
- **Write a brief report to explain how network analysis adapts to different travel modes (foot, using the car, cycling) and realistic speeds for your case**
- **Save your results into a PDF file (text and screenshots) and send it by email till next week**

Examples to get familiar with writing your own GIS reports:
- [Geog 204 Project Layout](https://gis.unbc.ca/geog204/geog-204-project-layout/)
- [Introductory level GIS Projects](https://cdn.serc.carleton.edu/files/NAGTWorkshops/gis10/introductory_level_gis_project.pdf?)
