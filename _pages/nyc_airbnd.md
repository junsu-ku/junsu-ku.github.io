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

![](/images/nyc_airbnb/intro.jpg)

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

[New York City Airbnb Listing Viewer](https://junsu-ku.shinyapps.io/NYC_Airbnb_Listing_Dashboard/).
[![](/images/nyc_airbnb/shiny_app.PNG)](https://junsu-ku.shinyapps.io/NYC_Airbnb_Listing_Dashboard/)

<br/>
<br/>


Visualization
-------------
![](/images/nyc_airbnb/unnamed-chunk-6-1.png)

The price for Airbnbs in New York City is heavily distributed between $70 to $200 per night with mean price at $152.72 and median price at $106.

<br/>

| Neighbourhood Group | Mean Price | Median Price |
|---------------------|------------|--------------|
| Bronx               | 87.5       | 65           |
| Brooklyn            | 124        | 90           |
| Manhattan           | 197        | 150          |
| Queens              | 99.5       | 75           |
| Staten Island       | 115        | 75           |

![](/images/nyc_airbnb/unnamed-chunk-7-1.png)

Again, prices in each neighbourhood seems to be distributed in between
$70 to $200 per night. Manhattan holds the highest mean and median price
compared to other neighbourhood groups, followed by brooklyn. This makes
sense as manhattan is the busiest area and a hot destination spot for
travellers visiting New York City. Also, there is a common trend within
price where mean is always greater than median, meaning price is skewed
to the right. This suggests there are many listings offered at a
relatively cheaper price compared to the price of an average listing,
but there are few high-end listings offered at a much higher prices.

<br/>

| Room Type       | Mean Price | Median Price |
|-----------------|------------|--------------|
| Entire Home/Apt | 212        | 160          |
| Private Room    | 89.8       | 70           |
| Shared Room     | 70.1       | 45           |

![](/images/nyc_airbnb/unnamed-chunk-8-1.png)

Again, there seems to be a trend of mean price being greater than median
price. Renting an entire home or an apartment is more costly, as it
should be, compared to renting a private room. Shared room is the
cheapest room type option as not many people would prefer choosing a
shared room than the alternatives.

<br/>

![](/images/nyc_airbnb/unnamed-chunk-9-1.png)

Manhattan holds the most number of listings as it is the most busiest
neighbourhood group, followed by Brooklyn. These two neighbourhood
groups combine to make up more than 85 percent of the listings within
New York City. This also supports the mean price difference within
neighbourhood group, Manhattan and Brooklyn must have many tourists and
visitors. More demand results in more supply and higher prices.

<br/>

![](/images/nyc_airbnb/unnamed-chunk-10-1.png)

Within Manhattan, Harlen neighbourhood holds the most number of
listings, with quite a bit of difference comparing to the second-most
neighbourhood. The number of listings in Manhattan seems mostly
distributed amongst top 12 neighourhoods.

<br/>

![](/images/nyc_airbnb/unnamed-chunk-11-1.png)

Within Brooklyn, Williamsburg holds the most listings, closely followed
by Bedford-Stuyvesant. In Brooklyn, listings appear to be distributed
amongst only the top 5 neighbourhoods, with the top 2 neighbourhoods
holding the majority of the listings in Brooklyn.

<br/>

![](/images/nyc_airbnb/unnamed-chunk-12-1.png)

Now, comparing the top 5 neighbourhoods in each neighbourhood groups,
surprisingly Williamsburg and Bedford-Stuyvesant contain the most number
of listings, with at least 1,000 more listings than Harlem. This could
be due to Manhattan having more diverse areas for landmarks and
tour-spots, thus listings being more evenly distributed amongst
neighbourhoods compared to Brooklyn.

<br/>

![](/images/nyc_airbnb/unnamed-chunk-13-1.png)

We see that majority of listings, almost 61 percent, in Manhattan are
offered as entire home or apartment. This is very unique and supports
the trends we have been seeing in price distribution. Manhattan had much
higher mean price compared to other neighbourhood groups and that may be
the case because it is the only neighbourhood group that has more than
half of its listings offered as entire home or apartment.
