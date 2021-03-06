# SQLAlchemy Surfs Up Project

![](Surf.gif)

For this project I took a SQLite dataset about Honolulu, Hawaii and with SQLAlchemy in Python ran a climate analysis on it. 

1. First I utilized SQLAlchemy create_engine to connect to the sqlite database.


2. I then used SQLAlchemy automap_base() to reflect my tables into classes and save a reference to those classes called Station and Measurement.


3. I then linked Python to the database by creating an SQLAlchemy session.

**Precipitation Analysis**

1. First I started by finding the most recent date in the data set.


2. Using this date, I then retrieved the last 12 months of precipitation data by querying the 12 preceding months of data. Note you do not pass in the date as a variable to your query.


3. I then narrowed the query results down to just the date and prcp values.


4. I then loaded the query results into a Pandas DataFrame and set the index to the date column and sorted the values by date.


5. I then utilized MatPlotLib to plot the results using the DataFrame plot method.

![](hist2.png)

6. Lastly, I used Pandas to calcualte the summary statistics for the precipitation data

**Exploratory Station Analysis**

1. For this analysis I first designed a query to calculate the total number of stations in the dataset.


2. Next I designed a query to find the most active stations (i.e. which stations have the most rows?). To do this I first listed the stations and observation counts in descending order. Then I calculated which station id has the highest number of observations. Using the most active station id, I then calculated the lowest, highest, and average temperature.


6. Next I designed a query to retrieve the last 12 months of temperature observation data (TOBS) and filter by the station with the highest number of observations. I ploted the results as a histogram.

![](hist.png)

**Flask API Climate App**

For the next step in this project I designed a Flask API based on the queries that I have just listed above.

I created routes for the app.

1. Home page that lists all the routes avalable

2. For the percipitation route I converted my query results to a dictionary using date as the key and prcp as the value. I then returned a JSON version of this dictionary.

3. For the stations route I returned a JSON list of stations from the dataset.

4. For the TOBS route I first queried the dates and temperature observations of the most active station for the last year of data. Then I returned a JSON list of temperature observations (TOBS) for the previous year.

5. I then created a start route that takes a start date and returns a MIN temp, AVG temp, and MAX temp for all dates greater than and equal to the start date.

6. I also created a start end route that takes both a start and end date and for dates between the start and end date inclusive returns a MIN temp, AVG temp, and MAX temp.

**Temperature Analysis**

I then went back to my Jupyter notebook and with Pandas preformed a Temperature Analysis on the stations in Hawaii.

1. To Do this I first converted the date column format from string to datetime, set the date column as the DataFrame index, and droped the date column.

2. Next Step in my temperature analysis of Hawaii weather stations was to identify the average temperature in June and December at all stations across all available years in the dataset. The obpjective here was to discover if there is a meaningful difference between the temperature in June and December.

3. I then used an independend t test because a paired t test requires equal sample sizes which we dont have, to determine whether the difference in the means, if any, is statistically significant.

FINDINGS: The pvalue here is really small so the probability that the means of these two sets are diferant by chance is really small meaning we reject the null hypothesis.

4. I also looked at the historical weather of the dates August first to August seventh to find out what the temperature has previously looked like.

5. I then utilized a function that will take the input of a year month and date in the %Y-%m-%d format, and returns the minimum, average, and maximum temperatures for that range of dates.

6. I then used this function to get results for the previous year

7. I then ploted the min, avg, and max temperature from my previous year query as a bar chart.


