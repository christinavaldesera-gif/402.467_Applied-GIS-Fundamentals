# Lab 00: Introduction to GIS Fundamentals  
## 🎯 Session Goals
- Discuss terminology of Geographic Information Systems (GIS)  
- Learn about spatial data types and data structure in GIS  
- Recognize the importance of managing your GIS workspace effectively  
- Get acquainted with the QGIS software: what it is and how to install it  

---

## 1. What is GIS? 🌍    
GIS (Geographic Information System) is a technology for capturing, storing, analyzing and visualizing spatial or geographic data. It enables us to understand patterns, relationships and trends through maps and spatial analysis.

## 2. Why is GIS Important?  
GIS helps in diverse fields such as environmental management, urban planning, transportation, public health and more. It allows decision-makers to make informed choices based on spatial information.

## 3. Key Concepts in GIS  

### I. Spatial Data Types 
**Vector Data:** Represents discrete geographic features using points, lines and polygons. Examples include:     
  - Points (e.g., cities, landmarks)     
  - Lines (e.g., roads, rivers)     
  - Polygons (e.g., administrative boundaries, lakes)   
      
**Raster Data:** Composed of grid cells or pixels representing continuous phenomena such as elevation, satellite imagery, or temperature.

### II. Layers  
  GIS maps are built from layers, each containing one type of spatial data. Layers can be combined and analyzed together.

### III. Attributes  
Features in layers have associated attribute data (e.g., a city’s name, population, or area).

### IV. Coordinate Reference Systems (CRS)  
CRS defines how your 2D map corresponds to real-world locations on Earth. Using the correct CRS ensures spatial accuracy and meaningful analysis.

---

## 4. Importance of Organizing Your GIS Workspace 📂 
Proper organization of files prevents data loss and improves workflow efficiency.  

**Tip:**  
- Create a dedicated project folder on your computer.  
- Inside that folder, create subfolders for:  
  - Raw Data  
  - Processed Data  
  - Outputs  

This structure keeps your GIS files and projects organized and easier to manage in QGIS.

---

## 5. File Naming Best Practices
QGIS file and folder names are *case sensitive* and sometimes sensitive to special characters. Avoid spaces and special characters; instead, use underscores `_` or hyphens `-`. For example:  
  - Use: `my_project.qgz`  
  - Avoid: `My Project.QGZ` or `my project.qgz`  

## 6. QGIS Project Files (`.qgz` or `.qgs`) 
These files save your workspace setup, including loaded layers, styles and layouts. Always save your project in your dedicated workspace folder and save frequently to avoid losing your work.

**Backing Up Your Data:**  
A good practice is to keep backup copies of data and project files in a different location or cloud storage to prevent accidental loss.
  
---

## 7. Introduction to QGIS 🗺️
QGIS is a free, open-source GIS software that enables users to work with spatial data easily. It supports a wide range of GIS tasks from data visualization to spatial analysis.

  
⁉️*Why use QGIS as our GIS software?*  

> **Answer:**  
> - It’s **free** and open-source, so accessible to everyone  
> - It supports a wide range of **data formats and coordinate systems**  
> - It combines **powerful GIS capabilities** with a friendly interface that beginners can quickly learn

---

## To Do: Install QGIS Software

1️⃣ **Download and Install QGIS**  
- Visit [https://qgis.org/en/site/](https://qgis.org/en/site/) and download the latest Long Term Release (LTR) english version suitable for your operating system  
- Follow the installation wizard prompts. Accept default settings unless you have specific needs  

---  

2️⃣ **Open QGIS and Explore the Interface**  
- When you launch QGIS, notice:  
  - **Menu Bar:** Contains all available tools and settings  
  - **Toolbars:** Quick access buttons for common functions
  - **Layers Panel:** Manage which layers are visible and editable
  - **Browser Panel:** Navigate files and data sources 
  - **Map Canvas:** Main area where your map and data appear
  - **Processing Toolbox:** Access advanced spatial analysis tools 

## What’s Next? ⏭️  
There is **no independent section to work on for Lab 00**, but it is essential that you download QGIS and grasp these foundational concepts before moving on. A solid understanding of GIS fundamentals will make working with QGIS in Lab 01 much smoother.

Take your time to familiarize yourself deeply with the concepts here before starting Lab 01.

---

