# aquaculture-detection
# Aquaculture Detection using Google Earth Engine

## Overview
This project aims to detect aquaculture areas and water bodies using satellite imagery and remote sensing techniques. The analysis leverages **Google Earth Engine (GEE)**, specifically using **Sentinel-2** imagery and **Normalized Difference Water Index (NDWI)** for classifying water bodies and aquaculture zones. The classification is carried out using the **Support Vector Machine (SVM)** classifier.

## Features
- NDWI computation to detect water bodies.
- Classification of water and non-water areas, including aquaculture detection.
- Cloud masking using QA bands from Sentinel-2 imagery.
- Export of results to Google Drive for further analysis.

## Requirements
- A **Google Earth Engine** account. If you don't have one, you can sign up [here](https://signup.earthengine.google.com/).
- Access to **Sentinel-2** imagery for the region of interest.
- **Geometry boundary** (polygon of the area you are analyzing, used in the `geometry` variable).

## How to Run the Code
1. **Go to the Google Earth Engine Code Editor**:
   - Navigate to [https://code.earthengine.google.com/](https://code.earthengine.google.com/).
   - Log in using your Google account (or sign up for access).

2. **Create a New Script**:
   - Click on **New** → **New Script**.
   - Give it a name, such as `Aquaculture Detection`.

3. **Copy and Paste the Code**:
   - Copy the GEE code from this repository.
   - Paste it into the new script in the Code Editor.

4. **Run the Script**:
   - After pasting the code, click the **Run** button at the top of the editor.
   - The map will display the classification of water bodies and aquaculture areas.

5. **Export the Results**:
   - The results (classified image) will be exported to your **Google Drive**.
   - Check your **Google Drive** for the image file, typically named `imageToDriveExample_transform`.

## Code Explanation
1. **Water Occurrence Masking**:
   - We use the **JRC Global Surface Water Dataset** to detect water occurrence.
   - A mask is created to identify water pixels and exclude areas with minimal water occurrence.

2. **Sentinel-2 Data Processing**:
   - Sentinel-2 imagery from the year 2020 is filtered and cloud masking is applied using the **QA60** band.
   - The **NDWI (Normalized Difference Water Index)** is calculated to distinguish water bodies from other land surfaces.

3. **Classification**:
   - A supervised classification is performed using the **Support Vector Machine (SVM)** classifier, with two classes: **Water** (class 1) and **Aquaculture** (class 0).

4. **Area Calculation**:
   - The script calculates the total area of the classified water and aquaculture regions using pixel areas.

5. **Export**:
   - The classified map is exported to Google Drive for further analysis or visualization.

## Exported Results
Once the script is executed, the output image will be stored in **Google Drive**. You can use this image for further spatial analysis, map creation, or reporting.

## Additional Notes
- You can modify the geometry (`geometry`) to analyze different regions.
- Adjust the NDWI threshold if the classification results are not satisfactory.
- The script currently uses a simple SVM classifier, but you can experiment with other machine learning classifiers or add more training data for better accuracy.

## License
This project is licensed under the **MIT License** - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgments
- **Sentinel-2** imagery: Provided by the European Space Agency (ESA).
- **Google Earth Engine**: For offering powerful cloud-based geospatial processing.
- **JRC Global Surface Water**: For the water occurrence dataset.

---

## Contributing
If you would like to contribute to this project:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Create a pull request.

---

## Contact
For questions or suggestions, feel free to reach out to **reshmaraj532@gmail.com**.
