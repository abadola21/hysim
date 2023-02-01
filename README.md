# hysim
Python codes to simulate hyperspectral data and generate vegetation map for boreal Alaska at Sentinel-2 scale.

There are three Jupyter notebooks: DEM_preprocessing, Simulation, Prediction

**1. DEM_preprocessing:**
This notebook is for preprocessing DEM that includes clipping and reprojecting DEM as Sentinel image. You can download ASTER Global Digital Elevation Model (GDEM) (https://earthdata.nasa.gov/). You will need to mosaic all the tiles that cover the scene. In this notebook, provide the location of DEM and Sentinel image. The output from this process will be used in Prediction. 

**2. Simulation:**
This notebook is for simulating hyperspectral data. Provide Sentinel image and 5 csv files as input (available inside Data folder)

**_birch.csv_:** this is the spectral reflectance of birch using spectroradiometer

**_black_spruce.csv_:**  this is the spectral reflectance of black spruce using spectroradiometer

**_trail.csv:_** this is the spectral reflectance of trail using spectroradiometer

**_srf_mss.csv_:** this is the spectral response function for Sentinel data (unique to the sensor)

**_AVIRIS_SRF.csv_** this is the spectral response function for AVIRIS_NG data (unique to the sensor)

Final output will be a folder with simulated tiles and a VRT file. The VRT file will be the input for the Prediction notebook. 

**3. Prediction:**
This notebook is for classifying the simulated hyperspectral data. 
Provide path for four files: DEM, simulated data, model path and metadata info (model path and metadata info files are available inside Data folder)

**_RandomForest.joblib_:** This is the trained model for the boreal domain of Alaska. 

**_Meta_Info.json_:** This has metadata information

The output will be tiles and the VRT file. Convert VRT file to Tiff using the following command in terminal:
**gdal_translate /..location../PredictedLabel.VRT /..location../Predicted.tif**

==============================================

**Important Note**

Notebook has comments at the locations where you need to change the file. 

If you want to simulate the data for different locations than boreal Alaska, you will have to identify the major classes on ground (like boreal region has birch, black spruce and gravel/trail). SRF for Sentinel and AVIRIS_NG data will remain the same.

You will have to train the model using the training data for your location. Additional Jupyter notebook (**Classification**) has been provided to train model and check model accuracy. You will have to provide DEM, simulated hyperspectral image (VRT file output from Simulation notebook) and input training data (shapefile or geojson (preferred format)).

The output will be RandomForest.joblib, Meta_Info.json and model assessments. Use RandomForest.joblib and Meta_Info.json in Prediction notebook.

**Reference material:**

Badola et al. (2021) https://doi.org/10.3390/rs13091693

Badola et al. (2022) https://doi.org/10.1016/j.jag.2022.102891

For additional information contact: abadola@alaska.edu

This material is based upon work supported by the National Science Foundation under the award OIA-1757348 and the State of Alaska
