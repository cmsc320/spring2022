# Project 4

Posted: April 28, 2022

Due: May 6, 2022 at 11:59pm EDT

## Aims

The aim of this project is to introduce the use of maps for visualizing data.
Finding some subset of the data that can be presented reasonably and
comprehensibly is the most important aspect of the project.

If you find yourself spinning your wheels for a significant amount of time.
There is something wrong, reach out to course staff.

## Part 1: Getting some Data

You'll need to find a dataset that include latitude and longitude information.
Many datasets have this information, possible places to start looking:

* Open data initiatives for the state you're from (e.g. opendata.maryland.gov)
* Crime and arrest data for a particular city
* Traffic data

As an example, I will be using vehicle crash data for the state of Maryland.

```{python}
import folium
import requests
import pandas

crash_table = pandas.read_csv("https://cmsc320.github.io/files/Baltimore_City_Vehicle_Crashes.csv")

crash_table

```

We can see that the table for this dataset has 135590 rows. Let's see if we
have a location for each of those rows:

```
crash_table[pd.notnull(crash_table["LOCATION"])]["LOCATION"].count()
```

In our case we have a location for every row of our dataset! No need to
worry about missing values.


## Part 2: Making a Map

Folium provides a python interface for [leaflet.js](https://leafletjs.com/).
Leaflet.js is a Javascript library for interactive maps, and can be useful to
know on its own. The benefit of using this library via Folium is that Folium
makes it very easy to use from within a Jupyter Notebook and to access your
python data-structures (e.g.  Pandas DataFrames).

The documentation for Folium can be found on its official website:
[https://python-visualization.github.io/folium/](https://python-visualization.github.io/folium/).
You will likely need to consult the documentation in order to complete this
project.

The following code will create a map centered on Baltimore:


```{python}
map_osm = folium.Map(location=[39.29, -76.61], zoom_start=13)
map_osm
```

Note: it is common to see the `osm` suffix because leaflet.js uses
OpenStreetMap.

## Part 3: Combining Parts 1 and 2

Use markers, [as described in the
documentation](https://python-visualization.github.io/folium/quickstart.html#Markers)
to mark information from your dataset. The task for this project is to come
up with a way to differentiate the data marked on the map. If all crashes
(or whatever your data is about) use
the same marker type, the map will be near meaningless. The columns in
your dataset will be a good first step, but you'll likely want to only
differentiate among a subset of the columns.

For example, with my Baltimore City Vehicle Crash dataset, I looked at the
columns available to me:

```
crash_table.columns
```

And saw that there was a column for "WEATHER_DESC", so I might want to do
something with showing the crashes under different weather conditions. For
example, the following code would place a red marker for crashes that
happened under "WEATHER_DESC" == "Snow" and a blue marker for "WEATHER_DESC"
== 'Severe Winds' (notice the additional mention of `map_osm` at the end, so
that I can see the updated map):

```
for index, crash in crash_table[crash_table["QUARTER"] == "Q1"].iterrows():
    if crash["WEATHER_DESC"] == "Foggy":
        folium.Marker(location=[crash["LATITUDE"], crash["LONGITUDE"]],
                    icon=folium.Icon(color='red')).add_to(map_osm)
        
    if crash["WEATHER_DESC"] == 'Severe Winds':
        folium.Marker(location=[crash["LATITUDE"], crash["LONGITUDE"]],
            icon=folium.Icon(color='blue')).add_to(map_osm)
map_osm 
```

The choice of how you differentiate the data should prioritize the following:

* Are you able to visually interpret the data?

Even if different data points use different markers, if the map is fully
covered by markers it will not be a useful map. Consider ways to restrict which
data points are shown, I did that above by looking only at the first quarter
of the year (`crash_table["QUARTER"] == "Q1"`).

## Submission:


Your submission must include the following:


1. the code to carry out each of the steps above

2. An explanation of your chosen dataset

2. output showing the result of your code (in this case the interactive map)

3. a short prose description of your interactive map (i.e., what are you
showing with this data and map). Remember, the writeup you are preparing is
intended to communicate your data analysis effectively.  Thoughtlessly showing
large amounts of output in your writeup defeats that purpose.

This should be submitted on ELMs in the usual way, for this project we only
require the .ipynb and .html, no need for a PDF.
