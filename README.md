# Analysis of Wildfire Smoke and Its Impact on Respiratory Health of Madison, WI

### Project Overview

Summers in the western U.S. are becoming more and more known for wildfires, with smoke spreading to many states. There are several reasons for this, including climate change, US forestry policies, and increased awareness of the problem. No matter what causes the fires, they have a wide impact because wildfire smoke lowers air quality in many cities. More studies are showing that smoke can have negative effects on health, especially respiratory health.

From a scientific perspective, understanding the health consequences of wildfire-induced smoke provides crucial insights into the direct impact of climate-related events on respiratory health. Practically, these findings can guide public health interventions, informing policies that protect vulnerable populations, especially during peak wildfire seasons. By integrating localized air quality data and health records, this research aims to identify whether increased smoke exposure correlates with adverse health effects. The specific research questions include:
 - Does wildfire smoke significantly affect respiratory health (COPD, asthma, and tuberculosis) outcomes in Madison?
 - Is there a relationship between wildfire smoke exposure and increased death rates from respiratory illnesses, particularly those linked to COPD, asthma, and tuberculosis?
 - What is the demand for hospitalization and emergency visits for asthma, COPD, TB in the upcoming years and how can healthcare providers prepare for this demand?

The study  hypothesizes that the increasing levels of smoke exposure correlate with a rise in respiratory illnesses, hospitalizations, and potentially mortality rates. If confirmed, it is expected for these trends to continue upward if smoke levels persist or increase in coming years. Based on the insights uncovered and the severity of any effects observed, we can then advise the Madison city council, city manager/mayor, and city residents on potential solutions to mitigate these health impacts. Complete project can be found [here](https://github.com/ManasaSRonur/data-512-project/blob/main/Project%20Report.pdf)



### License

#### Data License

- Data pertaining to Wildland Fires, provided by the USGS, are [publicly available](https://www.sciencebase.gov/catalog/item/53f6271fe4b09d12e0e9bd03) and not subject to copyright restrictions. However they can be cited as below.
``` text
Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
```

- AQI data accessed through the EPA API lies in the [public domain](https://edg.epa.gov/epa_data_license.html) and is not subject to domestic copyright protection under [17 U.S.C. § 105](https://www.copyright.gov/title17/92chap1.html#105).

- Respiratory illness incident data downloaded as csv from Wisconsin Department of Health Services is publicly available for strictly non-commercial use but must be cited.

- Mortality data obtained from Institute for Health Metrics and Evaluation (IHME) is [free for non-commercial research purposes](https://www.healthdata.org/Data-tools-practices/data-practices/ihme-free-charge-non-commercial-user-agreement) but must be cited as below
``` text
Global Burden of Disease Collaborative Network. Global Burden of Disease Study 2021 (GBD 2021) Results. Seattle, United States: Institute for Health Metrics and Evaluation (IHME), 2022.
https://vizhub.healthdata.org/gbd-results/.
```

#### Data Sources
  - [USGS Wildfire Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
  - [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
  - [Mortality Dataset - IHME](https://vizhub.healthdata.org/gbd-results/).
  - [Asthma Data - Wisconsin DHS](https://www.dhs.wisconsin.gov/epht/asthma.htm)
  - [COPD Data - Wisconsin DHS](https://www.dhs.wisconsin.gov/epht/copd.htm)
  - [TB Data - Wisconsin DHS](https://www.dhs.wisconsin.gov/tb/data.htm)


#### Code Attribution

Snippets of the code were taken from a code example developed by **Dr. David W. McDonald** for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the **Creative Commons CC-BY license**.

Rest of the code is licensed under standard [MIT licence](https://github.com/ManasaSRonur/data-512-project/blob/main/LICENSE).

### Documentation/References

- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
- [Wildland fire dataset from USGS](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
- [AQI Calculation](https://www.airnow.gov/publications/air-quality-index/technical-assistance-document-for-reporting-the-daily-aqi/)
- [GeoJSON](https://geojson.readthedocs.io/en/latest/)
- [pyproj](https://pyproj4.github.io/pyproj/stable/)
- [Wisconsin Department of Health Services](https://www.dhs.wisconsin.gov/)
- [The Institute for Health Metrics and Evaluation](https://www.healthdata.org/)
- [Public Health Madison and Dane County](https://publichealthmdc.com/health-services/respiratory-illness/dashboard)


#### Access Key
To use AQI related API we need to request a key using a valid email address. The EPA then sends a confirmation email link and a 'key' that we use for all other requests.
We only need to sign-up once, unless we want to invalidate the current key (by getting a new key) or we lose the key. Refer to the notebook [2_aqi_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/2_aqi_data_acquisition.ipynb) for additional information.

### Data Files

#### Input Data File

- The input wildfire data file is too large to be uploaded to the git repository. Follow the below instructions to obtain the inout file.

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

- [**asthma-county.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/input_files/asthma-county.csv)

    This csv file contains information on county wise asthma-related hospitalizations and emergency department visits across Wisconsin from 2000 - 2023.
  - **Fields**:
    - `Fips` : Integer - Federal Information Processing Standards (FIPS) code representing a unique geographic identifier for the county.
    - `County` : String - The name of the county.
    - `Topic` : String - Type of case: Emergency Visit or Hospitalization.
    - `Year` : Integer - The year of the data.
    - `Count` : Integer - The total number of cases reported for the given topic in the specified county and year.
    - `Crude Rate` : Float - The crude rate, calculated as the number of cases divided by the total population of the county.
    - `State Count` : Integer - The total number of cases reported for the given topic in the entire state for the specified year.
    - `State Crude Rate` : Float - The crude rate for the entire state, calculated as the number of cases divided by the total state population.


- [**copd-county.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/input_files/copd-county.csv)
    
    This csv file contains information on county wise copd-related hospitalizations and emergency department visits across Wisconsin from 2000 - 2022.
  - **Fields**:
    - `FIPS` : Integer - Federal Information Processing Standards (FIPS) code representing a unique geographic identifier for the county.
    - `COUNTY` : String - The name of the county.
    - `TOPIC` : String - Type of case: Emergency Visit or Hospitalization.
    - `YEAR` : Integer - The year of the data.
    - `COUNT` : Integer - The total number of cases reported for the given topic in the specified county and year.
    - `CRUDERATE` : Float - The crude rate, calculated as the number of cases divided by the total population of the county.
    - `ST_COUNT` : Integer - The total number of cases reported for the given topic in the entire state for the specified year.
    - `ST_CRUDERATE` : Float - The crude rate for the entire state, calculated as the number of cases divided by the total state population.


- [**tb-county.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/input_files/tb-county.csv)

      This csv file contains information on county wise TB cases from 2014 - 2023
  - **Fields**:
    - `County` : String - The name of the county.
    - `Year` : Integer - The year of the data.
    - `Cases` : Integer - The total number of TB cases reported for the specified county and year.


- [**IHME-GBD_2021_DATA.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/input_files/IHME-GBD_2021_DATA.csv)

  - This csv file provides extensive data on mortality rates attributed to a variety of respiratory illnesses, including asthma, COPD, and TB, segmented by factors such as age and sex for the Wisconsin region for period 1980 - 2021, at state level.
  - **Fields**:
    - `Measure` : String - The type of measure being reported (e.g., Death).
    - `Location` : String - The name of the state where the data is collected.
    - `Sex` : String - Gender category: Male, Female, or Both.
    - `Age` : String - Age group of the population: All Ages or specific age ranges.
    - `Cause` : String - The specific illness or condition that caused death.
    - `Metric` : String - The type of metric used: Number (absolute count) or Percentage (proportional rate).
    - `Year` : Integer - The year of the data.
    - `Val` : Float - The rate of mortality or count of mortality based on the metric.
    - `Upper` : Float - Upper bound of the confidence interval for the reported value.
    - `Lower` : Float - Lower bound of the confidence interval for the reported value.


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
    - `GIS_Acres`: Float - The overall area burned by the fire(s) in acres.
    - `GIS_Hectares`: Float - The overall area burned by the fire(s) in hectares.
    - `Listed_Fire_Names`: Sring - A string of comma-separated values for the fire(s) attributed to the polygon.
    - `Overlap_Within_1_or_2_Flag`: String - An attribute to identify areas that burned with >10% overlap of the current fire within 1 or 2 years of the current burn
    - `Shape_Length`: Float - A proprietary ESRI raw measurement of the longest section of the polygon in the ESRI projection space units (assumed m)
    - `Shape_Area`: Float - A proprietary ESRI raw measurement of the polygon area in the ESRI projection space units (assumed m^2).
    - `Circleness_Scale`: Float - A measure of a polygon's similarity to a true circle.
    - `shortest_dist`: Float - distance in miles


- [**madison_wildfire_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/madison_wildfire_1964_2024.csv)
 
    This csv file contains selected attributes and the calculated shortest distances for all fires that occured between 1964 and 2024 and were within 650 miles.
  - **Fields**:
    - `OBJECTID`: Integer - A unique ID for each fire polygon.
    - `Assigned_Fire_Type`: String - The attributed type of the fire. 
    - `Fire_Year`: Integer - The year of the fire season
    - `GIS_Acres`: Float - The overall area burned by the fire(s) in acres.
    - `GIS_Hectares`: Float - The overall area burned by the fire(s) in hectares.
    - `Listed_Fire_Names`: Sring - A string of comma-separated values for the fire(s) attributed to the polygon.
    - `Overlap_Within_1_or_2_Flag`: String - An attribute to identify areas that burned with >10% overlap of the current fire within 1 or 2 years of the current burn
    - `Shape_Length`: Float - A proprietary ESRI raw measurement of the longest section of the polygon in the ESRI projection space units (assumed m)
    - `Shape_Area`: Float - A proprietary ESRI raw measurement of the polygon area in the ESRI projection space units (assumed m^2).
    - `Circleness_Scale`: Float - A measure of a polygon's similarity to a true circle.
    - `shortest_dist`: Float - distance in miles

- [**gaseous_aqi_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/gaseous_aqi_1964_2024.csv)
 
    This csv file contains the gaseous pollutant data as raw response of API calls, from all the monitoring stations in Dane county.
  - **Fields**:
    - `state_code`: Integer - FIPS code of the state.
    - `county_code`: Integer - FIPS code of the county
    - `site_number`: Integer - The specific monitoring site identifier within the county.
    - `latitude`: Float - The latitude in decimal degrees where the air quality monitoring site is located.
    - `longitude`: Float - The longitude in decimal degrees where the air quality monitoring site is located.
    - `parameter_code`: Integer - This code represents the specific pollutant or parameter being monitored.
    - `validity_indicator`: String - A flag that indicates whether the sample data is valid or invalid.
    - `parameter`: String - The name of the specific pollutant or parameter.
    - `sample_duration`: String - The time period over which the pollutant sample is averaged.
    - `arithmetic_mean`: Float - The average concentration of the parameter measured.
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
    - `sample_duration`: String -The time period over which the pollutant sample is averaged.
    - `arithmetic_mean`: Float - The average concentration of the parameter measured.
    - `units_of_measure`: String - The units used to measure the parameter.
    - `date_local`: Date - The date of data collection in the format YYYY-MM-DD.
    - `aqi`: Integer - The Air Quality Index (AQI) value.


- [**yearly_aqi_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/yearly_aqi_1964_2024.csv)
 
    This csv file contains annual AQI estimates.
  - **Fields**:
    - `year`: Integer - Year.
    - `aqi`: Float - The average AQI estimate for the year. 

- [**respiratory_illness_mortality_data.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/intermediary_files/respiratory_illness_mortality_data.csv)
 
    This csv file contains health indicator data for asthma, copd and tuberculosis.
   - **Fields**:
      - `Year`: Integer - The year for which the data is recorded.  
      - `Illness_crude_rate_asthma`: Float - The crude rate of asthma illness, calculated as the number of emergency visits or hospitalizations for asthma per population unit.  
      - `Illness_crude_rate_copd`: Float - The crude rate of COPD illness, calculated as the number of emergency visits or hospitalizations for COPD per population unit.  
      - `Cases_tb`: Integer - The total number of tuberculosis cases reported in the specified year.  
      - `Death_percent_asthma`: Float - The percentage of deaths attributed to asthma in relation to the total population.  
      - `Death_percent_copd`: Float - The percentage of deaths attributed to COPD in relation to the total population.  
      - `Death_percent_tb`: Float - The percentage of deaths attributed to tuberculosis in relation to the total population.  


#### Output Files
All these files are located under [output_files]()

- [**madison_yearly_smoke_estimate_1964_2024.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/madison_yearly_smoke_estimate_1964_2024.csv)
 
    This csv file contains annual Smoke estimates.
  - **Fields**:
    - `Fire_Year`: Integer - The year the fire occured.
    - `Smoke_Estimate`: Float - The Smoke estimate for the year.

- [**forecasted_smoke_health_metrics.csv**](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/forecasted_smoke_health_metrics.csv)
 
    This csv file contains forecasted smoke values along with forecasted health indicators.
  - **Fields**:
    - `Year`: Integer - The year of the forecast.
    - `Death_percent_asthma` : Float - Proportion of deaths caused by asthma relative to all-cause deaths.
    - `Illness_crude_rate_asthma` : Float - The number of asthma cases divided by the total population of interest.
    - `Death_percent_asthma_lower` : Float - Lower bound of the confidence interval for asthma death percentage.
    - `Illness_crude_rate_asthma_lower` : Float - Lower bound of the confidence interval for the asthma crude rate.
    - `Death_percent_asthma_upper` : Float - Upper bound of the confidence interval for asthma death percentage.
    - `Illness_crude_rate_asthma_upper` : Float - Upper bound of the confidence interval for the asthma crude rate.
    - `Smoke_Estimate` : Float - The smoke estimate of the year.
    - `Death_percent_copd` : Float - Proportion of deaths caused by COPD relative to all-cause deaths.
    - `Illness_crude_rate_copd` : Float - The number of copd cases divided by the total population of interest
    - `Death_percent_copd_lower` : Float - Lower bound of the confidence interval for COPD death percentage.
    - `Illness_crude_rate_copd_lower` : Float - Lower bound of the confidence interval for the COPD crude rate.
    - `Death_percent_copd_upper` : Float - Upper bound of the confidence interval for COPD death percentage.
    - `Illness_crude_rate_copd_upper` : Float - Upper bound of the confidence interval for the COPD crude rate.
    - `Cases_tb` : Integer - Total number of tuberculosis (TB) cases.
    - `Death_percent_tb` : Float - Proportion of deaths caused by TB relative to all-cause deaths.
    - `Cases_tb_lower` : Integer - Lower bound of the confidence interval for the number of TB cases.
    - `Death_percent_tb_lower` : Float - Lower bound of the confidence interval for TB death percentage.
    - `Cases_tb_upper` : Integer - Upper bound of the confidence interval for the number of TB cases.
    - `Death_percent_tb_upper` : Float - Upper bound of the confidence interval for TB death percentage.
    - `Smoke_Estimate`: String - The Smoke estimate for the year.

- [histogram_number_of_fires.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/histogram_number_of_fires.png) 
A histogram showing the number of fires occurring every 50 mile distance from Madison for all fires ranging up to 1800 miles away from Madison. The histogram also indicates the 650 mile distance cut-off.

- [Total_acres_burned.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/Total_acres_burned.png)
A time series graph of total acres burned per year for the fires occurring in the 650 mile radius from Madison. 

- [compare_smoke_vs_aqi.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/compare_smoke_vs_aqi.png)
A time series graph comparing the calculated fire smoke estimates for Madison and the average AQI for Madison.

- [smoke_estimate.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/smoke_estimate.png)
A time series graph showing the trends in estimates smoke for historical and the forecasted smoke for next 25 years,

- [compare_smoke_and_health.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/compare_smoke_and_health.png)
A time series graph comparing the calculated fire smoke estimates for Madison and the respiratory health indicators (illness and motality) for asthma, copd and tuberculosis.

- [smoke_health_correlation.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/smoke_health_correlation.png)
A heatmap showing the correlation of each seleced health indicator with estimated smoke to determine the effects of smoke on respiratory health.

- [smoke_impact_on_health.png](https://github.com/ManasaSRonur/data-512-project/blob/main/output_files/smoke_impact_on_health.png)
A time series graph showing the impact of smoke on respiratory health, i.e showing the forecasted trends of the health for next 25 years.


### Project Workflow

- [1_wildfire_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/1_wildfire_data_acquisition.ipynb)

  This notebook reads the wildland fire dataset from USGS, calculates the distance from Madison for each fire, filters the data for years 1964 - 2024 and generates the two csv files with selected columns. One for all the fires between the mentioned dates and one for the fires occured between these dates but within 650 mile radius from Madison.

- [2_aqi_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/2_aqi_data_acquisition.ipynb)

  This notebook is used to fetch AQI data from API, clean the data, calculate missing APIs and finally generated a csv file of yearly AQI estimates for years 1964 - 2024.

- [3_smoke_estimation.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/3_smoke_estimation.ipynb)

  This notebook utilises the files generated by the above notebooks to calculate smoke estimates and compare with AQI data to validate the calculated smoke estimates.

- [4_predictive_model.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/4_predictive_model.ipynb)

  This notebook is used to build a predictive model on smoke estimates to forecast smoke estimates for next 25 years and save these forecasted estimated to be used later for impact analysis.

- [5_visualizations.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/5_visualizations.ipynb)

  This notebook is used to analyse the data generated so far through visuals. It generated the three specific visulas as mentioned under output files.

- [6_health_data_acquisition.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/6_health_data_acquisition.ipynb)

  This notebook is used to acquire, process and analyse the respiratory illness and mortality data. It generates a combined health data file to be used to analyse the smoke correlation and impact.

- [7_extended_model.ipynb](https://github.com/ManasaSRonur/data-512-project/blob/main/7_extended_model.ipynb)

  This notebook is used to compare smoke and health metrics, analyse the correlation between them amd to build predictive model that forecasts the smoke impact on health.

### Limitations and Considerations.

- The Listed_fire_Dates includes all individual dates from merged datasets that overlap in the same area and year. This can provide more details but also adds variation and possible duplication, especially when multiple sources are involved making it unreliable.
- The tool used to measure fire distances works only with ring-shaped fire boundaries, so 36 fires with curve ring shapes failed while calculating distance and not included in analysis.
- An actual smoke impact would be based on wind direction over a course of several days, the intensity of the fire, and its duration and many other factor. However, the fire polygon data only (reliably) provide a year for each fire - it does not (reliably) provide specific start and end dates for the fire or the wind details.
- AQI value was missing for many records fetched through APIs, which were recalculated using the available pollutants data. This adds some level of uncertainity to the calculated value.
- AQI data is very sparse for years 2001 to 2009 leading poor qualirt average. This makes it difficult to compare and asses out calculation of smoke estimates for this period.
- The predictive model has R^2 value of only 0.71 which means the model explains about 71% of the variation in the data, there is still a lot of room for improvement in the model. Additionally the predicted values could be off by atleast 2 units which is significantly high for our scale of smoke estimates. While this is a fairly good model considering the data availability limitaion, this is not the best model to forecast the smoke estimate.
- Despite having access to smoke data spanning the last 60 years, a significant limitation is the relatively shorter temporal range of healthcare data, particularly hospitalization records, which are available only from 2000 to 2023 for asthma and COPD, and from 2014 - 2023 for TB. The lack of overlapping historical data limits our ability to examine the health impacts of smoke exposure with the same depth as our smoke data. Ideally, aligning both datasets temporally would have enabled a more comprehensive analysis.
- County-specific mortality rate data is unavailable, compelling us to use aggregate data for the entire state of Wisconsin. By relying on statewide data, we risk obscuring local trends and nuances in mortality that might otherwise reveal significant insights. This limitation could lead to correlation errors and impact the precision of our findings regarding the health effects of smoke specifically in Madison, Dane county.
- The extended model although seems effective, there is room to further improvement in the Asthma and COPD models, particularly by reducing RMSE through addiiton of more features and increasing overall size of training data.
- Other confounding variables, such as existing health conditions, dietary habits, exposure to toxic gases from other sources, etc., are not considered for forecasting the health indicators for future years. So this analysis alone might not provide an informed decision.
- The entire analysis in this notebook is based on wildfires in the USA, but Madison is constantly impacted by wildfires in Canada every year due to its geographical location. So we might miss the dominant contributors to poor air quality, leading to weaker than expected correlations with respiratory health trends.


### Conclusion

This study examined the impact of wildfire smoke on respiratory health outcomes in Madison, Wisconsin, with the hypothesis that increasing levels of smoke exposure correlate with a rise in respiratory illnesses, hospitalizations, and potentially mortality rates, particularly for asthma, COPD, and tuberculosis. The findings strongly support this hypothesis, revealing a significant positive correlation between smoke exposure and the incidence of asthma and COPD. While the relationship between smoke and tuberculosis was less pronounced, COPD mortality showed a notable connection to smoke levels, whereas asthma and tuberculosis mortality were more influenced by systemic factors such as healthcare access and preexisting conditions. Projections suggest a steep rise in respiratory illnesses over the coming decades if current trends in wildfire smoke continue unabated.

Beyond the statistical findings, this study exemplifies how data science can serve as a bridge between complex environmental data and real-world health outcomes. It underscores the importance of ethical considerations and a human-centered approach, ensuring that the research is not only robust but also aligned with the broader goal of improving quality of life. The conclusions offer valuable guidance for policymakers, healthcare providers, and urban planners in developing strategies such as enhancing air quality monitoring systems, preparing healthcare infrastructure for increased respiratory care demand, and raising public awareness about protective measures. This research reaffirms the potential of data-driven approaches to foster equitable, informed, and community-focused responses to pressing public health challenges.
