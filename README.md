# Sparkify Capstone Project - Spark Predictive Analysis

## Introduction

For my capstone project, I chose to work with the Sparkify dataset. There were other projects about predictive analytics in a business setting, but this project gave me the chance to leverage Spark, in order to interact with a 12 GB dataset (over 25 million rows!).

## Project Overview

The goal of this project is to leverage user log files, to predict whether or not a user will cancel their account with the Sparkify service. The Sparkify service is a ficititious music service, created by udacity, to mock real music service log files, such as Spotify. A user can visit many different pages, and have multiple types of interactions to click Next Song, witness an Advertisement, Upgrade, or Downgrade. The log files also provide user specific information, like the location of the user/ the user agent they are acessing the service with.

## File Structure

* |- `Sparkify-Copy2.html` (Scrap work)
* |- `Sparkify-Copy2.ipynb` (Scrap work)
* |- `Sparkify-small-data-set.ipynb`
* |- `Sparkify-small-data-set.html`
* |- `mini_sparkify_event_data.json.zip` (Small dataset)
* |- `Sparkify-emr.html` (Large Dataset)
* |- `Sparkify-emr.ipynb` (Large Dataset)

## Cleaning and Converting Data

* Location column coverted into a city and a state column
* User agent string converted into a browser and a platform column
* Timestamp was converted into a unique day column
* These columns were cleaned for empty strings to ensure creation of the new column
* Lastly, the page action of cancelling an account helped to define user churn in a column with a 1 or a 0

## Visualizing Data

* All visualizations looked at the difference between the sets of users that did or not did not churn.
* A bar plot was used to look at the state, browser, and platform variables, to get an idea of how each value in these columns affected churn.
* A box and whisker plot was used for the remaining features that revolved aroun the count of other columns given certain conditions.

## Feature Engineering

* In leveraging the previously created uniqueDay column, aggregations were run to count total daily interactions with specific pages, like clicking next song, or giving the current song a thumbs down. These were then converted into average daily columns, to better define the user's behavior.
* 2 other features that were engineered, but related to the overall experience, not the daily experience, were the count of distinct artists listened to, and the amount of time using the service.

## Modeling

* Features are vectorized before modeling, using StringIndexer for categorical features, and VectorAssembler for numerical features.
* After numerical features are scaled, with StandardScaler, the index and previous vector are passed through VectorAssembler again.
* I tried out models of logistic regression, random forest, and gradient boosted trees, to see which would work best, and then ran a crossvalidator to improve the model. (Results depends on whether I was using the small dataset or the large dataset (through AWS EMR)

## Results

### **Small Dataset**: 
 
* Logistic Regression Test Set (F1: 70.31%, AreaUnderRoc: 86.25%)
* Gradient Boosted Trees Test Set (F1: 60.27%, AreaUnderRoc: 72.71%)
* Random Forest Test Set (F1: 71.70%, AreaUnderRoc: 79.17%)
* After running a crossvalidator, Logistic Regression Training Set (F1: 86.94%, AreaUnderRoc: 90.41%) and Test Set (F1: 79.55%, AreaUnderRoc: 83.33%)

### **Large Dataset (EMR)**: 
 
* Logistic Regression Test Set (F1: 81.51%, AreaUnderRoc: 85.16%)
* Gradient Boosted Trees Test Set (F1: 81.07%, AreaUnderRoc: 81.73%)
* Random Forest Test Set (F1: 81.57%, AreaUnderRoc: 83.53%)
* After running a crossvalidator, Logistic Regression Training Set (F1: 81.95%, AreaUnderRoc: 86.64%) and Test Set (F1: 82.45%, AreaUnderRoc: 85.50%)
* After running a crossvalidator, Random Forest Training Set (F1: 84.70%, AreaUnderRoc: 96.14%) and Test Set (F1: 91.89%, AreaUnderRoc: 86.93%)