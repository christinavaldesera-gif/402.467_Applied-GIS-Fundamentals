# Lab_01: QGIS Basics ~ Reproducing John Snow's Mapping Method  

## Introduction  

In the Soho district of London in 1854, a [Cholera outbreak occurred](https://en.wikipedia.org/wiki/1846%E2%80%931860_cholera_pandemic). Dr. John Snow challenged the common belief that the disease spread through the air. He mapped cholera cases and water pumps, showing that one pump was the source of the contamination. This work laid the groundwork for modern spatial epidemiology and GIS. The aim of this lab is to recreate Snow’s mapping technique using current basemaps to study the outbreak.

---
## 🎯Learning Objectives
  
- **Understand historical context of disease mapping**
- **Load vector data & apply basic symbology**
- **Create simple thematic maps with layouts**
- **Reflect on spatial patterns and perform basic spatial analysis**

---
## Data  

For access to the data follow this link: [SnowGIS_Data](https://drive.google.com/drive/folders/1N4wrFSpLlSWzj4WdFuFx8zFMOaKnOKkK?usp=sharing)

The folder `SnowGIS_Data` contains three shapefiles:  
- `Cholera_Deaths.shp`: locations and number of cholera cases  
- `Pumps.shp`: locations of water pumps  
- `City_Blocks.shp`: polygons of city blocks with aggregated case counts within each block  

Additionally, ready-made basemaps of the study area are included: `OSMap`, `OSMap_Grayscale`.  

The coordinate reference system (CRS) used for the layers is “WGS_1984_UTM_Zone_30N” (EPSG:32630).  

---
## Steps

1️⃣ **Launch QGIS**
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Then, get familiar with the interface
   
2️⃣ **Import Data Layers**
- Go to `Main menu` > `Layer` > `Add Layer` > `Add Vector Layer` and navigate in your folder by selecting the `...`. You can select multiple layers at once

3️⃣ **Inspect Your Data**
- Open `Attribute Table`. Right click on each layer in the `Layers Panel` and select `Open Attribute Table`
> [!tip]
> Shortcut to the `Attribute Table`
> select the layer and press `F6`

- View `Layer Properties`. Right click on each layer and choose `Properties`. Review information such as CRS, symbology and metadata
- Use the `Identify Features` tool. Click on individual features to see their attributes

4️⃣ **Apply Symbology**
- For `Pumps`:
  - On the `Layers panel` right-click on the Pumps layer > `Properties` > `Symbology`. Choose Single Symbol from the drop down menu at the top. Set a uniform symbol for the pumps, adjust the size to make it more visible. Click `Apply` and `OK` to see your changes
- For `Cholera_Deaths`:
  - Go to `Symbology` tab as mentioned above and choose Graduated this time. Then, choose Count as the value, select a Symbol, the Color and the Size of your preference and press Classify. For Mode you can leave the default option. Click `Apply` and `OK` to see your changes

> ❓**Question:** Click to see the answer    
<details>
  <summary>Why use graduated symbols here?</summary>
  
  Graduated symbols show the different numbers of cholera cases at each location. This helps you find clusters with higher case counts, which might suggest closeness to a contaminated source. 
  </details>

- For `City_Blocks`:
  - `Properties` > `Symbology` > Graduated. Set value to the deaths field, classify with a yellow-to red ramp choropleth effect. `Apply` and `OK`

5️⃣ **Create Maps**   
- Customize your results. Go to `Project` > `New Print Layout` and add a title. Select the `Add Map` icon and drag a rectangle on the canvas. Also `Add Legend`, `Add Scale Bar` and `Add North Arrow`. `Add Label` for title, your name and student number

6️⃣ **Export Maps**
- Once satisfied with your map, export via `Layout` > `Export as Image/PDF`

---
## 🚀Independently
Create two separate map compositions:  

   - **Map 1:** Show pump locations using a uniform symbol and represent cholera cases with proportional circular symbols scaled by the number of cases at each location.  
   
   - **Map 2:** Use color gradation to symbolize the polygons of city blocks according to the number of cholera cases within their boundaries.

Both maps must include your full name, student number, map scale, legend, title  

Each map should include a basemap. You may use any of the static maps provided in the data folder or a dynamic basemap of your choice, exploring the OpenLayers Plugin or HCMGIS extensions in QGIS. Export the final two maps as PDF files. Compress them into one archive and send them by email.

---
## Data Source

GeoDa Data and Lab ([https://geodacenter.github.io/](https://geodacenter.github.io/))
