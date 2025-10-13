# databricks-demo-stravadata

Databricks demo project with my [Strava](https://www.strava.com/dashboard) activity data. 

Currently this pipeline filters the activities only to those Walk, Run, Ride, and Nordic Ski activities that have certain columns available (not NULL). The total number of these activities is around 1700 as of Oct 2025. *NOTE:* This currently does not use Delta Live Tables.

## Content

- `setup` contains code for creating the catalog, schemas, and a landing volume
- `pipeline` contains the actual pipeline code, using the Medallion architechture
- `exploration.ipynb` is a notebook for studying the data in different phases of the pipeline
- `dashboard.lvdash.json` is a dashboard that can be viewed in Databricks. Below is an example of the dashboard that I made with the Databricks editor.

![dashboard](db.png)

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


An example machine learning problem to apply here could be to try and predict the sport type based on predictor variables like average speed, duration, date, elevation gain, and weather data.
