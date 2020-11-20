![logo](./Resources/logo.png)
# Surf n' Shake Shop: Investor Analysis

## Overview
Wanting to fufil my dream of living...*and making a living*... in Hawaii, I have reached out to investor, W. Avy, to help finance the launch of my business, the **Surf n' Shake** shop, a place you can get all your surfing and ice cream needs met on the island of Ohau!

While W. Avy loved the idea (being a surfer himself) and the proposal, he did have concerns about the weather. To address his concerns, we initially analyzed the previous year's precipiation; now, he would like to go further and include information about temperature trends before deciding on if (and when) to open the surf shop. 

### Objective
Specifically, W. Avy would like to see statistical temperature data for **June** and **December** from the **weather dataset he has provided** to determine if the surf and ice cream shop business can be sustained throughout the year.

However, that's not all the information W. Avy will be getting from me; making the right decision on if, and when, to open for business is too important!

## Analysis

###Resources
The weather dataset W. Avy provided is a **SQLite** database, **hawaii.sqlite**, and is located in this repository.  

The data consisits of daily persipitation and daily temperatures for the years 2010 - 2017 from weather stations.  Not all weather stations report every day.

The data is accessed and analyzed using Python code written in a Jupyter Notebook and accessing several modules and imports, including:  

* numpy
* pandas
* sqlalchemy
	* from sqlalchemy.ext.automap import ```automap_base```
	* from sqlalchemy.orm import Session
	* from sqlalchemy import ```create_engine```, func

### Analysis
After using the ```create_engine``` function to establish a link and create a session to connect to the SQLite database, reflecting the existing database into a new model, reflecting the tables, and saving the references to each table, the queries are relatively simple to execute for June and December:
```results_jun = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date) == '06').all()```
```results_dec = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date) == '12').all()```

Getting the summary statistics using ``.describe()`` is also relatively simple once the list of temperatures are converted from a list to a dataframe.

## Results
The temperature data provided in **hawaii.sqlite** included daily statsitics for June vs December Temperatures
![temps](./Resources/june_dec_temps.png)

Items to note from these results:

1.  The **difference in minimum temperature** between June (summer equinox) and December (winter equinox) is only **8 degrees**
2.  The **difference in maximum temperature** is even less, only **2 degrees**
3.  Not surprisingly, the **average temperature differs by only 3.8 degrees**.  
4. However, looking at the distribution of the temperatures, it appears that December has well over 50% of it's daily temperatures 73 degrees and below, while June has only 25%. 
![temps2](./Resources/jun_dec_hist.png)

Let's dig a little deeper into the number of warm, surfable days in June and December...and how about the preciptation in these months?  Chilly and rainy is not good for business!

## Next Steps
Merging the perciptation data with the daily temperature, we can get an idea of how many days are raining and/or cool (below 73 degrees) that would make decrease the demand for ice cream and/or surfing!


 
There is a high-level summary of the results and there are two additional queries to perform to gather more weather data for June and December. (5 pt)