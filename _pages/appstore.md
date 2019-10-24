---
title: "Apple Appstore Mobile Games"
subtitle: "Exploratory Data Analysis"
permalink: /appstore/
header:
  image: "/images/appstore/appstore_header.png"
---

<br/>

Introduction
------------

![](/images/appstore/intro.png)

With the initial launch of iPhone App store on July 10, 2008, the mobile games industry has grown to worth billions of dollars over the years, with companies spending vast amounts of money on the development and marketing of these games. Some mobile games, such as Clash of Clans and Pokemon Go, have become an international success, accumulating over hundred millions of users, proving just how attractive and accessible mobile games are to people with smart devices. Even the most popular veteran console game developers, such as Nintendo, have release free mobile games, extending their franchise into the mobile games industry.

The Apple Appstore Mobile Games dataset was found on [Kaggle.com]https://www.kaggle.com/tristan581/17k-apple-app-store-strategy-games) and it contains Airbnb listings of New York City with 48895 observations and 16
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
While performing data cleaning process, some duplicated rows of
observations were discovered. For best practices, we will create a
seperate dataset containing the duplicated observations and remove the
duplicates from the main dataset.

``` r
# Uniqueness of observations ----

  # Check if all rows are unique
    nrow(unique(games)) == nrow(games)
```

    ## [1] FALSE

``` r
  # Find duplicated rows and save them just in case
    indices <- duplicated(games) | duplicated(games, fromLast = TRUE)
    dupes <- games[indices, ]

  # Remove duplicated rows
    games <- unique(games)
```

<br/>
<br/>

Missing Data
------------

    ##  Average User Rating User Rating Count       Price         
    ##  Min.   :1.000       Min.   :      5.0   Min.   :  0.0000  
    ##  1st Qu.:3.500       1st Qu.:     12.0   1st Qu.:  0.0000  
    ##  Median :4.500       Median :     46.0   Median :  0.0000  
    ##  Mean   :4.062       Mean   :   3306.2   Mean   :  0.8154  
    ##  3rd Qu.:4.500       3rd Qu.:    307.2   3rd Qu.:  0.0000  
    ##  Max.   :5.000       Max.   :3032734.0   Max.   :179.9900  
    ##  NA's   :9359        NA's   :9359        NA's   :24        
    ##       Size          
    ##  Min.   :5.133e+04  
    ##  1st Qu.:2.295e+07  
    ##  Median :5.674e+07  
    ##  Mean   :1.158e+08  
    ##  3rd Qu.:1.330e+08  
    ##  Max.   :4.006e+09  
    ##  NA's   :1

``` r
  # Confirm that 9446 NA is user rating and user rating counts belong in the same obs.
  { na_data <- NULL

    na_ur <- games %>%
      filter(is.na(`Average User Rating`))

    na_urc <- games %>%
      filter(is.na(`User Rating Count`))

    na_data <- rbind(na_ur, na_urc)
    na_data <- unique(na_data)

    games %>%
      filter(is.na(`User Rating Count`) | is.na(`Average User Rating`)) %>%
      nrow() == nrow(na_data) }
```

    ## [1] TRUE

There are 9446 missing data on Avrage User Rating and User Rating Count
variables. I suspected that these are games where no users have left
ratings for, thus resulting in NA as Average User Rating and User Rating
Count, meaning NA User Rating Count results into NA Average User Rating.
This hypothesis is confirmed.

<br/>

