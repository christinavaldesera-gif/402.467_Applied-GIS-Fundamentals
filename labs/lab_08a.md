# Lab 08a: Calculating NDVI & NDWI Indices using QGIS 

## 🎯Learning Objective
- **Calculate NDVI and NDWI indices using QGIS Raster Calculator**

---
## Steps

1️⃣ **Open QGIS, Add your Image Tile & Bands**
- Go to `Layer` > `Add Layer` > `Add Raster Layer` and load your image tile (e.g.tile_02)
- From the bands folder, also add the bands `B04` & `B03`

2️⃣ **Calculate NDVI using QGIS Raster Calculator**
- Open QGIS Raster Calculator via `Raster` > `Raster Calculator`
- To calculate **NDVI**, adjust the expression below according to your tile:

("tile_02_B04@1" - "tile_02_B03@1") / ("tile_02_B04@1" + "tile_02_B03@1") ,

here: `"tile_02_B04@1"` is the Near-Infrared band and `"tile_02_B03@1"` is the Red band

- Set output layer like `NDVI.tif` and save
- Right click the newly created layer and go to `Properties` > `Symbology` > `Render Type: Singleband pseudocolor`
- Choose the `Greens` color ramp. Higher vegetation values will appear dark green and lower values will appear light green to white
- Select `Equal Interval`, then press `Apply` and `OK`

3️⃣ **Calculate NDWI using QGIS Raster Calculator**
- Load the `B02` band
- To calculate **NDWI**, adjust the expression below according to your tile:

 ("tile_02_B02@1" - "tile_02_B04@1") / ("tile_02_B02@1" + "tile_02_B04@1") ,

here: `"tile_02_B02@1` is the Green band and `"tile_02_B04@1"` is the Near-Infrared band

- Save output as `NDWI.tif` and save
- Apply the `Blues` color ramp  for clear visualization

> ❓**Question:** Click to see the answer  
<details>
  <summary>Why do we calculate NDVI and NDWI using these band combinations?</summary>

  These combinations highlight specific land cover characteristics: NDVI emphasizes vegetation health using NIR and Red bands; NDWI highlights water bodies using Green and NIR bands.
</details>

---
## 🚀Independently
- Provide your image classification results and make sure to answer the following giving specific examples:
    - which land cover class was most challenging to classify on your tile and what were the possible reasons?
    - how did the number and distribution of your ROIs impact your classification accuracy?
    - what challenges or uncertainties did you encounter during classification (such as cloud shadows or mixed pixels) and how might these be addressed?
- Provide your NDVI and NDWI results and explain in your own words what are some advantages of using Remote Sensing and GIS for environmental analysis.
- Include the aforementioned tasks in your QGIS report
---
