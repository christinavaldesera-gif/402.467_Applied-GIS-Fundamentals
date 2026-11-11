# Lab 05: Raster Data ~ Park Suitability Analysis in NYC

## 🎯Learning Objectives

- **Load and explore raster data in QGIS**
- **Reclassify rasters into numerical suitability scores**
- **Combine raster calculations and thematic mapping**
- **Combine & weight rasters using overlay analysis**

---
## Data

For this exercise you will be working on New York and specifically on your assigned borough. The initial data has been pre-processed and downsampled according to the lab's needs. Following the links below, each team will find their layers reprojected to EPSG:2263 coordinate system and their corresponding DEM and land cover datasets clipped for each different borough.
  
Please download the ZIP file for your assigned borough from the links below:  

- [Download Manhattan Dataset](https://drive.google.com/file/d/1tm-sVxn5UE-EC1keHLC1oQ1mgSLXZP7J/view?usp=sharing)  
- [Download Brooklyn Dataset](https://drive.google.com/file/d/1catf2spkEva0ufdZKTNHtsEmz9JSS0mc/view?usp=sharing)  
- [Download Queens Dataset](https://drive.google.com/file/d/1WduH2LnQiQe9CYR5VCW_OyW1_hGqLQLe/view?usp=sharing)  
- [Download The Bronx Dataset](https://drive.google.com/file/d/1BljNac5l0kJKA5Nl3vRsjr7UhEtxXw2N/view?usp=sharing) 
- [Download Staten Island Dataset](https://drive.google.com/file/d/1FsprWtQhTXvf1-IIz_Od9x4kQkxCoEqm/view?usp=sharing)

---
## Steps

1️⃣ **Prepare Your Workspace and Load Data**
- Open QGIS
- Load your data including the DEM raster file, the land cover raster layer and your selected borough

2️⃣ **Calculate Slope Raster from DEM**
- Select your DEM layer
- Go to `Raster` > `Analysis` > `Slope`
- Input your loaded DEM raster
- Save the slope raster in your working directory and give it a name 
- Right click on the produced slope layer and go to `Properties` > `Symbology`
- Select `Singleband pseudocolor` for `Render Type`. Choose from the `Color ramp` a `RdYlGn` representation for the highest slope to be in red colour
- Press `Apply` and `OK`

> ❓**Question:** Click to see the answer    
<details>
  <summary>How does slope works?</summary>
  
  The slope tool identifies the steepness at each cell of a raster surface. The lower the slope value, the flatter the terrain; the higher the slope value, the steeper the terrain (ArcGIS Pro documentation).
  </details>

3️⃣ **Land Cover**
- Select your land_cover_2017 layer
- Right click and go to `Properties`
- Select `Symbology`. For `Render Type` select `Paletted/Unique values`
- Press `Classify`. You should be able to see the eight land cover classes mapped
- Set the symbology to the different classes according to the data's source. Find the dataset's land cover classes here --> [Land cover raster data](https://data.cityofnewyork.us/Environment/Land-Cover-Raster-Data-2017-6in-Resolution/he6d-2qns/about_data) 
- Select `Apply` and `OK`

> [!IMPORTANT]  
> Take a look at the produced slope layer and assess your borough. In which locations can you find steeper slopes? Are the steepest slopes near the coast, inland, or scattered?

4️⃣ **Reclassify Slope Raster into Suitability Scores**
- Select the created slope layer
- Open the `Processing Toolbox` and search for `Reclassify by table`
- Input raster: your slope raster (e.g.`boroughname_slope`). Open the reclassification table by selecting the `...`. In the following suitability criteria, a higher value means more suitable for a park and a lower value means less suitable for a park:

| Min          | Max          | Value (suitability score) |
|--------------|--------------|---------------------------|
| 0.0          | 5.0          | 4                         |
| 5.0          | 10.0         | 3                         |
| 10.0         | 15.0         | 2                         |
| 15.0         | 99999.0      | 1                         |

- Choose an output raster name, e.g. `boroughname_slope_reclassify` and save it as a .tif file. Check the `Use NoData when no range matches value` if necessary and select `Int32` as `Output data type `
- Click `Run`
- Right click on the created layer to check the `Symbology`. Select `Paletted/Unique values` and `Classify`. This ensures that each suitability value (1,2,3,4) gets its own solid color. Make sure that red is assigned to a value with 1 score (meaning unsuitable) and green is assigned to a value with 4 score (highly suitable). 

 > ❓**Question:** Click to see the answer    
<details>
  <summary>Why was it necessary to reclassify the original continuous slope data (degrees) into these distinct categories (1, 2, 3, 4) for our park suitability analysis? What did this step achieve that simply using the raw slope values wouldn't?</summary>  

 Reclassification was necessary to convert a continuous, complex range of slope values into a simpler, standardized set of categories or scores. This allows us to assign a clear 'suitability' level to each slope range.
 </details>

 5️⃣ **Reclassify Land Cover Raster into Suitability Scores**
- Open the `Processing Toolbox` and search for `Reclassify by table`
- Input raster: your land cover raster (e.g.`boroughname_land_cover_2017`). Open the reclassification table and create one row per land cover class code. See the table below:

| Min          | Max          | Value (suitability score) |
|--------------|--------------|---------------------------|
| 1            | 1            | 4                         |
| 2            | 2            | 4                         |
| 3            | 3            | 3                         |
| 4            | 4            | 1                         |
| 5            | 5            | 1                         |
| 6            | 6            | 1                         |
| 7            | 7            | 2                         |
| 8            | 8            | 1                         |

- Choose an output raster name, e.g. `boroughname_lc_reclassify`. Select `Int32` as `Ouput data type ` and save it as a .tif file
- Click `Run`
- Right click on the created layer to check the `Symbology`. Select `Paletted/Unique values` and `Classify`. Assign colors corresponding to your suitability scheme. Use red to green color to represent unsuitable and suitable land cover classes according to the score you assigned above.

6️⃣ **Generate a Combined Park Suitability Map**
- Open `Raster` > `Raster Calculator`
- Build this expression: 

("boroughname_lc_reclassify@1" * 0.6) + ("boroughname_slope_reclassify@1" * 0.4)

- Name the output raster e.g. `boroughname_park_suitability`. Save it as a .tif file

> ❓**Question:** Click to see the answer    
<details>
  <summary>What do 0.6 and 0.4 represent? </summary>  

 Assigning 0.6 to land cover and 0.4 to slope in a raster calculation means you are giving 60% importance (weight) to land cover suitability and 40% importance (weight) to slope suitability in the final combined park suitability score.
 </details>

7️⃣ **Symbolize & Interpret the Final Suitability Raster**
- Right click on the final raster > `Properties` > `Symbology` > `Singleband pseudocolor` 
- Choose the `RdYlGn` color ramp. Red means low suitability, yellow moderate and green high suitability

8️⃣ **Create Final Map Layout**
- Add the borough boundary vector as border/outline
- Open `New Print Layout`
- Make sure to add a title (e.g. `Park Suitability Map — Boroughname `), a legend (with suitability ramp), north arrow and scale bar
- Add your names too
- Export the map as pdf or png file

---
## 🚀 Independently
- Identify your top three most suitable areas for a new park in your borough, explaining what specific slope and land cover characteristics make them highly suitable according to your map. Check your results by loading a basemap such as Google Satellite. See if parks already exist in the areas you identified. Using your analysis, suggest new areas, where parks are not present.
- Describe two limitations of this simplified park suitability model for a city like NYC and suggest two additional data layers that would improve its realism.
- How could your final suitability map be used as a preliminary tool by city planners and what crucial factors (e.g. population density or land ownership) would still need consideration before any park development?
- Write a short GIS report. Remember to include your answers to the questions, your final map and screenshots of your main QGIS steps.

---
## Data Source

NYC OpenData ([https://opendata.cityofnewyork.us/](https://opendata.cityofnewyork.us/)) 