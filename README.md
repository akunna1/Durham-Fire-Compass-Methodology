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

## Community

## Scenarios

Additional cleaned datasets are used by the **Scenarios** page. These datasets are generated using the second Python script and include:

* `Compass_Data_2_Cleaned.csv`
* `Compass_Data_2a_Cleaned.csv`
* `Compass_Data_2b_Cleaned.csv`
