## Lab_01: QGIS Basics ~ Reproducing John Snow's Mapping Method  

---

### Introduction  

In the Soho district of London in 1854, a [Cholera outbreak occurred](https://en.wikipedia.org/wiki/1846%E2%80%931860_cholera_pandemic). Dr. John Snow challenged the common belief that the disease spread through the air by using a new method for the time. He gathered the addresses of the people who fell ill and marked locations on a map with symbols that reflected the number of cases. He also marked where local residents got their drinking water from various pumps. The connection between the city blocks, the number of cases and the pump locations pointed to one pump as the source of contamination. Although authorities initially rejected Snow's claims, it was later confirmed that the disease was spread through water, not air. John Snow laid the groundwork for modern spatial epidemiology and GIS. Many consider him the first to apply geographic analysis in epidemiology. The goal of this laboratory exercise is to reproduce John Snow’s mapping technique by combining the collected data with modern static and dynamic basemaps to study his findings.

---
### 🎯Learning Objectives
  
- **Understand historical context of disease mapping**
- **Load vector data & apply basic symbology**
- **Create simple thematic maps with layouts**
- **Reflect on spatial patterns and perform basic spatial analysis**

---
### Data  

For access to the data follow this link: [SnowGIS_Data](https://drive.google.com/drive/folders/1N4wrFSpLlSWzj4WdFuFx8zFMOaKnOKkK?usp=sharing)

The folder `SnowGIS_Data` contains three shapefiles:  
- `Cholera_Deaths.shp`: locations and number of cholera cases  
- `Pumps.shp`: locations of water pumps  
- `City_Blocks.shp`: polygons of city blocks with aggregated case counts within each block  

Additionally, ready-made basemaps of the study area are included: `OSMap`, `OSMap_Grayscale`.  

The coordinate reference system (CRS) used for the layers is “WGS_1984_UTM_Zone_30N” (EPSG:32630).  

---
### Steps

1️⃣ Launch QGIS
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Then, get familiar with the interface
2️⃣ Import Data Layers
- Go to `Main menu` > `Layer` > `Add Layer` > `Add Vector Layer` and navigate in your folder by selecting the `...`. You can select multiple layers at once
3️⃣ Inspect Your Data
- Open `Attribute Table`. Right click on each layer in the `Layers Panel` and select `Open Attribute Table`
> [!TIP]  Shortcut to the `Attribute Table` 
Select the layer and press `F6`
- View `Layer Properties`. Right click on each layer and choose `Properties`. Review information such as CRS, symbology and metadata.
- Use the `Identify Features` tool. Click on individual features to see their attributes.
4️⃣ Apply Symbology
For `Pumps`: On the `Layers panel` right-click on the Pumps layer > `Properties` > `Symbology`. Choose Single Symbol from the drop down menu at the top. Set a uniform symbol for the pumps, adjust the size to make it more visible. Click `Apply` and `OK` to see your changes.
For `Cholera_Deaths`: Go to `Symbology` tab as mentioned above and choose Graduated this time. Then, choose Count as the value, select a Symbol, the Color and the Size of your preference and press Classify. For Mode you can leave the default option. Click `Apply` and `OK` to see your changes.
For `City_Blocks`: `Properties` > `Symbology` > Graduated. Set value to the deaths field, classify with a yellow-to red ramp choropleth effect. `Apply` and `OK`.
5️⃣ Create and Explore Maps
Customize your results. Go to `Project` > `New Print Layout` and add a title. Select the `Add Map` icon and drag a rectangle on the canvas. Also `Add Legend`, `Add Scale Bar` and `Add North Arrow`. `Add Label` for title, your name and student number.
6️⃣ Once satisfied with your map, export via `Layout` > `Export as Image/PDF`

---
## 🚀Independently
Create two separate map compositions:  

   - **Map 1:** Show pump locations using a uniform symbol and represent cholera cases with proportional circular symbols scaled by the number of cases at each location.  
   
   - **Map 2:** Use color gradation to symbolize the polygons of city blocks according to the number of cholera cases within their boundaries.

Both maps must include:  
   - Your full name, student number 
   - Map scale, legend, title  

Each map should include a basemap. You may use any of the static maps provided in the data folder or a dynamic basemap of your choice, exploring the OpenLayers Plugin or HCMGIS extensions in QGIS.  

Export the final two maps as PDF files. Compress them into one archive and send them by email.


- Which pump do you think might have had cholera-infected water? Why?
- Try to add different basemaps of your choice and discuss results.
- Make spatial queries "death_count_field" BETWEEN 0 AND 15

---
### Data Source & Documentation

GeoDa Data and Lab ([https://geodacenter.github.io/](https://geodacenter.github.io/))
QGIS Laying out the maps ([https://docs.qgis.org/3.40/en/docs/user_manual/print_composer/index.html](https://docs.qgis.org/3.40/en/docs/user_manual/print_composer/index.html))
