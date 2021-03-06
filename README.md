# Fair_Weather_Cyclists

*Does weather impact Citi Bike ridership in New York City?*

<p align="center">
  <img width="650" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/fair_weather_cyclist.png">
</p>

New Yorkers are supposed to be tough. They're supposed to be resilient. They're supposed to be like this guy in a suit and tie riding a bike through the East Village in the rain. But I must confess, that even as a New Yorker with a deep love for my two-wheeled machine, I am a fair-weather cyclist. 

This is the kind of week I love to spend in the saddle. It's the middle of September 2020. It's balmy (red line), humidity is low (yellow line), and there is absolutely no rain (brown line). And during this week, New Yorkers hopped on a Citi Bike and took a ride 413,223 times (blue line).  

<p align="center">
  <img width="600" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/great_bike_week.png">
</p>

It was a welcomed week at the tail end of Summer's dog days where, like this Wednesday from August, the air was thick and hot and gave the city its rainiest hour of the year. And although 66,069 riders braved the oppressive elements, the graph clearly shows that as rain began to fall in the late afternoon, ridership plummeted. 

<p align="center">
  <img width="600" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rainy_day.png">
</p>

Am I not the only fair-weather cyclist in New York City? Do others who love to ride also hate the feeling of a water logged shoes and streaks of mud running up their backs? Is there a statistically significant link between bike ridership and weather events like rain, temperature and humidity in New York City?

----

### The Data

To infer any possible links between ridership and weather, I turned to Citi Bike's [public system data](https://www.citibikenyc.com/system-data) and hourly Integrated Surface Data from the [National Centers for Environmental Information](https://www.ncei.noaa.gov/access/search/index)(NCEI). Both datasets are easily accessible via the respective organization's websites, although a public S3 bucket and an API are also available. 

**Citi Bike**

The entire dataset contains nearly every ride taken in New York City and Jersey City since June 2013 (Citi Bike removes rides taken by working staff and rides shorter than 60 seconds). For my test, I focused on 2020, the most recent full year available, with the following specifications:

  * Rides taken in New York City 
  * 19.5+ million data points.
  * Columns for trip duration, start/end time and date, start/end station, station name/id/lat/long, bike id, user type, gender and birth year.

**Weather**

NCEI's Integrated Surface Data is available via its website or an API and comes in a variety of customizable measurements and frequencies. For this test, I collected:

  * Hourly data measured at the Central Park weather station for all of 2020.
  * 8,700 + data points after removing weekly/monthly summaries and other non-regular reports.
  * Columns included air temperature, dew point, liquid precipitation, wind gusts, and sky cover conditions.

<br /> 

<p align="center">
  <img width="200" src="https://d21xlh2maitm24.cloudfront.net/nyc/Citi-Bike-provided-by-Lyft-Positive-170x57px.svg?mtime=20201023151104">
  <img width="200" src="https://d32ogoqmya1dw8.cloudfront.net/images/nesta/about/noaa_logo.v2.jpg">
</p>

---

### The Data: Issues

*COVID-19*

As we all know, the world was greatly impacted by the COVID-19 pandemic in 2020, and New York City was no exception. In particular, the pandemic influenced both the need for and choice of transportation options for the city's denizens. This test is not meant as a study of COVID-19's impact on Citi Bike and any potential impact is not considered. A rough chart of daily ridership does show a dip in ridership beginning in early spring, about the time the pandemic took over the city, and a surge in late summer. The extent of the pandemic's impact on these trends cannot be determined without further investigation. 
   
<img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/daily_trips_2020.png" width="400"> 
<img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/outliers.png" width="400">     
   
*Unrealistic outliers*

During EDA, charts of temperature and dew point against time showed a handful of unrealistic measurements above 1,800 degrees Fahrenheit. Twenty-seven of these measurements were found for dew point and 25 for temperature. None were sequential, except for a single pair of dew points. Because weather measurements were made every hour and ride start times were recorded down to the second, a single weather measurement was associated with thousands of rides. This made simply dropping the outliers an unappealing option. To deal with the outliers, I averaged the measurements from the hour before and the hour after as an estimate for the hour in question. 

*Dew Point = Humidity*

This test relies on dew point as a measurement for humidity. According to the National Oceanic and Atmospheric Association, "If you want a real judge of just how 'dry' or 'humid' it will feel outside, look at the dew point instead of [relative humidity]. The higher the dew point, the muggier it will feel." The Association suggests the following ranges:

  * less than or equal to 55: dry and comfortable
  * between 55 and 65: becoming "sticky" with muggy evenings
  * greater than or equal to 65: lots of moisture in the air, becoming oppressive


----

### The Data: Exploration

Temperature, dew point and rain were all plotted against rides/hour. The goal was to estimate reasonable segmentation points so that the data could be grouped into sub-populations for comparison. 

  <img align="left" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rides_temp_dot.png" width="400"> 

For this first pass at my test, two sub-populations for each weather condition were created. Based on experience, recommendations from experts, and the resulting plots, conditions were split into the following groups with the resulting sizes: 

  <b>Rain:</b> No rain <i>(=0mm):</i> 8,033 vs. Any rain <i>(>0mm):</i> 679
  <b>Temperature:</b> Cool <i>(<75F):</i> 4,854 vs. Hot <i>(>=75F):</i> 3,858
  <b>Dew Point:</b> Low <i>(<=55F):</i> 5,927 vs. High <i>(>55F):</i> 2,785

<br /> 

---

### The Test

To address the question "Does weather impact Citi Bike ridership in New York City?" null and alternative hypothesizes were set along with a significance level. A Welch's t-test was chosen for the comparison due to the sub-populations' large size. 

  * <b>Ho:</b> Ridership is unaffected by weather conditions such as temperature, humidity, and rain
  * <b>Ha:</b> Ridership will decrease based on high measurements of temperature, humidity, and rain
  * <b>Alpha:</b> 0.05 <i>(0.0167 with a Bonferroni correction for three test)</i> 

----

### The Results 

<img align="right" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rain_test.png" width="400"> 

The test returned extremely low p-values, well below the alpha, for all three tests. As a result, I can safely reject my null hypothesis (and soothe my ego) to conclude ridership is impacted by temperature, rain, and humidity. The chart to the right shows the normalized frequency of rides in the 'No rain' and 'Any rain' sub-populations. The dashed lines show the sub-population's actual means separated by a significant margin, which was expected given our p-values. The results for dew and temperature appear similar.

<i>P-values:</i>
  * Dew: 9.780001451639427e-75
  * Rain: 2.293253491572896e-53
  * Temp: 1.9517356662769365e-207

---

### The Future

This was a first pass at combining weather measurements and ride data for the purpose of a single statistical test. The resulting dataset is dense and rich with many more avenues for exploration.

A finer understanding of weather's impact on ridership could be gained by parsing the data further. Additional sub-populations could be created to account for more moderate weather conditions, seasons, and the time of day. This test did not account for the continuous nature of the data over 24 hour periods. 

Attributes already present in the data set including gender, age, geography, customer type, and additional weather conditions could be explored to further refine these findings or answer other questions.

Finally, an additional year could be considered to avoid the uncertainty around COVID-19's impact on ridership or, when compared to 2020, measure what impact the pandemic had.  

----

### The Tech


<img align="left" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/600px-Pandas_logo.svg.png" width="200"> 

<img align="right" src="https://matplotlib.org/stable/_static/logo2_compressed.svg" width="200">

<p align="center">
  <img src="https://cdn.icon-icons.com/icons2/2415/PNG/512/python_original_logo_icon_146381.png" width="100"/> 
</p>

