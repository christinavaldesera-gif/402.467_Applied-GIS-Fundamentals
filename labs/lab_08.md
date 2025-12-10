# Lab 08: Supervised Image Classification in QGIS using SCP

## 🎯Learning Objectives

- **Use the Semi-Automatic Classification Plugin (SCP) for supervised image classification**
- **Classify Sentinel-2 tiles for Graz, Austria**
- **Export a classified land cover raster of Graz with 4 land cover classes**

You can find the SCP documentation [here](https://semiautomaticclassificationmanual.readthedocs.io/en/latest/)

---
## Classification in Remote Sensing

In Remote Sensing, **Classification** involves categorizing pixels in an image into predefined classes based on their spectral characteristics. Each spectral band captures specific information about the Earth's surface. By analyzing these bands, we can distinguish between different land cover types. For instance, vegetation strongly reflects in the **Near-Infrared (NIR)** band, while water bodies absorb most visible light and reflect little in the NIR. By examining reflectance values across multiple bands, we classify pixels as vegetation, water, soil, etc.

---
## Data

Please download the data from the folder matching the last digit of your matriculation number (student number). More specifically:

- If your student number ends in 1,3,5,7 or 9 --> download [here](https://drive.google.com/file/d/1qJII011McjpHnHtBcAlYdpyt6EnpUu-G/view?usp=sharing/)
- If your student number ends in 0,2,4,6, or 8 --> download [here](https://drive.google.com/file/d/1-x6Gn8HfTH5gCkF2-c1PofbIgj-t2wyF/view?usp=sharing/)


The image data used in this exercise is Sentinel-2 10m resolution imagery for Graz, Austria. Each student will work on a specific tile of the image with 8 spectral bands and dimensions approx. 3660×2196 pixels. SCP works by processing a band set. While individual band files can be loaded, they are typically combined into a single stacked raster by SCP for classification, as will be done in step 3. For this exercise, only 4 bands are used: **Band 2 (Blue), Band 3 (Green), Band 4 (Red) and Band 8 (Near Infrared)**, which support further index analyses. For more information about Sentinel-2 spectral bands, click [here](https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/bands/).

---
## Steps

1️⃣ **Install SCP Plugin**
- Open QGIS   
- Go to `Plugins` > `Manage and Install Plugins...`  
- Search for **Semi-Automatic Classification Plugin** and click `Install`

2️⃣ **Load Data**
- Load your image tile e.g.`tile_02`
- Right click and go to `Properties` > `Symbology`. For Render type select `Multiband color` and for Red band select `Band 3`, for Green band select `Band 2` and for Blue band select `Band 1`. Observe how your initial image changed. In Remote Sensing, this band combination is typically called a _Natural Color Composite_
- Load also the 4 individual band files directly into QGIS 

3️⃣ **Prepare the Band Set in SCP**
- Go to `SCP` plugin from the `Main Menu` and select `Band set`
- In the `Band Set ` window:  
   - Click the `Add bands loaded in QGIS` button  
   - Select Bands 2, 3, 4 and 8 for classification. Hold the `Ctrl` key to select multiple bands  
   - Click `OK` to add these bands to the band set  
   - Confirm the bands are in the correct order: `Blue (2)`, `Green (3)`, `Red (4)`, `Near Infrared (8)`  
   - In the  `Band quick settings ` menu at the  `Wavelength ` field, select the `Sentinel-2` option from the dropdown to assign accurate central wavelengths  
   - Check the box `Create raster of band set (stack bands)`  
   - Press `Run`. A dialog will prompt you to select a directory and filename for the stacked raster. Choose a location and save  
   - The stacked raster will be created and saved in your selected folder
   - Click `Close` to apply these settings and close the band set window   

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why is it important to correctly prepare and order your band set before classification?</summary>
  Proper band stacking and ordering ensure that spectral data corresponds correctly to each band, which is essential for accurate classification results.
</details>

4️⃣ **Create Training Input (ROIs)**

In SCP, supervised classification requires training data in the form of **ROIs (Regions of Interest)** polygons drawn on the satellite imagery that represent known land cover classes.
- ROIs are also called *training polygons* because they provide spatial samples used to train the classifier  
- Each ROI stores polygon geometry plus spectral information from the pixels within  
- To achieve good classification results, digitize multiple ROIs per class to capture spectral variability
- We will create a classification with the classes below:

| Macroclass name | Macroclass ID |
|-----------------|---------------|
| Water           | 1             |
| Buildings       | 2             |
| Vegetation      | 3             |
| Bare Soil       | 4             |

**Steps to create ROIs:**  
- In the plugin `Training input` window, select to `Create a new training input`. Name it `training.scpx` in your directory
- In the `Layers panel` place the new layer on top
- Click the `Create a ROI polygon` button
- Place vertices on a polygon to create a ROI. Left click to create vertices and right click to complete the polygon
- Name the ROI after the land cover class it represents (e.g., "Water", "Vegetation", etc.)  
- Choose a distinct color for each class to help visualization  
- Draw **at least 7–10 polygons per class**, spaced across your tile to capture variability  
- Save your ROIs regularly using the `Save ROI` button, which creates a `.scpx` file for reuse  

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why is it important to create multiple and representative ROIs for each land cover class?</summary>
  Because they capture the spectral diversity within each class, enabling the classifier to learn the variability and reduce misclassification.
</details>

5️⃣ **Classification Preview**
- Go to the `Classification` tab in SCP  
- Select a classification algorithm. Use `Minimum Distance`   
- Click the `Preview` button  
- Examine the preview map classes are colored as per your ROIs  
   - If classes appear mixed or incorrect, improve your ROIs and repeat the preview  

When you are satisfied, proceed to the full classification step.

> ❓**Question:** Click to see the answer  
<details>
  <summary>What insights can the classification preview provide about your training data?</summary>
  The preview shows if classes are well separated or overlapping, helping identify if the ROIs are effective or need refinement.
</details>

6️⃣ **Run Full Classification and Save Results**
- In the SCP Dock, under `Classification`, click the `Classify` button to run classification on the full tile  
- When prompted, choose a location and filename to save the classified raster (e.g., `tile_02_classified.tif`)  
- Wait for the process to finish (may take several minutes depending on data size and computer)  
- After completion, the classified raster will be automatically added to your Layers panel  
- You can style the classified image by right clicking the layer > `Properties` > `Symbology` and assigning colors to each class

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why should you visually inspect the classified map after running classification?</summary>
  Visual inspection helps detect misclassifications or errors, guiding further refinement of ROIs or parameters.
</details>

7️⃣ **Analyze and Export Your Results**
- Visually inspect the classified map to verify class assignments  
- If needed, refine your ROIs (add or adjust polygons) and rerun classification to improve accuracy  
- When satisfied, export the classified raster: right-click layer > `Export` > `Save As...`. Save as GeoTIFF or preferred format  
- Optionally, use QGIS Print Layout to create maps and reports for assignment submission

> ❓**Question:** Click to see the answer  
<details>
  <summary>What criteria can you use to assess the quality of your classification?</summary>
  Compare with known land cover, spectral signature consistency, spatial patterns and accuracy metrics if reference data are available.
</details>

---
## Data Source

[Copernicus Dataspace](https://browser.dataspace.copernicus.eu/?zoom=5&lat=50.16282&lng=20.78613&themeId=DEFAULT-THEME&visualizationUrl=U2FsdGVkX1%2BUq4RcOfRKcSZKY29ODsLIuV7%2BMnYCOgOf7DIZu6ubnPyMlqEwc4z1bDA6ZY9l5H%2BPM7o2QG7iG0nOFiZM000mS75Re1FwMrcmVnTw8kZWOWZJGded1XNW&datasetId=S2_L2A_CDAS&demSource3D=%22MAPZEN%22&cloudCoverage=30&dateMode=SINGLE)  
