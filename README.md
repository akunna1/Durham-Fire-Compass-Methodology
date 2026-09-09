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
* Dropped records with invalid dates or times — Records where Alarm Date and Alarm Time could not be converted into a valid date/time were excluded from the analysis.
* Extracted time attributes — For each valid incident, I extracted the month, weekday, and hour from the alarm date/time and kept the recorded shift.
* Grouped incidents by time and shift — Incidents were grouped and counted by month, weekday, hour, and shift.
* Prepared and analyzed incident classifications — Loaded the cleaned CSV, counted incidents by Incident Type Group for the radar chart, and broke each group down into its individual Incident Types with their respective counts.
* Broke down incident types by group — Grouped each individual Incident Type under its Incident Type Group and counted how many times each type
* Created a heatmap of incident density — Loaded incident latitude and longitude coordinates, removed records with invalid coordinates, and plotted the remaining incidents as a heatmap where blue indicates lower activity and red indicates the most intense concentrations.

## Coverage
## Coverage

### Input Data

The Coverage page uses `Compass_Data_1_Cleaned.csv`, which contains incident response-time, location, station, shift, and incident type group information.

Station locations are loaded separately from `Fire_Stations_Geocoded.csv`. The Durham City boundary is loaded from `durham_city.geojson`.

### Coverage Analysis
* Filtered invalid response-time and location records — Only incidents with a valid Dispatch Total Response Time, Latitude, and Longitude were included in the coverage analysis.
* Calculated average response time — Calculated the average first-unit response time for all incidents and for the selected Incident Type Group.
* Classified response times — Incidents were categorized as **Fast (≤5 minutes)**, **Moderate (5–8 minutes)**, or **Slow (>8 minutes)**.
* Calculated coverage metrics — Counted incidents in each response-time category and used these counts to display Fast Coverage and Weak Coverage (>8 minutes).
* Created response-time distribution — Displayed the number of incidents in each response-time category using a line chart.
* Added Incident Type Group filtering — Allowed users to filter the coverage analysis by Incident Type Group while updating the response-time metrics and map.
* Mapped response performance — Plotted incidents on the map using their latitude and longitude and displayed them according to their response-time category.
* Identified weak coverage areas — Highlighted incidents with response times greater than 8 minutes to help identify locations with slower response performance.
* Mapped fire stations — Added geocoded fire station locations and station labels to the map.
* Added station service-radius buffers — Added interactive 3-, 5-, and 7-mile buffers around each fire station to provide geographic context for station coverage.
* Added Durham City boundary — Overlaid the Durham City boundary to provide geographic context for incident locations and station coverage.


## Stations

## Apparatus

## Community

## Scenarios
Additional cleaned datasets are used by the **Scenarios** page and are generated using the second pyhton code to create `Compass_Data_2_Cleaned.csv`, `Compass_Data_2a_Cleaned.csv`, and `Compass_Data_2b_Cleaned.csv`.
