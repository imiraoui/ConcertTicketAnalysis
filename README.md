
# Concert Ticket Analysis

## Introduction

Ed Sheeran's last concert sold within 5 min and was advertised on Viagogo for as high as 800€ soon after (vs (80€ initially). Concert prices can vary wildly depending on the type of event. For some really popular events, primary tickets are almost impossible to get a hold of. Ticket scalping is an industry in and of itself. 

Both big music fans, we aimed at cracking the code of the concert industry and set out to predict what concert would sell out. In front of the diversity of events and artists, we were convinced that data science could prove invaluable in approaching the problem. 

**Would we be able to predict whether a concert would sell out? If so, could we predict what's its fair value and its final resale price would be?**

In this report, we outline our approach and our findings:

_**[1. Data Scraping](#scraping)
[2. Data Processing & Feature Engineering](#processing)
[3. Finding the Best Model](#model)
[4. Final Results](#results)**_

## 1. Data Scraping <a name="scraping"></a>

Given the nature of our problem, it was impossible to find readily available historical data. Hence, we started creating our own dataset and run our script on a daily basis at 9PM PST. We started scraping the data on *October 19th 2019* and aggregated data from 4 different sources using the available **APIs** and the **Python Requests Library** for web scraping:
1. [SongKick](http://songkick.com)
   - Gave us the calendar of upcoming events and details on the events' venues
   - Allowed us to check if the event was sold out
2. [Spotify](http://spotify.com)
   - Provided us with information regarding the artists and their genre
   - Allowed us to use songs' characteristics as features
3. [Last.fm](http://last.fm)
   - Giving us additional features on artists' genres and popularity stats
4. [SeatGeek](http://seatgeek.com)
   - Provided with consistent insights into secondary markets (number of listings, price range, etc.)

To alleviate the burden of running a script every day, we created a virtual machine instance on [Google Cloud Platform (GCP)](https://cloud.google.com/) and created a Cron-Tab to automate the process. 

We hypothesized that most of the popular events and the demand was centered around the main urban areas and thus decided to focus our research on the four main US metropolitan areas: **New York**, **San Francisco**, **Chicago** and **Los Angeles**.

## 2. Data Processing & Feature Engineering <a name="processing"></a>

### Data Cleaning

Given the variety of sources that we used we faced numerous problems in aggregating our datasets.

FUZZY WUZZY PR SEATGEEK et SPOTIFY et LAST.FM

QUD CONCERT EXISTE PAS/VS JUSTE CHECK SOLD OUT AND UPDATE FEATURES

RETROUVER SEATGEEK AVEC LA DATE ET LIEU PR ETRE SUR QUE RIGHT EVENT



### Exploratory Data Analysis

VIF / Correlation heatmaps
Creating new Variables / Feature Engineering
MCA

### Visualizing Concerts

Tracking sold outs across time (graphs with distributions?)
# In construction...

## 3. Finding the Best Model <a name="model"></a>


In the end, we settled on LightGBM. LightGBM provided with numerous advantages including:
- Simplified class imbalance management
- Efficient runtime
- Advanced categorical variable handling
- Ability to model complex nonlinear relationships

## 4. Final Results <a name="results"></a>

<iframe src="/assets/model_perfs.html"> </iframe>

### Sources (sources dans markdown???)

- [The Independent - Ed Sheeran](https://www.independent.ie/entertainment/ed-sheeran-tickets-sold-out-in-under-five-minutes-35417761.html)