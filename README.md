# DATA 512:  Part 1 - Common Analysis

## Wildland Fire Impacts on Madison, WI

### Project Overview

Summers in the western U.S. are becoming more and more known for wildfires, with smoke spreading to many states. There are several reasons for this, including climate change, U.S. forestry policies, and increased awareness of the problem. No matter what causes the fires, they have a wide impact because wildfire smoke lowers air quality in many cities. More studies are showing that smoke can have negative effects on health, tourism, property, and many other areas of society.

The main goal of this project is to closely study the effects of wildfire smoke on Madison, WI to provide practical insights that can help various interested groups. First, we will look at past wildfire data to estimate how much smoke has reached the city in recent years and compare with AQI values for Madison city. Using this information, we build a predictive model to predict smoke patterns that Madison might experience over the next 25 years.

### License

#### Data License

- Data pertaining to Wildland Fires, provided by the USGS, are [publicly available](https://www.sciencebase.gov/catalog/item/53f6271fe4b09d12e0e9bd03) and not subject to copyright restrictions. However they can be cited as below.
``` text
Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
```

- AQI data accessed through the EPA API lies in the [public domain](https://edg.epa.gov/epa_data_license.html) and is not subject to domestic copyright protection under [17 U.S.C. § 105](https://www.copyright.gov/title17/92chap1.html#105).

#### Code Attribution

Snippets of the code were taken from a code example developed by **Dr. David W. McDonald** for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the **Creative Commons CC-BY license**.

Rest of the code is licensed under standard [MIT licence](https://github.com/ManasaSRonur/data-512-project/blob/main/LICENSE).


### API Documentation/References

- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
- [Wildland fire dataset from USGS](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
- [AQI Calculation](https://www.airnow.gov/publications/air-quality-index/technical-assistance-document-for-reporting-the-daily-aqi/)
- [GeoJSON](https://geojson.readthedocs.io/en/latest/)
- [pyproj](https://pyproj4.github.io/pyproj/stable/)


#### Access Key
To use AQI related API we need to request a key using a valid email address. The EPA then sends a confirmation email link and a 'key' that we use for all other requests.
We only need to sign-up once, unless we want to invalidate the current key (by getting a new key) or we lose the key. Refer to the notebook [2_aqi_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/2_aqi_data_acquisition.ipynb) for additional information.

### Data Files

#### Input Data File

The input data file is too large to be uploaded to the git repository. Follow the below instructions to obtain the inout file.

1. Visit this [link](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81).
2. Download `GeoJSON Files.zip`.
3. unzip to extract the contents.
4. Locate the file `USGS_Wildland_Fire_Combined_Dataset` to be used as input file.

The input files has below keys.
- `displayFieldName`: An empty string which otherwise denotes the name of the dataset.

- `fieldAliases`: dictionary that holds human readable name of each of the 30 fields.

- `geometryType`: Specifies shape type of the spatial data.

- `spatialReference`: Defines the coordinate system used for the Geodata

- `fields`: A list of dicts identifying the name, type and alias of 30 attributes.

- `features`: The list of all observations stored in JSON format. Each observation is saved as dictionary with keys for the attributes (fields) and geometry.


### Intermediary Data Files

These files are generated as we progress through the project workflow to be used in the subsequent stages. They are located under the folder [intermediary_files](https://github.com/ManasaSRonur/data-512-project/tree/main/intermediary_files)

- [**distance.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/distance.csv)
 
    This csv file contains the calculated shortest distances for each fire from Madison.
  - **Fields**:
    - `OBJECTID`: Integer - A unique ID for each fire polygon.
    - `shortest_dist`: Integer - distance in miles

- [**all_wildfire_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/all_wildfire_1964_2024.csv)
 
    This csv file contains selected attributes and the calculated shortest distances for all fires that occured between 1964 and 2024
  - **Fields**:
    - `OBJECTID`: Integer - A unique ID for each fire polygon.
    - `Assigned_Fire_Type`: String - The attributed type of the fire. 
    - `Fire_Year`: Integer - The year of the fire season
    - `GIS_Acres`: Integer - The overall area burned by the fire(s) in acres.
    - `GIS_Hectares`: Integer - The overall area burned by the fire(s) in hectares.
    - `Listed_Fire_Names`: Sring - A string of comma-separated values for the fire(s) attributed to the polygon.
    - `Overlap_Within_1_or_2_Flag`: String - An attribute to identify areas that burned with >10% overlap of the current fire within 1 or 2 years of the current burn
    - `Shape_Length`: Integer - A proprietary ESRI raw measurement of the longest section of the polygon in the ESRI projection space units (assumed m)
    - `Shape_Area`: Integer - A proprietary ESRI raw measurement of the polygon area in the ESRI projection space units (assumed m^2).
    - `Circleness_Scale`: Integer - A measure of a polygon's similarity to a true circle.
    - `shortest_dist`: Integer - distance in miles


- [**madison_wildfire_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/madison_wildfire_1964_2024.csv)
 
    This csv file contains selected attributes and the calculated shortest distances for all fires that occured between 1964 and 2024 and were within 650 miles.
  - **Fields**:
    - `OBJECTID`: Integer - A unique ID for each fire polygon.
    - `Assigned_Fire_Type`: String - The attributed type of the fire. 
    - `Fire_Year`: Integer - The year of the fire season
    - `GIS_Acres`: Integer - The overall area burned by the fire(s) in acres.
    - `GIS_Hectares`: Integer - The overall area burned by the fire(s) in hectares.
    - `Listed_Fire_Names`: Sring - A string of comma-separated values for the fire(s) attributed to the polygon.
    - `Overlap_Within_1_or_2_Flag`: String - An attribute to identify areas that burned with >10% overlap of the current fire within 1 or 2 years of the current burn
    - `Shape_Length`: Integer - A proprietary ESRI raw measurement of the longest section of the polygon in the ESRI projection space units (assumed m)
    - `Shape_Area`: Integer - A proprietary ESRI raw measurement of the polygon area in the ESRI projection space units (assumed m^2).
    - `Circleness_Scale`: Integer - A measure of a polygon's similarity to a true circle.
    - `shortest_dist`: Integer - distance in miles

- [**gaseous_aqi_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/gaseous_aqi_1964_2024.csv)
 
    This csv file contains the gaseous pollutant data as raw response of API calls, from all the monitoring stations in Dane county.
  - **Fields**:
    - `state_code`: Integer - FIPS code of the state.
    - `county_code`: Integer - FIPS code of the county
    - `site_number`: Integer - The specific monitoring site identifier within the county.
    - `latitude`: Integer - The latitude in decimal degrees where the air quality monitoring site is located.
    - `longitude`: Integer - The longitude in decimal degrees where the air quality monitoring site is located.
    - `parameter_code`: Integer - This code represents the specific pollutant or parameter being monitored.
    - `validity_indicator`: String - A flag that indicates whether the sample data is valid or invalid.
    - `parameter`: String - The name of the specific pollutant or parameter.
    - `sample_duration`: The time period over which the pollutant sample is averaged.
    - `arithmetic_mean`: The average concentration of the parameter measured.
    - `units_of_measure`: String - The units used to measure the parameter.
    - `date_local`: Date - The date of data collection in the format YYYY-MM-DD.
    - `aqi`: Integer - The Air Quality Index (AQI) value.


- [**particulate_aqi_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/particulate_aqi_1964_2024.csv)
 
    This csv file contains the particles pollutant data as raw response of API calls, from all the monitoring stations in Dane county.
  - **Fields**:
    - `state_code`: Integer - FIPS code of the state.
    - `county_code`: Integer - FIPS code of the county
    - `site_number`: Integer - The specific monitoring site identifier within the county.
    - `latitude`: Integer - The latitude in decimal degrees where the air quality monitoring site is located.
    - `longitude`: Integer - The longitude in decimal degrees where the air quality monitoring site is located.
    - `parameter_code`: Integer - This code represents the specific pollutant or parameter being monitored.
    - `validity_indicator`: String - A flag that indicates whether the sample data is valid or invalid.
    - `parameter`: String - The name of the specific pollutant or parameter.
    - `sample_duration`: The time period over which the pollutant sample is averaged.
    - `arithmetic_mean`: The average concentration of the parameter measured.
    - `units_of_measure`: String - The units used to measure the parameter.
    - `date_local`: Date - The date of data collection in the format YYYY-MM-DD.
    - `aqi`: Integer - The Air Quality Index (AQI) value.


- [**yearly_aqi_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/yearly_aqi_1964_2024.csv)
 
    This csv file contains annual AQI estimates.
  - **Fields**:
    - `year`: Integer - Year.
    - `aqi`: String - The average AQI estimate for the year. 

- [**madison_yearly_smoke_estimate_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/madison_yearly_smoke_estimate_1964_2024.csv)
 
    This csv file contains annual Smoke estimates.
  - **Fields**:
    - `Fire_Year`: Integer - The year the fire occured.
    - `Smoke_Estimate`: String - The Smoke estimate for the year. 

#### Output Files
All these files are located under [output_files]()
- [histogram_number_of_fires.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/histogram_number_of_fires.png) 
A histogram showing the number of fires occurring every 50 mile distance from Madison for all fires ranging up to 1800 miles away from Madison. The histogram also indicates the 650 mile distance cut-off.

- [Total_acres_burned.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/Total_acres_burned.png)
A time series graph of total acres burned per year for the fires occurring in the 650 mile radius from Madison. 

- [compare_smoke_vs_aqi.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/compare_smoke_vs_aqi.png)
A time series graph comparing the calculated fire smoke estimates for Madison and the average AQI for Madison.


### Project Workflow

- [1_wildfire_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/1_wildfire_data_acquisition.ipynb)

This notebook reads the wildland fire dataset from USGS, calculates the distance from Madison for each fire, filters the data for years 1964 - 2024 and generates the two csv files with selected columns. One for all the fires between the mentioned dates and one for the fires occured between these dates but within 650 mile radius from Madison.

- [2_aqi_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/2_aqi_data_acquisition.ipynb)

This notebook is used to fetch AQI data from API, clean the data, calculate missing APIs and finally generated a csv file of yearly AQI estimates for years 1964 - 2024.

- [3_smoke_estimation.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/3_smoke_estimation.ipynb)

This notebook utilises the files generated by the above notebooks to calculate smoke estimates and compare with AQI data to validate the calculated smoke estimates.
- [4_predictive_model.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/4_predictive_model.ipynb)

This notebook is used to build a predictive model on smoke estimates to forecast smoke estimates for next 25 years.

- [5_visualizations.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/5_visualizations.ipynb)

This notebook is used to analyse the data generated so far through visuals. It generated the three specific visulas as mentioned under output files.

### Limitations/Considerations.

- The Listed_fire_Dates includes all individual dates from merged datasets that overlap in the same area and year. This can provide more details but also adds variation and possible duplication, especially when multiple sources are involved making it unreliable.
- The tool used to measure fire distances works only with ring-shaped fire boundaries, so 36 fires with curve ring shapes failed while calculating distance and not included in analysis.
- AQI was missing for many records, which were recalculated using the available pollutants data. This adds some level of uncertainity to the calculated value.
- AQI data is very sparse for years 2001 to 2009 leading poor qualirt average. This makes it difficult to compare and asses out calculation of smoke estimates for this period.
- The predictive model has R^2 value of only 0.71 which means the model explains about 71% of the variation in the data, there is still a lot of room for improvement in the model. Additionally the predicted values could be off by atleast 2 units which is significantly high for our scale of smoke estimates. While this is a fairly good model considering the data availability limitaion, this is not the best model to forecast the smoke estimate.



