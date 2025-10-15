# Lab_02: Getting to Know QGIS ~ Work with OSM Data in QGIS

## 🎯 Learning Objectives  
- Adding and managing layers in QGIS  
- Learn to use QGIS plugins
- Get familiar with open data sources  
- Working with attribute table

---
## Open Street Maps 
OpenStreetMap (OSM) is an open-source collaborative project that creates and provides free, editable geographic data alternative to commercial map services. It's built by a global community of volunteers who map the world by collecting data from surveys, aerial imagery and other sources. This data is then made available under an open license, allowing anyone to use, modify and share it.

Learn more and explore OSM on its official wiki: [OpenStreetMap Wiki](https://wiki.openstreetmap.org/)

---
## Steps

1️⃣ **Open QGIS and Set Up Your Project**
- Launch QGIS  
- Start a new project. `Project` > `New` and save it right away. `Project` > `Save as` in your working folder. Give it a name like `Lab02_<YourName>`

2️⃣ **Add Basemap via QuickMapServices Plugin**
- Click `Plugins` in the `Main menu`
- Select `Manage and Install Plugins`
- Search for **QuickMapServices** and install plugin
- The plugin can be found in `Web` in the `Main menu`. The **QuickMapServices** plugin offers a variety of basemaps including multiple OSM styles, satellite imagery and other web map layers.  

> [!TIP]
> If you don’t see a wide variety of basemap options in QuickMapServices, don’t worry!  
> - Go to `Web` > **QuickMapServices** > **Settings**  
> - Open the **More services** (or Contributed Services) tab  
> - Click **Get contributed pack** to download and add many additional basemaps  
> - After that, close the settings and reopen the QuickMapServices menu to discover many more map styles and layers to choose from

3️⃣ **Mark The Place Of Your Choice**  

**Create Layer & Attributes**
- Click `Layer` > `Create Layer` > `New Shapefile Layer`  
- Set `File name` by clicking the `...` button & choosing the folder and name for your new layer (e.g., `MySpecialPlace.shp`)
- Set `File encoding` as default & for `Geometry type` set `Point`
- Set the `CRS` to `EPSG:3857`   
- Add attribute fields (columns) by filling in the `New Field` section:
   - add a field called `name` with type **Text (string)** and length set as default
   - add a field called `notes` with type **Text (string)** and length set as default
   - click **Add to Fields List** for each field you create
   - When finished adding fields, click **OK** to create the layer
  
**Add Coordinates**
- In the `Layers Panel`, right-click your new point layer and select **Toggle Editing** to enable editing mode 
- Double click to go to `Fields` and then add another two fields:
   - add a field called `x_coord` with type **Decimal number (real)** and length set as default 
   - add a field called `y_coord` with type **Decimal number (real)** and length set as default 
- Go to `Attributes Form` select the x_coord field and set `$x` as a `Default value` and click `Apply default value on update`. Do the same for the y_coord and set `$y`
- Press `Apply` and `OK`

**Add Point(s) in Map Canvas**
- Activate the `Add Point` tool from the `Toolbar`  
- Click on the map where your special place is located to add your point. You’ll see that coordinates are automatically assigned to your point  
- When finished adding points, click the **Save Edits** button (floppy disk icon on the toolbar) to save your changes to the layer  
- When you finish editing both geometries and attributes, right-click your layer again and select **Toggle Editing** to exit the editing mode safely.  

> [!WARNING]  
> You cannot add points directly on basemap layers (like QuickMapServices), as these are raster images and non-editable. Always work on an editable vector point layer for digitizing!

4️⃣ **Style Your Point(s) for Clarity and Personality** 🎨  
- To make your points visually clear and meaningful, you can customize their symbology:  
  - Right-click your point layer > **Properties**  
  - Go to the **Symbology** tab  
  - Choose a simple symbol (circle, star, etc.)  
  - Change size, color, or add labels using the **Labels** tab  
  - Click **OK** to apply changes
  
5️⃣ **Add Additional Layers or Context**
- You can continue enriching your map by adding other layers:  
  - Load OSM vector layers using QGIS plugins such as OSMDownloader and/or QuickOSM  
  - Add basemaps for reference  
      
6️⃣ **Create a Map Layout for Presentation**  
- Open the **Print Layout** with **Project > New Print Layout**  
- Give your layout a name like `Map_of_<YourPlace>`  
- In the layout window, add your map with **Add Map** tool and draw a rectangle for it  
- Use the **Add Label** tool to add a big, clear title — something like *“My Special Place”*  
- Add a legend, scale bar and north arrow
  
7️⃣ **Export Your Map**  
- Once happy with the layout, export your map as an image:  
  - Click **Layout > Export as Image**  
  - Save the file in your project folder with a meaningful name  

---
🥳Well done ! You have completed creating your own map.

---
## 🚀Independently
- **Experiment with the Open Street Map's capabilities and create a complete map with your personal touch**
- **Save the map as an image and write a brief report explaining your steps**
