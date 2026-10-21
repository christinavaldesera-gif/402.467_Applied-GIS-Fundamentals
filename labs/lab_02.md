# Lab 02: Georeferencing a Historical Map

## Georeferencing

Georeferencing links positions in a digital image to coordinates in a known coordinate reference system (CRS). In this lab, you will match identifiable features on a historical map of Villach with their corresponding locations on a modern reference map. You will then assess how well the georeferenced historical map aligns with that reference. Georeferencing establishes the image's geographic placement, but does not guarantee that every feature is accurately located.

---
## 🎯Learning Objectives

- **Understand the importance of georeferencing**
- **Select and justify appropriate ground control points**
- **Reflect on limitations and potential sources of error**

---
## Information of the Map 🗺️

- **Description:** Franziszeischer Kataster — Historical map of Villach, Austria
- **Date:** ~1800s
- **Original GeoTIFF pixel size:** approximately 0.5 x 0.5 meters. The teaching TIFF has had its georeferencing removed
- **Target Coordinate Reference System:** EPSG:31258 (MGI / Austria GK M31 - Projected)
- **Dimensions:** 18,461 × 9,753 pixels
- **File Size:** approximately 317 MB

---
## Data

**Historical map of Villach** [Click here for access to the map](https://drive.google.com/file/d/1h7ER-mQyQetVwPDBGWIudmp3zsWFSkBd/view?usp=drive_link)

The link contains a Franziszeischer_Kataster.tif file (a clipped extract of the historical Franziszeischer Kataster, focusing on the Villach area)

---
## Steps

1️⃣ **Launch QGIS**   
- Launch QGIS  
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab02_<YourName>`

2️⃣ **Install Required Plugins**
- Go to `Plugins` > `Manage and Install Plugins...`
- In the search bar, type **OSM Place Search**. Select the plugin and click install plugin
- Search for **QuickMapServices** and install plugin. The plugin can be found in `Web` in the `Main menu`. The **QuickMapServices** plugin offers a variety of basemaps including multiple OSM styles, satellite imagery and other web map layers  
- Close the Plugins dialog when done

> [!TIP]
> If you don’t see a wide variety of basemap options in QuickMapServices, don’t worry!  
> - Go to `Web` > **QuickMapServices** > **Settings**  
> - Open the **More services** (or Contributed Services) tab  
> - Click **Get contributed pack** to download and add many additional basemaps  
> - After that, close the settings and reopen the QuickMapServices menu to discover many more map styles and layers to choose from

3️⃣ **Set Project CRS**
- In the main QGIS window, locate the **CRS status button** at the bottom-right corner (showing the current EPSG code). Click it to open the Project Properties CRS dialog
- For spatial work in Villach, Austria, choose a CRS commonly used for Austria: `EPSG:31258 (MGI / Austria GK M31)`
- Confirm your selection

4️⃣ **Load OSM Basemap**  
- In the Menubar, find `Web` > `QuickMapServices`> `OSM`> `OSM Standard`. This basemap will serve as a reference for placing accurate Ground Control Points (GCPs)
- Also, open the **OSM Place Search** panel and search for **Villach, Austria**. Double-click the appropriate result to zoom to the study area
- When selecting GCPs in the next step, you can also search for named landmarks to help locate potential matching features

5️⃣ **Load the Historical Map & Add Ground Control Points**  
- Go to `Layer` > `Georeferencer`
- In the Georeferencer window, select `File` > `Open Raster` and open your historical map image
- Use the `Add GCP Point` tool to begin placing Ground Control Points (GCPs)
- Zoom in & identify a precise point visible on both maps, e.g. a road intersection. Click this point on the historical map
- In the coordinate dialog, click `From Map Canvas`, then click the corresponding point on the OSM basemap and confirm the coordinates
- Repeat this process to add at least 5 GCPs spread across the map, including its outer parts and interior
- The GCPs and their details will appear in a table at the bottom of the Georeferencer window

> [!tip]
> Landmarks & street intersections are a good place to start, especially those that have remained stable over time!

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why is it important to distribute GCPs evenly across the map area rather than clustering them in one spot?</summary>
  
  Even distribution helps the transformation model better correct distortions across the entire map rather than just locally.
</details>

6️⃣ **Start Georeferencing**
- When you feel confident with your GCPs, click the `Transformation Settings` button
- The transformation settings will open. Select the following options:  

| Setting                         | Value                                         |
|--------------------------------|-----------------------------------------------|
| Transformation type            | Polynomial 1                                 |
| Resampling method              | Cubic                                       |
| Target SRS                    | EPSG:31258                         |
| Output Raster                 | Save somewhere you will remember with a unique ID |
| Compression                  | LZW                                         |
| Use 0 for transparency when needed | Unchecked                                |
| Save GCP points               | Checked                                     |
| Load in QGIS when done        | Checked                                     |

- Click the green `Start Georeferencing` button. A progress bar will appear
- The new file will be added to the QGIS document. Look at it closely to make sure everything is lining up properly

7️⃣ **Review GCP Residuals**  
- Inspect the `Residual` column in the GCP table. Check the displayed units: pixels or map units
- Recheck points with unusually large residuals against both maps. Correct misplaced points or replace unreliable matches
- If you change any GCPs, run georeferencing again and use the updated output for the visual assessment

8️⃣ **Load, Visualize & Assess the Georeferenced Map**  
- Use transparency controls to overlay the georeferenced historical map on the basemap  
- Compare several stable features that were not used as GCPs, including features near the map edges. Identify areas of good and poor alignment

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why is it important to review the georeferenced raster after the process completes?</summary>
  
  To verify that the map aligns well with the basemap and to ensure no large distortions remain after georeferencing.
</details>

9️⃣ **Save and Close the Georeferencing Process**
- Save the GCP list using `File` > `Save GCP points as...`
- Close the Georeferencer window
- Save your QGIS project (`Project` > `Save`)

---
## 🚀Independently

- With Polynomial 1, compare results using different numbers of GCPs. Assess alignment at features not used as GCPs.
- Compare Polynomial 1 and Polynomial 2 using the same 8–10 GCPs. Save each output separately.
- In a short report, briefly explain how changing the number of GCPs & the transformation type affected your results, supported by screenshots.

## Data Sources

- Map acquired from: ([**KAGIS – Franziszeischer Kataster**/](https://gis.ktn.gv.at/webgisviewer/atlas-mobile/map/Basiskarten/Franziszeischer%20Kataster))

- Georeferencing: [USGS](https://www.usgs.gov/faqs/what-does-georeferenced-mean)

## GIS report

- UNBC’s GIS report structure guide: [Guide](https://gis.unbc.ca/geog204/geog-204-project-layout)
- GIS report template: [Word file to download](https://gsp.humboldt.edu/olm/Courses/GSP_510/00%20Introduction/Lab/Overview.html)