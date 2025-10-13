# databricks-demo-stravadata

Databricks demo project with my [Strava](https://www.strava.com/dashboard) activity data. 

Currently this pipeline filters the activities only to those Walk, Run, Ride, and Nordic Ski activities that certain columns (not NULL). The total number of these activities is around 1700 as of Oct 2025. An example machine learning problem to apply here could be to try and predict the sport type based on predictor variables like average speed, duration, date, elevation gain, and weather data.

## Content

- `setup` contains code for creating the catalog, schemas, and a landing volume
- `pipeline` contains the actual pipeline code, using the Medallion architechture
- `explorations.ipynb` is a notebook for studying the data in different phases of the pipeline

## Data flow

1. Raw `activities.csv` file is dropped into the landing volume. This I have obtained by exporting my data from Strava. In a real pipeline this manual part could be replaced by integration with the Strava API, so that the data is autoloaded, possibly incrementally.
2. Bronze transformations handle csv reading, and sanitizing the column names of the activities.
3. Silver transformations select certain columns, creates new columns, handles de-duplication and drops rows with NULL values.
4. Gold transformations produce data summaries that reveal insights.

## Data insights

The summaries can answer questions like

- What is my average speed for each sport type?
- Which sport is my most common activity type in February?
- Which sport has the most uphills?


