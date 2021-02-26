# Fair_Weather_Cyclists

*Is there a link between Citi Bike ridership and weather conditions? Does everyone hate riding in the rain?*

<p align="center">
  <img width="650" src="https://github.com/leckieje/fair_weather_cyclists/blob/main/images/rider_in_the_rain.jpg">
</p>

New Yorkers are supposed to be tough. They're supposed to be resilient. They're supposed to be like this guy in a suit and tie riding a bike through the East Village in the rain. But I must confess, that even as a New Yorker with a deep love for my two-wheeled machine, I am a fair-weather cyclist. 

This is the kind of week I love to spend in the saddle. It's the middle of September 2020. It's balmy (red line), humdity is low (yellow line), and there is absolutely no rain (brown line). And during this week, 413,223 New Yorkers hopped on a Citi Bike and took a ride (blue line).  

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

  * 12 files with more than 19.5 million data points.
  * Columns for trip duration, start/end time and date, start/end station name/id/lat/long, bike id, user type, gender and birth year.

**Weather**

NCEI's Integrrated Surface Data is availible via its website or an API and comes in a variety of customizable measurements and frequencies. For this project, I downloaded:

  * Hourly data measured at the Central Park weather station located in Belvedere Castle for all of 2020.
  * After cleaning, the data set contained more than 8,700 data points.
  * Columns included air temperature, dew point, liquiid precipitation, wind gusts, and sky cover conditions.

**Issues to Consider**

* COVID-19
* Unrealistic outliers 
* Which hour?
* Dew Point = Humidity

<p align="center">
  <img width="200" src="https://d21xlh2maitm24.cloudfront.net/nyc/Citi-Bike-provided-by-Lyft-Positive-170x57px.svg?mtime=20201023151104">
  <img width="200" src="https://d32ogoqmya1dw8.cloudfront.net/images/nesta/about/noaa_logo.v2.jpg">
</p>

----

### The Test

----

### The Results 


Dew = pvalue=9.780001451639427e-75

Rain = pvalue=2.293253491572896e-53

Temp = pvalue=1.9517356662769365e-207



**Future Avenues for Investigation**


----

### The Tech


<img align="left" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/600px-Pandas_logo.svg.png" width="200"> 

<img align="right" src="https://matplotlib.org/stable/_static/logo2_compressed.svg" width="200">

<p align="center">
  <img src="https://cdn.icon-icons.com/icons2/2415/PNG/512/python_original_logo_icon_146381.png" width="100"/> 
</p>