|    | ID         | Name                           | Average User Rating | User Rating Count | Price | Size       |
|----|------------|--------------------------------|---------------------|-------------------|-------|------------|
| 1  | 1104421243 | Germiz                         | NA                  | NA                | NA    | 296098816  |
| 2  | 1437301951 | Gears POP!                     | NA                  | NA                | NA    | 304507904  |
| 3  | 1452474937 | State of Survival              | NA                  | NA                | NA    | 251956224  |
| 4  | 1453501895 | LEAGUE OF WONDERLAND           | NA                  | NA                | NA    | 155536384  |
| 5  | 1457687242 | Western Redemption: Cowboy Gun | NA                  | NA                | NA    | 450572288  |
| 6  | 1457796984 | Magic ARena                    | NA                  | NA                | NA    | 387767296  |
| 7  | 1464481838 | WW2 Battle Front Simulator     | NA                  | NA                | NA    | 541718528  |
| 8  | 1464510254 | "Lock's Quest"                 | NA                  | NA                | NA    | 1565436928 |
| 9  | 1466576839 | Second Galaxy                  | NA                  | NA                | NA    | 1625473024 |
| 10 | 1467043008 | Game of Thrones Beyond\u2026   | NA                  | NA                | NA    | 2005816320 |
| 11 | 1467205227 | Color Defense                  | NA                  | NA                | NA    | 98912256   |
| 12 | 1468267370 | Crazy Restaurant Cooking Games | NA                  | NA                | NA    | 178845696  |
| 13 | 1469002408 | Fleet Chronicle                | NA                  | NA                | NA    | 94469120   |
| 14 | 1469019441 | Idle Mars Colonization         | NA                  | NA                | NA    | NA         |
| 15 | 1469316065 | Idle Computer Game Company     | NA                  | NA                | NA    | 95491072   |
| 16 | 1471495472 | Terrorist Shooter: City Missio | NA                  | NA                | NA    | 222621696  |
| 17 | 1471767851 | Type II                        | NA                  | NA                | NA    | 811570176  |
| 18 | 1471952843 | Island Jurassic Survival       | NA                  | NA                | NA    | 306213888  |
| 19 | 1472974346 | Flying Carpet Shooting         | NA                  | NA                | NA    | 101702656  |
| 20 | 1473098634 | War Shooting Battle Survival   | NA                  | NA                | NA    | 261016576  |
| 21 | 1474104832 | Magic Puzzle Box: 3 in 1       | NA                  | NA                | NA    | 114580480  |
| 22 | 1474206079 | Block Soldier Sniper           | NA                  | NA                | NA    | 170358784  |
| 23 | 1474608803 | Super kid                      | NA                  | NA                | NA    | 11404288   |
| 24 | 1474611467 | Lava Island Adventure          | NA                  | NA                | NA    | 21191680   |

There are 24 missing prices and 1 missing size. The row with missing
size in contained within the rows with missing prices. The observations
with missing prices are also missing the Avrage User Rating and User
Rating Count. These rows will be discarded as they do not provide any
insight to the analysis performed later.

<br/>
<br/>

Data Manipulation
-----------------
Some data manipulation was required on Primary Genre and Genres variables:


| Name                           | Primary Genre | Genres                                 |
|--------------------------------|---------------|----------------------------------------|
| Sudoku                         | Games         | Games, Strategy, Puzzle                |
| Reversi                        | Games         | Games, Strategy, Board                 |
| Morocco                        | Games         | Games, Board, Strategy                 |
| Sudoku (Free)                  | Games         | Games, Strategy, Puzzle                |
| Senet Deluxe                   | Games         | Games, Strategy, Board, Education      |
| Sudoku - Classic number puzzle | Games         | Games, Entertainment, Strategy, Puzzle |
| Gravitation                    | Games         | Games, Entertainment, Puzzle, Strategy |
| Colony                         | Games         | Games, Strategy, Board                 |
| Carte                          | Games         | Games, Strategy, Board, Entertainment  |
| "Barrels O' Fun"               | Games         | Games, Casual, Strategy                |


-   Primary Genre was mostly Games, which is redundent as this is a
    dataset of mobile games. For very few rows where primary genre was
    not Games, it was included inside Genres. Thus, Primary Genre
    variable proves uninsightful.

-   Strategy was included in almost all rows of Genres. Entertainment is
    uninsightful as all games are a source of entertainment and does not
    distinguish one game from another in terms of genre. Games was
    included in all rows. Strategy, Entertainment and Games were removed
    from Genres.

-   The type of genres will be separated out into a list within each
    rows.

<br/>
<br/>


Analysis
--------

For mobile games, measure of success ties in closely with the number of
users a game has, which is directly reflected on the number of user
rating count and the average user rating. The table below shows top 10
mobile games on the app store as of August 3rd, 2019. Top 10 was
selected by descreasing order of user rating count of games with average
user rating of 4.5 or higher.


Table of Top 10 User Rating Count:

