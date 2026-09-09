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
* Grouping incidents by time and shift — Incidents were grouped and counted by month, weekday, hour, and shift.
* Prepared and analyzed incident classifications — Loaded the cleaned CSV, counted incidents by Incident Type Group for the radar chart, and broke each group down into its individual Incident Types with their respective counts.
* Broke down incident types by group — Grouped each individual Incident Type under its Incident Type Group and counted how many times each type
* Created a heatmap of incident density — Loaded incident latitude and longitude coordinates, removed records with invalid coordinates, and plotted the remaining incidents as a heatmap where blue indicates lower activity and red indicates the most intense concentrations.

## Coverage

## Stations

## Apparatus

## Community

## Scenarios
Additional cleaned datasets are used by the **Scenarios** page and are generated using the second pyhton code to create `Compass_Data_2_Cleaned.csv`, `Compass_Data_2a_Cleaned.csv`, and `Compass_Data_2b_Cleaned.csv`.
