1. Data Source and Download Procedure

Nighttime light data used in this project were obtained from the Visible Infrared Imaging Radiometer Suite (VIIRS) Black Marble product, 
specifically the VNP46A2: Gap-Filled Lunar BRDF-Adjusted Nighttime Lights Daily L3 Global product. This dataset is produced by the NASA 
Earth Observing System Data and Information System (EOSDIS) and distributed through the NASA Earthdata portal and the LAADS Distributed 
Active Archive Center (DAAC). The VNP46A2 product provides daily observations of nighttime radiance corrected for atmospheric effects, 
lunar illumination, and bidirectional reflectance distribution function (BRDF) effects. These corrections improve the consistency of 
nighttime light measurements and allow the dataset to be used for time-series analysis of human activity, infrastructure, and disaster impacts.

Data were accessed using the NASA Earthdata system through the Python library earthaccess, which enables programmatic searching and downloading 
of satellite data products. The dataset was queried by specifying the product name (VNP46A2), a temporal range, and a geographic bounding 
box corresponding to the Houston, Texas region. For initial testing, a single day of observations was downloaded. Because the study area 
overlaps two VIIRS spatial tiles, the download returned two files representing adjacent grid tiles (h08v05 and h08v06) for that day. Each file 
is provided in Hierarchical Data Format version 5 (HDF5) (.h5), which stores multiple scientific variables within a structured data hierarchy.

2. Dataset Structure and Variables

Each downloaded VIIRS file contains a 2400 × 2400 grid representing nighttime radiance values over a geographic tile with a spatial resolution 
of approximately 15 arc-seconds (~500 m). The data are organized into several scientific variables stored within the HDF-EOS grid structure. 
The primary variable used for analysis is Gap_Filled_DNB_BRDF-Corrected_NTL, which represents the gap-filled, BRDF-corrected nighttime radiance 
measured in nWatts/cm²/sr. Additional variables included in the dataset provide supporting information such as the raw corrected radiance 
(DNB_BRDF-Corrected_NTL), lunar irradiance (DNB_Lunar_Irradiance), and quality control flags indicating cloud contamination, snow presence, and retrieval reliability.

To facilitate further analysis and machine learning applications, the raster data were converted into a tabular format where each pixel 
corresponds to a geographic coordinate. In this structure, each row represents a single pixel with associated latitude, longitude, 
nighttime light intensity, and quality indicators. This transformation enables the dataset to be easily analyzed using standard 
data science and machine learning tools while preserving the spatial information of the original satellite observations.
