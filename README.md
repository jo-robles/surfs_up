# Analysis for Surfs_Up

# Overview

For our client - W.Avy, and his interest in opening up a surf shop in Oahu, we retrieved temperature data for both the months of June and December over a period 7 years. This data will be utilized to make a determination of the feasibility of opening up a surf shop for W. Avy year-round.

# Resources Utilized

* Jupyter Notebook
* SQL
* SQLAlchemy
* Pandas
* Python
* Hawaii.sqlite

# Results

To begin the analysis, after importing our dependencies, we began by creating our engine and reflecting the tables into our Jupyter Notebook:

```
engine = create_engine('sqlite:///hawaii.sqlite')
Base = automap_base()
Base.prepare(engine, reflect = True)
```

Saving references to our tables:

```
Measurement = Base.classes.measurement
Station = Base.classes.station
```

And finally, creating a link from Python to our databases:

```
session = Session(engine)
```

From there, by utilizing SQLAlchemy, we created the following queries to pull data for both June and December from our SQLite file:

```
june_temps = session.query(Measurement.tobs).filter(extract('month', Measurement.date)==6)
december_temps = session.query(Measurement.tobs).filter(extract('month', Measurement.date)==12)
```

With these steps completed, we were able to transform these queries to lists, and then to Pandas Dataframes to perform a statiscial analysis on both months utilizing the ```describe()``` function. From this, we note the three following key differences in weather between June and December:

* Counts
    * The ```describe()``` function notes the following counts of temperature observations:

        * June - 1700
        * December - 1517
        
    As both June and December are 1 day apart in terms of length (e.g., June has 30 days and December has 31), there does seem to be a question of why there are less observations for the month of December. Further analysis would be warranted to determine root causes or to determine if the differences would be enough to be considered significant.  

* 50th percentile and Min

    The ```describe()``` function notes the following differences between the 50th percentile in temperatures recorded:

    * June:
        * 50th Percentile - 75.0
        * Min - 64.0
        
    * December
        * 50th Percentile - 71.0
        * Min - 56.0 
    
    From here, we can put the range of temperature range for both months as:
    
    * June : 11 degrees
    
    * December: 15 degrees
    
    Ultimately not only do we see lower temperatures for the month of December, we also see a slightly larger range of temperatures for the month of December as well.

* Averages

    The ```describe()``` function notes the following average temperatures:
    
    * June: 74.944
    
    * December: 71.042
    
    At a glance, we do not notice much difference in the average temperatures between the two months. However, when looked at in context of the other data provided above, we notice that the averages simply do not provide enough of an in-depth view to make a definitive statement.

# Summary

Overall, the results of the analysis show some slight variations between the month of June & December. Unfortunately, with the data provided, it would be difficult to provide a definitive answer to whether the business would be sustainable year-round. However, additional queries could certainly provide some further insight:

* Precipitation totals for the months of June and December
    * While we understand the temperature variations, determining how much precipitation is present could certainly provide greater context to the overall picture. 
    
* Station Information
    * At the moment, additional queries into why there are fewer obervations for the months of December as compared to June would be warranted. To do so, querying the stations that are reporting for each month could provide some insight into how the data is gathered. 

