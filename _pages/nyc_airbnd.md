---
title: "New York City Airbnb"
subtitle: "Exploratory Data Analysis"
permalink: /nyc_airbnb/
header:
  image: "/images/nyc_airbnb/nyc_header.png"
---

<br/>

Introduction
------------

Airbnb is an online platform for arranging lodging, homestays or tourism experiences. Acting as an online broker, Airbnb allows hosts to offer their real estate listings on their platform and users can easily book their stay for their next travel destinations.

The New York City Airbnb dataset was found on [Kaggle.com](https://www.kaggle.com/dgomonov/new-york-city-airbnb-open-data) and it contains Airbnb listings of New York City with 48895 observations and 16
variables such as price, neighbourhood, room type, minimum nights, reviews per month and last review date.

<br/>
<br/>


Abstract
--------
This explanatory data analysis will focus on univariate/bivariate analysis through visualization to uncover some trends within the New York City’s Airbnb market. The first part of the analysis will focus on the price distribution amongst different levels of other variables such as neighbourhood group, neighbourhoods within each group, room type and others. Next, we will use reviews per month metric to see which listings are more popular than others. This exploratory data analysis was performed on R and the source code can be found [here](https://github.com/junsu-ku/NYC-Airbnb-EDA-in-R).

<br/>
<br/>


Data Cleaning
-------------
Data manipulation and cleaning procedures have been performed but not shown on this post to keep this post simple. Detailed version of this post which outlines the data cleaning procedure can be found [here](https://junsu-ku.github.io/NYC-Airbnb-EDA-in-R/).

<br/>
<br/>


Listing Viewer via R Shiny App
------------------------------
I have created an interactive viewer of the listings which allows you to apply filters to easily sort through the data. You can also download the filtered table through this shiny app viewer.
[New York City Airbnb Listing Viewer](https://junsu-ku.shinyapps.io/listing_viewer_shiny_app/).
![](/images/nyc_airbnb/shiny_app.PNG)

<br/>
<br/>


Visualization
-------------
![](/images/nyc_airbnb/unnamed-chunk-6-1.png)

The price for Airbnbs in New York City is heavily distributed between $70 to $200 per night with mean price at $152.72 and median price at $106.