|    | ID         | Name                              | Average User Rating | User Rating Count | Price | Developer                            | Size   | Genres       | Original Release Date | Current Version Release Date |
|----|------------|-----------------------------------|---------------------|-------------------|-------|--------------------------------------|--------|--------------|-----------------------|------------------------------|
| 1  | 529479190  | Clash of Clans                    | 4.5                 | 3032734           | 0     | Supercell                            | 161.2  | Action       | 2012-08-02            | 2019-06-20                   |
| 2  | 1053012308 | Clash Royale                      | 4.5                 | 1277095           | 0     | Supercell                            | 145.1  | Action       | 2016-03-02            | 2019-08-01                   |
| 3  | 1330123889 | PUBG MOBILE                       | 4.5                 | 711409            | 0     | Tencent Mobile International Limited | 2384.1 | Action       | 2018-03-19            | 2019-06-12                   |
| 4  | 597986893  | Plants vs. Zombies\u2122 2        | 4.5                 | 469562            | 0     | PopCap                               | 120.8  | Adventure    | 2013-08-15            | 2019-07-29                   |
| 5  | 672150402  | Boom Beach                        | 4.5                 | 400787            | 0     | Supercell                            | 202.8  | Action       | 2014-03-26            | 2019-07-03                   |
| 6  | 1270598321 | Cash, Inc. Fame & Fortune Game    | 5                   | 374772            | 0     | Lion Studios                         | 246    | Simulation   | 2017-10-06            | 2019-07-12                   |
| 7  | 1116645064 | Idle Miner Tycoon: Cash Empire    | 4.5                 | 283035            | 0     | Kolibri Games GmbH                   | 444    | Simulation   | 2016-07-01            | 2019-07-31                   |
| 8  | 847985808  | Star Wars\u2122: Commander        | 4.5                 | 259030            | 0     | NaturalMotion                        | 123.1  | Action       | 2014-08-21            | 2019-07-18                   |
| 9  | 995999703  | Agar.io                           | 4.5                 | 257852            | 0     | Miniclip.com                         | 83.9   | Action       | 2015-07-08            | 2019-07-08                   |
| 10 | 921022358  | Star Wars\u2122: Galaxy of Heroes | 4.5                 | 240990            | 0     | Electronic Arts                      | 180.6  | Role Playing | 2015-11-24            | 2019-07-22                   |

There is a significant difference in the number of user rating counts
between the first, second and third in the list. Clash of Clans is a
very famous game that has generated over $6.4 billion globally since its
release in 2012. Later in 2016, the developers of Clash of Clans,
Supercell, has released a sister-game called Clash Royale, a game with
same characters involved as Clash of Clans but very distinct and unique
play style. With the popularity of Clash of Clans, it was relatively
easy for Clash Royale to take the second spot in the list.

<br/>

Table of Top 10 Genres:

|    | Genres       | Number of games |
|----|--------------|-----------------|
| 1  | Puzzle       | 3919            |
| 2  | Simulation   | 2124            |
| 3  | Action       | 1989            |
| 4  | Board        | 1697            |
| 5  | Casual       | 1689            |
| 6  | Role Playing | 1122            |
| 7  | Education    | 939             |
| 8  | Adventure    | 826             |
| 9  | Family       | 765             |
| 10 | Sports       | 733             |

As of August 3, 2019, Puzzle genre games take up the most number of
games available on Appstore, followed by Simulation games, then Action
games.

<br/>

![](/images/appstore/unnamed-chunk-7-1.png)

We see that there is a strong increasing trend of mobile games released
up until 2016. Starting 2017, The mobile games industry has been on a
decreasing trend in terms of the number of games released each year.

<br/>

![](/images/appstore/unnamed-chunk-8-1.png)

Out of all the mobile games released each year, Puzzle genre counts the
most number of games, followed by Simulation and Action.

<br/>

Table of Top 10 Developers:

|    | Developer                            | Total User Rating Count | Total Average User Rating | Total Number of Games |
|----|--------------------------------------|-------------------------|---------------------------|-----------------------|
| 1  | Supercell                            | 4710616                 | 4.5                       | 3                     |
| 2  | Tencent Mobile International Limited | 711409                  | 4.5                       | 1                     |
| 3  | Electronic Arts                      | 593165                  | 4.5                       | 6                     |
| 4  | Ninja Kiwi                           | 476661                  | 4.3                       | 17                    |
| 5  | PopCap                               | 469562                  | 4.5                       | 1                     |
| 6  | Lion Studios                         | 453471                  | 4.7                       | 3                     |
| 7  | Niantic, Inc.                        | 444110                  | 3.2                       | 2                     |
| 8  | Donut Games                          | 428938                  | 3.4                       | 8                     |
| 9  | Glu Games Inc                        | 406341                  | 4.2                       | 17                    |
| 10 | TapJoy                               | 311224                  | 3.5                       | 3                     |

