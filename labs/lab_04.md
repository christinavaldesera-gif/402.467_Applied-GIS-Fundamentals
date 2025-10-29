# Lab 04: Georeferencing a Historical Map

## Georeferencing

Georeferencing means that the internal coordinate system of a digital map or aerial photo can be related to a ground system of geographic coordinates. A georeferenced digital map or image has been tied to a known Earth coordinate system, so users can determine where every point on the map or aerial photo is located on the Earth's surface. [USGS](https://www.usgs.gov/faqs/what-does-georeferenced-mean)

---
## 🎯Learning Objectives

- **Understand the importance of georeferencing**
- **Identify and select appropriate ground control points**
- **Reflect on limitations and potential sources of error**

---
## Information of the map 🗺️

- Description: Austria-Hungary, 11th edition, 1911, E058. Austria-Hungary with Excursions to Cetinje, Belgrade and Bucharest
- Date: 1911
- Source: Austria-Hungary by Baedeker 1911
- Author: Karl Baedeker (1801–1859)
- Dimensions: 1,520 × 2,000 (5.69 MB)
- Format: JPEG

---
## Data

Historical map of Graz [Click here for access to the map](https://drive.google.com/file/d/1Z3n0FN0VRolJx1LpgxuvXNVFrhgPG81_/view?usp=sharing)

---
## Steps

1️⃣ **Launch QGIS**   
- Launch QGIS  
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab04_<YourName>`

2️⃣ **Install Required Plugins**
- Go to `Plugins` > `Manage and Install Plugins...`
- In the search bar, type **Georeferencer**
- If **Georeferencer GDAL** is not already installed, select it and click **Install Plugin**
- In the search bar, type **OSM Place Search**. Select and download the plugin
- Close the Plugins dialog when done

3️⃣ **Set Project CRS**
- In the main QGIS window, locate the **CRS status button** at the bottom-right corner (showing the current EPSG code). Click it to open the Project Properties CRS dialog
- For spatial work in Graz, Austria, choose a CRS commonly used for Austria: `ETRS89 / UTM zone 33N (EPSG:25833)`
- Confirm your selection

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why do you think setting the correct CRS is important before adding data?</summary>
  
  Setting the CRS ensures that all spatial data align correctly and geometric measurements are accurate.
</details>

4️⃣ **Load OSM Basemap**  
- In the Menubar, find `Web` > `QuickMapServices`> `OSM`> `OSM Standard`. This basemap will serve as a reference for placing accurate Ground Control Points (GCPs)

5️⃣ **Load the Historical Map & Add Ground Control Points**  
- Go to `Layer` > `Georeferencer`
- In the Georeferencer window, select `File` > `Open Raster` and open your historical map image
- Use the `Add GCP Point` tool to begin placing Ground Control Points (GCPs)
- Click on a recognizable feature in the historical map in the top pane
- When prompted, using the `From Map Canvas`, add the coordinates using the basemap as a reference 
- Repeat this process to add at least 5 GCPs, distributed evenly across the map area for maximum accuracy
- The GCPs and their details will appear in a table at the bottom of the Georeferencer window

> [!tip]
> Landmarks & street intersections are a good place to start, especially those that have remained stable over time!

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why is it important to distribute GCPs evenly across the map area rather than clustering them in one spot?</summary>
  
  Even distribution helps the transformation model better correct distortions across the entire map rather than just locally.
</details>

6️⃣ **Check RMSE (Root Mean Square Error)**  
- After GCP entry, review the RMSE value in the GCP table at the bottom
- **Analytical tip:**  
   - Lower RMSE values indicate better accuracy
   - Examine residuals for each GCP. Adjust or remove points with unusually high errors to achieve lower overall RMSE

> [!IMPORTANT]  
> The pixel size defines the ground area represented by each raster pixel, in meters for your CRS. Aim for an RMSE less than or about half the pixel size to ensure accurate georeferencing.

> ❓**Question:** Click to see the answer    
<details>
  <summary>What is RMSE?</summary>
  
  RMSE measures how closely your control points match real locations; smaller values are better.
</details>

7️⃣ **Start Georeferencing**
- When you feel confident with your GCPs, click the `Transformation Settings` button
- The transformation settings will open. Select the following options:  

| Setting                         | Value                                         |
|--------------------------------|-----------------------------------------------|
| Transformation type            | Polynomial 1                                 |
| Resampling method              | Cubic                                       |
| Target SRS                    | EPSG:25833                         |
| Output Raster                 | Save somewhere you will remember with a unique ID |
| Compression                  | LZW                                         |
| Use 0 for transparency when needed | Checked                                |
| Save GCP points               | Checked                                     |
| Load in QGIS when done        | Checked                                     |

- Click the green `Start Georeferencing` button. A progress bar will appear.
- The new file will be added to the QGIS document. Look at it closely to make sure everything is lining up properly.

> ❓**Question:** Click to see the answer  
<details>
  <summary>How might choosing different transformation types affect your georeferencing results?</summary>
  
  Different transformations handle distortions differently; higher-order polynomials can model more complex warping but may overfit if too many GCPs are not available.
</details>

8️⃣ **Load, Visualize & Assess the Georeferenced Map**  
- Use transparency controls to overlay the georeferenced historical map on the basemap  
- Visually check that features align and the spatial accuracy is acceptable

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why is it important to review the georeferenced raster after the process completes?</summary>
  
  To verify that the map aligns well with the basemap and to ensure no large distortions remain after georeferencing.
</details>

9️⃣ **Save and Close the Georeferencing Process**
- After completion, save your QGIS project (`Project` > `Save`)  
   - Close the Georeferencer window  
   - Save the GCP points list from the Georeferencer window (`File` > `Save GCP points as...`) for documentation or later reuse

---
## 🚀Independently

- Experiment with adding more or fewer GCPs and see how the RMSE and map accuracy change.
- Try different transformation types (Polynomial 2 or Thin Plate Spline) on your map. Observe how each transformation affects the alignment and distortion of the map features.
- Reflect in a short report about what are the benefits and limitations of georeferencing historical maps? How could inaccuracies impact analysis?