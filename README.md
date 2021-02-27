# Fair_Weather_Cyclists

*Does weather impact Citi Bike ridership in New York City?*

<p align="center">
  <img width="650" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rider_in_the_rain.jpg">
</p>

New Yorkers are supposed to be tough. They're supposed to be resilient. They're supposed to be like this guy in a suit and tie riding a bike through the East Village in the rain. But I must confess, that even as a New Yorker with a deep love for my two-wheeled machine, I am a fair-weather cyclist. 

This is the kind of week I love to spend in the saddle. It's the middle of September 2020. It's balmy (red line), humdity is low (yellow line), and there is absolutely no rain (brown line). And during this week, New Yorkers hopped on a Citi Bike and took a ride 413,223 times (blue line).  

<p align="center">
  <img width="600" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/great_bike_week.png">
</p>

It was a welcomed week at the tail end of Summer's dog days where, like this Wednesday from August, the air was thick and hot and gave the city it's rainiest hour of the year. And although 66,069 braved the opprresive elements, the graph clearly shows that as rain began to fall in the late afternoon, ridership plummeted. 

<p align="center">
  <img width="600" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rainy_day.png">
</p>

Am I not the only fair-weather cylcist in New York City? Do others who love to ride also hate the feeling of a water logged shoes and streaks of mudd running up their backs? Is there a statistically significant link between bike ridership and weather events like rain, temperature and humidity in New York City?

----

### The Data

To infer any possible links betwen ridershiip and weather, I turned to Citi Bike's [public system data](https://www.citibikenyc.com/system-data) and hourly Integrated Surface Data from the [National Centers for Environmental Information](https://www.ncei.noaa.gov/access/search/index). Both datasets are easily accesible via the respective organization's websites, althought a public S3 bucket and an API are also availible. 

**Citi Bike**

The entire dataset contains nearly every ride taken in the system since June 2013 (Citi Bike removes trips taken by working staff, trips to/from "test" stations and trips shorter than 60 seconds). For my test, I focused on 2020, the most recent full year availible, with the following specifications:

  * Nearly every ride taken in New York City during 2020 (Citi Bike removes rides by woking staff and rides shorter than 60 seconds)
  * 19.5+ million data points.
  * Columns for trip duration, start/end time and date, start/end station, station name/id/lat/long, bike id, user type, gender and birth year.

**Weather**

NCEI's Integrrated Surface Data is availible via its website or an API and comes in a variety of customizable measurements and frequencies. For this project, I downloaded:

  * Hourly data measured at the Central Park weather station for all of 2020.
  * 8,700 + data points after removing weekly/montly summaries and other non-regular reports.
  * Columns included air temperature, dew point, liquiid precipitation, wind gusts, and sky cover conditions.

---

**Issues to Consider**

*COVID-19*

As we all know, the world was greatly impacted by the COVID-19 pandemic in 2020, and New York City was no exception. In particular, the pandemic influenced both the need for and choice of transportation options. This test is not meant as a study of COVID-19's impact on Citi Bike and any potential impact is not considered. A rough chart of daily ridership does show a dip in ridership beginning in early spring, about the time the pandemic took over the city, and a surge in late summer The extent of the pandemic's impact on these trends cannot be determined without further investigation. 
   
<img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/daily_trips_2020.png" width="400"> 
<img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/outliers.png" width="400">     
   
*Unrealistic outliers*

During EDA, charts of temperature and dew point against time showed a handfull of unrealisstic measurments above 1,800 degrees fahrenheit. Twenty-seven of these measurements were found for dew point and 25 for temperature. None were sequential, except for a single pair of dew points. Because weather measurements were made every hour and ride start times were recorded down to the second, a single weather measurement was associate with thousands of rides. This made simply dropping the outliers an unappealing option. To deal with the outliers, I averaged the measurements in the hour before and the hour after as an estimate for the hour in quesiton. 

*Dew Point = Humidity*

This test relies on dew point as a measurment for humidity. According to the National Oceanic and Atmospheric Association, "If you want a real judge of just how 'dry' or 'humid' it will feel outside, look at the dew point instead of the rerlative humidity. The higher the dew point, the muggier it will feel." The assocaition suggests the following ranges:

  * less than or equal to 55: dry and comfortable
  * between 55 and 65: becoming "sticky" with muggy evenings
  * greater than or equal to 65: lots of moisture in the air, becoming oppressive

<br /> 

<p align="center">
  <img width="200" src="https://d21xlh2maitm24.cloudfront.net/nyc/Citi-Bike-provided-by-Lyft-Positive-170x57px.svg?mtime=20201023151104">
  <img width="200" src="https://d32ogoqmya1dw8.cloudfront.net/images/nesta/about/noaa_logo.v2.jpg">
</p>

----

### The Data: Exploration

Temperature, dew point and rain were all plotted against rides/hour. The goal was to estimate reasonable segmentation points so that the data could be grouped into sub-populations for comparison. For this first pass at my test, two subpopulations for each weather condition were created. Based on experience, recomendations from experts, and the resulting plots, conditions were split into the following groups with resulting sizes: 

  * <b>Rain:</b> No rain (=0mm): 8,033 vs. Any rain (>0mm): 679
  * <b>Temperature:</b> Cool (<75F): 4,854 vs. Hot (>=75F): 3,858
  * <b>Dew Point:</b> Low (<=55F): 5,927 vs. High (>55F): 2,785


<img align="left" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rides_temp_dot.png" width="400"> <img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rides_rain_dot.png" width="400"> 

<br />  

---

### The Test

Does weather impact Citi Bike ridership in New York City?

Null hypothesis:

  * Ho: Ridership is unaffected by weather conditions such as temperature, humidity, and rain

Alternative hypothesis:

  * Ha: Ridership will decrease based on high measurements of temperature, humidity, and rain

Welch’s t-test, given the large population size and unequal variance

Alpha: 0.05
0.0167 with a Bonferroni correction for three tests 

----

### The Results 


Dew = pvalue=9.780001451639427e-75

Rain = pvalue=2.293253491572896e-53

Temp = pvalue=1.9517356662769365e-207



**Future Avenues**

The dataset is dense and rich with many more avenues to explore. Attributes including gender, age, geography, customer type, and other additional weather conditions could be explored to further refine these findings or answer other questions.
Parse the data further
moderate weather conditions
seasons
time of day 

Other attributes
age 
geography 
gender 

Additional year

----

### The Tech


<img align="left" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/600px-Pandas_logo.svg.png" width="200"> 

<img align="right" src="https://matplotlib.org/stable/_static/logo2_compressed.svg" width="200">

<p align="center">
  <img src="https://cdn.icon-icons.com/icons2/2415/PNG/512/python_original_logo_icon_146381.png" width="100"/> 
</p>

