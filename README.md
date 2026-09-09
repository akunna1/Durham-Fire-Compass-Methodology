# Durham Fire Compass — Data & Methodology

This guide documents the data sources, analysis, and methodology used to develop Durham Fire Compass.

## Demand 

### Input Data

The primary dataset for this page is `Compass_Data_1_Cleaned.csv`.

The original incident data was obtained from **ESO Suite** and processed using Python scripts in the [Durham Fire Compass Data Cleaning repository](https://github.com/akunna1/Durham-Fire-Compass-Data-Cleaning).

The cleaned dataset contains information including:

* Alarm date and time
* Incident number
* Incident type and incident type group
* Latitude and longitude
* Shift
* Station
* Battalion
* EMS and suppression apparatus counts
* Apparatus type
* Dispatch total response times
* On-scene time
* Total incident duration

### Demand Analysis

* **Input data and filtering** — Used `Compass_Data_1_Cleaned.csv` and excluded records where Alarm Date and Alarm Time could not be converted into valid date/time values. Invalid latitude and longitude records were also excluded from the incident density analysis.
* **Time-based analysis** — Extracted month, weekday, hour, and shift and counted incidents across these time periods.
* **Incident classification analysis** — Counted incidents by Incident Type Group and grouped individual Incident Types under their corresponding Incident Type Group.
* **Interactive filtering** — Selecting a month, weekday, hour, or shift filters the other demand charts to the selected criteria.
* **Incident density mapping** — Created a heatmap using incident coordinates, with lower activity shown in blue and higher concentrations shown in red, and overlaid the Durham City boundary.

## Coverage

### Input Data

The Coverage page uses `Compass_Data_1_Cleaned.csv`, `Fire_Stations_Geocoded.csv`, and `durham_city.geojson`.

### Coverage Analysis

* **Input data and filtering** — Used `Compass_Data_1_Cleaned.csv` and excluded incidents without a valid Dispatch Total Response Time, Latitude, or Longitude. Fire station locations were loaded from `Fire_Stations_Geocoded.csv`, and the Durham City boundary was loaded from `durham_city.geojson`.
* **Response-time analysis** — Calculated average first-unit response time and classified incidents as **Fast (≤5 minutes)**, **Moderate (5–8 minutes)**, or **Slow (>8 minutes)**.
* **Coverage metrics** — Counted incidents within each response-time category and calculated Fast Coverage and Weak Coverage (>8 minutes).
* **Interactive filtering and mapping** — Allowed filtering by Incident Type Group and updated the response-time metrics and map accordingly.
* **Coverage visualization** — Displayed response-time distributions, incident locations, weak coverage areas, fire stations, 3-, 5-, and 7-mile station buffers, and the Durham City boundary.

## Stations

### Input Data

The Stations page uses `Compass_Data_1_Cleaned.csv`, focusing on station, battalion, shift, and response-time data.

### Stations Analysis

* **Input data and filtering** — Used `Compass_Data_1_Cleaned.csv` and excluded records without a valid Dispatch Total Response Time or Station.
* **Station and battalion analysis** — Calculated incident volume and average response time for each station and battalion and identified the busiest and fastest.
* **Shift and cross-filtering** — Allowed filtering by Shift A, B, or C and selecting a station or battalion to update related metrics.
* **Performance visualization** — Displayed station and battalion incident volume and average response time using interactive bar charts.

## Apparatus

### Input Data

The Apparatus page uses `Compass_Data_1_Cleaned.csv`, focusing on Incident Type Group, Suppression Apparatus Count, Apparatus Type, and Total On Scene Time.

### Apparatus Analysis

* **Input data and filtering** — Used `Compass_Data_1_Cleaned.csv` and excluded records without an Incident Type Group or valid Total On Scene Time. Missing Suppression Apparatus Count values were treated as zero, and missing Apparatus Type values were classified as `Unknown`.
* **Suppression apparatus analysis** — Calculated the average number of suppression apparatus deployed for each Incident Type Group.
* **Apparatus distribution analysis** — Counted apparatus types within each Incident Type Group and displayed the results in a pivot-style heatmap table.
* **On-scene time analysis** — Grouped incidents into on-scene time ranges from 0–10 minutes through 60+ minutes and calculated the average suppression apparatus count for each range.
* **Visualization** — Displayed suppression apparatus deployment and on-scene time relationships using interactive bar charts and a heatmap table.


## Community

### Input Data

The Community page uses multiple datasets and geographic files:

* `Compass_Data_1_Cleaned.csv` — incident data from ESO Suite
* `pop_incidents.csv` — census tract population and incident-rate data
* `zone_incidents_summary.csv` — zoning, land-area, and incident-rate data
* `durham_tracts_pop.geojson` — census tract boundaries and population
* `durham_zoning_cleaned_1.geojson` — zoning boundaries and classifications
* `durham_city.geojson` — Durham City boundary

### Community Analysis

* **Input data and filtering** — Used the population and zoning datasets for the analysis. Population records with invalid numeric values were excluded, while zoning records without a valid zoning classification, land-area value, or incident rate were excluded. Geographic layers were loaded from the corresponding GeoJSON files.
* **Population and incident-rate analysis** — Compared census tract population with incident rates per 1,000 residents and calculated a linear regression and R² value to measure the strength of the relationship.
* **Land-use and incident-rate analysis** — Compared zoning classifications and land area with incident rates per 100 acres. Total acres were log-transformed to reduce the effect of large differences in zone size.
* **Mapped community characteristics** — Mapped population by census tract and zoning classifications using interactive geographic layers, with an optional Durham City boundary overlay.
* **Visualized relationships and interpretation** — Used scatter plots, regression lines, zoning/population maps, and explanatory summaries to examine how population, land area, and land use relate to incident patterns.


## Scenarios

### Input Data

The Scenarios page uses:

* `Compass_Data_2_Cleaned.csv` — incident locations and Incident Type Groups
* `Compass_Data_2a_Cleaned.csv` — average response time by Incident Type Group
* `Compass_Data_2b_Cleaned.csv` — average response time by station
* `Fire_Stations_Geocoded.csv` — fire station locations and physical addresses
* `durham_city.geojson` — Durham City boundary

The Compass_Data_2 files were generated using the second python code found in [Durham Fire Compass Data Cleaning repository](https://github.com/akunna1/Durham-Fire-Compass-Data-Cleaning).

### Scenarios Analysis

* **Input data and filtering** — Loaded the three cleaned CSV datasets and excluded incidents with invalid or zero latitude/longitude coordinates. Station and response-time records were converted to numeric values for mapping and dispatch calculations.
* **Station inventory and response planning** — Used editable station apparatus inventory and incident-type response plans to determine which apparatus are available for each scenario.
* **Dispatch eligibility and prioritization** — Checked apparatus availability first, then evaluated stations within 3-, 5-, and 7-mile buffers. Eligible stations were prioritized using the lowest calculated station–incident response time.
* **Response-time calculation** — Calculated station–incident response time as the average of the selected station's average response time and the average response time for the incident's type group.
* **Scenario simulation and mapping** — Simulated dispatch behavior as inventory or response-plan values change and displayed the active incident, eligible/dispatched stations, coverage buffers, and mutual-aid status on the map.
