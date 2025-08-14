# New York City Citi Bike Ride Analysis

## Summary
This Tableau visualization project involved analyzing data from the New York Citi Bike program to generate reports for city officials, aiming to improve program publicity and performance. By aggregating trip history logs and identifying unexpected phenomena, visualizations and dashboards will be created in Tableau to provide insights into ridership patterns, station popularity, and other relevant metrics.

[View My Tableau Dashboard Visualizations here](https://public.tableau.com/views/2023_Quadrimester1_Analysis/StoryDashboard?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## Data Source:
The Data that was used for this analysis was ride data from the Citi Bike Data webpage https://www.citibikenyc.com/system-data. The timeframe selected (January through April 2023, four months of data) aligns with the lesser-known term ["first quadrimester"](https://en.wikipedia.org/wiki/Calendar_year) of the year.

Connections began by importing and performing a Union on the following files:<br/>
JC-202301-citibike-tripdata.csv<br/>
JC-202302-citibike-tripdata.csv<br/>
JC-202303-citibike-tripdata.csv<br/>
JC-202304-citibike-tripdata.csv<br/>

The Citi Bike csv files natively provided only 2 time relevant columns `started_at` and `ended_at`, meaning multiple intermediary calculated fields needed to be coded in order to view `Length of Trip` and `Average Trip Length`, both of which required breaking out columnar data by seconds, then minutes, then hours, which each proceeding field dependent on the one created prior (hours dependent on minute, minute dependent on seconds).

Creating these Calculated Fields was surprisingly one of the most time-intensive aspects of the project- all to viewe something as unsuspectingly simple as trip length and average trip length!

I created these 5 Calculated Fields created in order to see `Trip Duration` by `Ride ID`:

* =# Total Trip in Seconds<br/>
DATEDIFF('second', [Started At], [Ended At])

* =Abc Total Seconds Diff<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds]%60)),2)

* =Abc Total Minutes Diff<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds]%3600/60)),2)

* =Abc Total Hour Diff<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds]/3600)),2)

* =Abc Trip Duration<br/>
[Total Hour Diff] + ':' + [Total Minute Diff] + ':' + [Total Seconds Diff]

I created these 5 additional Calculated Fields to see Average Trip Length amongst all riders:

* =# Total Trip in Seconds - Avg<br/>
AVG(DATEDIFF('second', [Started At], [Ended At]))

* =Abc Total Seconds Diff – Avg<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds - Avg]%60)),2)

* =Abc Trip Duration - Avg<br/>
[Total Hour Diff - Avg] + ':' + [Total Minute Diff - Avg] + ':' + [Total Seconds Diff - Avg]

* =Abc Total Minute Diff – Avg<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds - Avg]%3600/60)),2)

* =Abc Total Hour Diff – Avg<br/>
RIGHT("0" + STR(FLOOR([Total Trip in Seconds - Avg]/3660)),2)
