
# Concert Ticket Analysis 

## Introduction

Ed Sheeran's last concert sold within 5 min and was advertised on Viagogo for as high as 800€ soon after (vs (80€ initially). Concert prices can vary wildly depending on the type of event. For some really popular events, primary tickets are almost impossible to get a hold of. Ticket scalping is an industry in and of itself. 

Both big music fans, we aimed at cracking the code of the concert industry and set out to predict what concert would sell out. In front of the diversity of events and artists, we were convinced that data science could prove invaluable in approaching the problem. 

**Would we be able to predict whether a concert would sell out? If so, could we predict what's its fair value and its final resale price would be?**

Convinced by the potential relevance of our work, we have decided to keep our code private **for now**. However, we outline our approach and our findings in this report as follows:

_**[1. Data Scraping](#scraping)**_

_**[2. Data Processing & Feature Engineering](#processing)**_

_**[3. Finding the Best Model](#model)**_

_**[4. Final Results & Dashboard](#results)**_

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

### Data Cleaning & Processing

#### Merging the Datasets and matching the strings
Given the variety of sources that we used we faced numerous problems in aggregating our datasets. One of our main problem, besides the diversity in format among the various sources, was in **reconciliating the different concerts and making sure that the string matched appropriately.**

Some artists' names are rather ambiguous (i.e. [The Blaze](https://open.spotify.com/artist/1Dt1UKLtrJIW1xxRBejjos?si=q-pILVELSlCO6iOFa1kiPg) is very very different from [Blaze](https://open.spotify.com/artist/5yK5YSsWKH35QRTsHQHxEN?si=fczjQ-m1Sp62ikfH3gJMFA)) and required the utmost attention as we navigate through the different APIs.  

We leveraged [SeatGeek](http://seatgeek.com)'s fantastic library, [Fuzzy Wuzzy](https://github.com/seatgeek/fuzzywuzzy), intensely to make sure that the artists' and the events' names matched exactly acrossed the different sources. 

#### Updating the Records on a Daily Basis

An additional challenge we faced was to aggregate our observations accordingly. Every day, we collected information on **~9,000 events**. As we aggregated our data, we had to be careful at which information we would update from one day to the next and at our memory usage. We used various tricks such as the **Multiprocessing Python Library** to efficiently process the different data types and limit runtime.

#### Leveraging More Details for Matching with [SeatGeek](http://seatgeek.com)

We seeked to collect data regarding the secondary markets and quickly noticed that the task was more difficult than it seemed. Some artists performed twice a day in a given city, parking passes were sold for some events, etc. We thus created stringent criteria so as to guarantee that our datasets would remain as accurate as possible.


### Dealing with High Dimensions

There are countless different venues and music types represented in our dataset. To incorporate a maximum of informations from these, we attempted various clustering techniques such as K-Means or using proxy variables such as the number of seats or latitudes/longitudes. Ultimately, we settled on leveraging Multiple Correspondance Analysis (MCA) has it allowed us to reduce significantly the number of dimensions while keeping the unique information embedded in the venue/the genre itself.


### Exploratory Data Analysis

Armed with our dataset and **70+ features**, we tried to get a grasp of some underlying dynamics. 

### Correlation & VIF Analysis

As we tried to understand what were the key drivers of concerts' popularity, we started by looking at how correlated our variables were. 

Aside from songs' internal characteristics and popularity indicators, our variables seem to be relatively uncorrelated and we were able to weed out redundant information from the dataset.

![Correlation Matrix](assets/img/correlation_matrix.jpg)

**VIF conclusions to add**

### Going Beyond our Prejudice

Interestingly, regardless of the urban areas, **~6%** of concerts eventually sell out. 

While we may have expected that concerts sell-out primarily around the weekend, our analysis also indicates that sell-out rates are relatively uniform through the week days.

![Proportion of sold out concerts per day of the week](assets/img/week_day.jpg)

**Add: Tracking sold outs across time (graphs with distributions used in the dashboard to show how long it took to sell out vs how long before a concert)!!**

## 3. Finding the Best Model <a name="model"></a>

We aimed at optimizing the ability of our model to correctly predict that a concert would sell out. In that regard, we focused on maximizing **Precision** (defined as $\frac{True Positive}{True Positive + False Positive}$ ).

We started by using a logistic regression and found the following results:




## 4. Final Results & Dashboard <a name="results"></a>

In the end, we settled on using LightGBM. It provided us with numerous advantages including:
- Simplified class imbalance management
- Efficient runtime
- Advanced categorical variable handling
- Ability to model complex nonlinear relationships

### Hyperparameter Tuning

Being a boosting model, LightGBM We used Bayesian optimization techniques to find the optimal parameters .

### TKinter and Dash

## Conclusion



### Sources

- [The Independent - Ed Sheeran](https://www.independent.ie/entertainment/ed-sheeran-tickets-sold-out-in-under-five-minutes-35417761.html)