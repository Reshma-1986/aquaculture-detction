# Aquaculture Mapping Using Sentinel-2 NDWI in Google Earth Engine

This project maps aquaculture ponds within a user-defined study area using Sentinel-2 satellite imagery and NDWI (Normalized Difference Water Index). It utilizes Google Earth Engine (GEE) for cloud filtering, water detection, vectorization, and geometric filtering to isolate aquaculture features.

##  Data Source
- **Satellite**: Sentinel-2 Surface Reflectance (COPERNICUS/S2_SR)
- **Time Period**: January 1, 2020 – December 31, 2020
- **Bands Used**:
  - B3 (Green)
  - B8 (Near Infrared - NIR)
  - QA60 (for cloud and cirrus masking)

##  Study Area
The script uses a predefined geometry (`g1`) that represents the boundary of the region of interest (ROI). Replace `g1` with your study area polygon.

---

##  Workflow Overview

### 1. **Cloud and Cirrus Masking**
- The QA60 band is used to mask clouds and cirrus using bitwise operations.

### 2. **NDWI Calculation**
- NDWI = (Green - NIR) / (Green + NIR)
- Helps in identifying water bodies.

### 3. **Image Collection Processing**
- Sentinel-2 SR images are filtered for the year 2020 and cloud cover < 20%.
- NDWI is calculated for each image.
- A mean composite NDWI image is generated.

### 4. **Thresholding**
- NDWI threshold of `> 0.06` is applied to isolate water bodies.
- Threshold can be tuned for different regions.

### 5. **Vectorization**
- Binary NDWI mask is converted to vector polygons.
- Geometry is simplified to reduce complexity.

### 6. **Shape and Area Filtering**
- Polygons are filtered by:
  - Area < 50 hectares (500,000 sq. meters)
  - Shape Index > 0.2 (to eliminate linear features like rivers)

### 7. **Output**
- Final layer highlights probable aquaculture ponds.
- Total area of aquaculture is calculated and printed in:
  - Square meters
  - Hectares


##  Technical Concepts

###  NDWI (Normalized Difference Water Index)
The **Normalized Difference Water Index (NDWI)** is a satellite-derived index that highlights water features in remote sensing imagery. It is particularly useful for identifying water bodies such as lakes, ponds, and aquaculture farms.

**Formula:**

NDWI = (Green - NIR) / (Green + NIR)


- **Green Band (B3)**: Strongly reflects from water surfaces.
- **NIR Band (B8)**: Water absorbs NIR, resulting in low reflectance.

**Values:**
- NDWI > 0.06 typically indicates water bodies.
- NDWI < 0 often corresponds to vegetation, built-up areas, or bare soil.

> NDWI helps distinguish water features from non-water areas efficiently and is widely used for water resource mapping, flood detection, and aquaculture monitoring.

---

###  Shape Index (Compactness Index)
To differentiate between **aquaculture ponds** and **natural linear features** like rivers or canals, we use a geometric measure called the **Shape Index** (also known as Compactness Index).

**Formula:**
Shape Index = (4 × π × Area) / (Perimeter²)


- **Value Range**:
  - Close to **1.0** → Perfectly circular or square (ideal for aquaculture ponds).
  - Close to **0.0** → Very elongated or irregular (rivers, canals).

> This helps filter out natural water bodies that are less compact and retain only features that resemble human-made ponds used for aquaculture.

---

###  Area Filtering
Large natural water bodies like lakes and wetlands are often excluded by setting an **area threshold**, e.g., `< 50 hectares (500,000 sq. meters)`. This size constraint complements the shape index in isolating small-scale, regular aquaculture ponds.

---

By combining **spectral (NDWI)** and **geometric (shape and area)** characteristics, the model ensures a more accurate detection of aquaculture features while minimizing false positives.



---

## Recommendations
- **NDWI Threshold**: Tune based on region and season. Consider using dynamic thresholding (e.g., Otsu’s method).
- **Seasonal Filtering**: Restrict analysis to dry/post-monsoon season to avoid misclassification due to flooding.
- **Validation**: Use high-resolution imagery (e.g., from Google Earth or PlanetScope) to validate detected ponds/Use Support Vector Machine (SVM).
- **Export**: Use `Export.table.toDrive()` to save the vector results for further analysis.
-  **Use Better Data Product**: Use A nalysis Ready Data(ARD) for better ddetection.

---

## How to Run
1. Open [Google Earth Engine Code Editor](https://code.earthengine.google.com).
2. Paste the full script into the editor.
3. Replace `g1` with your own study area geometry.
4. Click **Run**.
5. View the results in the map and console.

---

## License
This code is provided under the MIT License. You may use, modify, and distribute it freely with attribution.

---

##  Author
- Reshma