Top mobile game developers have been selected by selecting the top 10
developers with most number of user rating count summed across all of
their games. Mobile game developer Supercell, creater of Clash of Clans
and Clash Royale, has the most number of total user rating count, having
more than six times the amount of second place, Tencent Mobile. It seems
obvious to consider Supercell as the most successful developer in the
mobile games industry.


<br/>

Table of Top 10 Games:

|    | ID         | Name                              | Average User Rating | User Rating Count | Price | Developer                            | Size   | Genres       | Original Release Date | Current Version Release Date |
|----|------------|-----------------------------------|---------------------|-------------------|-------|--------------------------------------|--------|--------------|-----------------------|------------------------------|
| 1  | 529479190  | Clash of Clans                    | 4.5                 | 3032734           | 0     | Supercell                            | 161.2  | Action       | 2012-08-02            | 2019-06-20                   |
| 2  | 1053012308 | Clash Royale                      | 4.5                 | 1277095           | 0     | Supercell                            | 145.1  | Action       | 2016-03-02            | 2019-08-01                   |
| 3  | 1330123889 | PUBG MOBILE                       | 4.5                 | 711409            | 0     | Tencent Mobile International Limited | 2384.1 | Action       | 2018-03-19            | 2019-06-12                   |
| 4  | 597986893  | Plants vs. Zombies\u2122 2        | 4.5                 | 469562            | 0     | PopCap                               | 120.8  | Adventure    | 2013-08-15            | 2019-07-29                   |
| 5  | 672150402  | Boom Beach                        | 4.5                 | 400787            | 0     | Supercell                            | 202.8  | Action       | 2014-03-26            | 2019-07-03                   |
| 6  | 1270598321 | Cash, Inc. Fame & Fortune Game    | 5                   | 374772            | 0     | Lion Studios                         | 246    | Simulation   | 2017-10-06            | 2019-07-12                   |
| 7  | 1116645064 | Idle Miner Tycoon: Cash Empire    | 4.5                 | 283035            | 0     | Kolibri Games GmbH                   | 444    | Simulation   | 2016-07-01            | 2019-07-31                   |
| 8  | 847985808  | Star Wars\u2122: Commander        | 4.5                 | 259030            | 0     | NaturalMotion                        | 123.1  | Action       | 2014-08-21            | 2019-07-18                   |
| 9  | 995999703  | Agar.io                           | 4.5                 | 257852            | 0     | Miniclip.com                         | 83.9   | Action       | 2015-07-08            | 2019-07-08                   |
| 10 | 921022358  | Star Wars\u2122: Galaxy of Heroes | 4.5                 | 240990            | 0     | Electronic Arts                      | 180.6  | Role Playing | 2015-11-24            | 2019-07-22                   |

Top 10 games have been selected by filtering out the Average User Rating
of 4.5 or higher and arranging by a decreasing order of User Rating
Count. As expected, all three games created by Supercell are placed
within top 5, with two of them taking the first and second place. The
third place, PUBG MOBILE, is a franchise game of a famous PC/Console
game called Player Unknown’s Battleground. Thus, the advantage of being
able to play a very similar game on smart devices is a huge merit to
users, directly reflected on the popularity of the mobile games version.

<br/>

Table of Free Games vs. Paid Games:

|   | Free  | Has In-App Purchases | Number of Games |
|---|-------|----------------------|-----------------|
| 1 | TRUE  | FALSE                | 7055            |
| 2 | TRUE  | TRUE                 | 7029            |
| 3 | FALSE | FALSE                | 2165            |
| 4 | FALSE | TRUE                 | 574             |

Most mobile games are offered at no cost to attract more users. Free
mobile games generate revenue by either offering in-app purchases or
showing in-game advertisements for their clients. As shown on the table
above, majority of mobile games in the dataset are free to download,
while half of those free games have in-app purchases.
