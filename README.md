# Project Statistical Modeling with Python

## Project Objectives:
The project aims to utilize the CityBikes API to gather data on bike stations, connect to Foursquare and Yelp APIs to retrieve information on nearby points of interest, and build a statistical model to understand the relationship between bike availability and surrounding characteristics. 

## Process Overview:
### Step 1: Collecting information on bike stations in a particular city using the CityBikes API
* Sending a request to the CityBikes API to retrieve the data source.
* Selecting New York City and retrieving all available bike stations in that city.
* Using a loop to parse the JSON object to obtain the latitude, longitude, and number of bikes for each bike station.
* Putting the results into a Pandas dataframe.
* Storing the dataframe in a CSV file.

### Step 2: Collecting information on POIs (Points of Interest) for each bike station collected from Step 1
* Sending requests to the Foursquare API and Yelp API to retrieve POIs within a 10,000-meter radius for each bike station based on latitude and longitude.
* Using a loop to parse the JSON object to obtain POI details such as name, address, and distance from the bike station, as well as phone, rating, price, review_count, url, and category.
* For analysis purposes, the POIs will include: 'restaurant', 'coffee', 'bar', 'hotel', 'park', 'shopping', 'supermarket', 'museum', 'stadium', 'cinema', 'bus', 'school', 'hospital'.
* Analyzing the results from both APIs to determine which one provides more comprehensive information
* Putting the results into Pandas dataframes.
* Storing the dataframes in CSV files.

### Step 3: Joining - Loading - Performing EDA
* Merging the data from Citybikes with the data from either Foursquare or Yelp to create a new dataframe
* Establishing a SQLite database to store the data collected from the APIs on POIs into SQLite3 database. Validate data.
* Exploratory Data Analysis
	- Take a premilinary look to get a brief overview of dataset
	- Explore data by descriptive statistics
	- Data Wrangling: cleaning and transforming data 
	- Explore data by visualization (Univariate and Bivarirate exploration)
	- Use hypothesis testing
* Storing dataframe in csv files

### Step 4: Building statistical model
* Defining target variable and independent variables and selecting features
* Encoding categorical variables
* Builing model using Python's statsmodels module
* Evaluating and Interpreting model results to understand the relationship between bike stations and nearby POIs.
* Iterating to find the best model


## Results Summary:

1. **APIs**: 
After comparing the quality of data coverage between the Foursquare API and Yelp API for New York, US, it was found that YELP API provided more detailed information.
    * FOURSQUARE API: has not yet covered the attributes I want, such as rating, main/max_price,etc... even though its documentation says it does.
    * YELP API: provides a lot of different interesting attributes for each POI, such as review count, rating, price, phone, even business url, menu url, etc...
	    - However, YELP API has one drawback. It does not support to looking for many categories at one single API call. With FOURSQUARE API, we can search 'restaurant,coffees' at one time; while with YELP API, we search 'restaurant' then later search 'coffee'.
Given the advantage of Yelp API, it was chosen for further analysis.

2. **Model Result**:
    * The results from the Linear Regression Model were not particularly bright. Due to the dataset, it appears that there is minimal correlation observed among the numerical variables.

<p align="center" style="margin-top: 20px; margin-bottom: 20px;">
<img width="90%" src="https://github.com/ThuyTran102/Statistical-Modelling-Project/blob/main/images/pairplot.png" alt="pairplot"></img>
</p>	

<p align="center" style="margin-top: 20px; margin-bottom: 20px;">
<img width="70%" src="https://github.com/ThuyTran102/Statistical-Modelling-Project/blob/main/images/heatmap.png" alt="heatmap"></img>
</p>	


* Overall Linear Regression model with 2 independent varibales (Longitude and Distance) appears to be statistically significant. **The characteristics of longitude and distance to nearby POIs appear to be the most important predictors of the number of bikes at bike stations.**. However, the model doesn't well fits the data. The Adj. R-squared is extremely low (0.003) meaning that this model is capable of explaining 0.3% of the patterns in the data ---> this model explains only a very small portion of the variation in the dependent variable.
* The **target varibale 'Number_Of_Bikes' is not a continuous data**, so Regression Model is not appropriate.

<p align="center" style="margin-top: 20px; margin-bottom: 20px;">
<img width="70%" src="https://github.com/ThuyTran102/Statistical-Modelling-Project/blob/main/images/model_output.png" alt="model_ouput"></img>
</p>	


## Challenges:
1. Limit usage for YELP API is 500 call per day
	- Initially, I chose Vancouver and found 250 bike stations and 2 POIs in order to stay within the limitation. However, with only 2 POIs, the data was insufficient for robust analysis and statistical modeling purposes. Unfortunately, by the time I finished Part 3, I had to restart the process to find another city with fewer bike stations to gather more POI data. Actually, 37 bike stations dataset is small quantity for analysis.
	- Each time I ran the code to test, it consumed the daily API limit.
2. Data I collected is not enough in term of quantity and probably including quality, so my dataset does not reveal the strong correlated relationship between bike stations and nearby POIs as initially anticipated. Model results are not good even though I tried to revisit EDA process.


## Future Goals
If I had more time, I would consider the following:
* Investigate additional data sources or APIs that provide more comprehensive coverage of POIs 
* Collecting more data.
* Experiment with different statistical modeling techniques (for example Classification model) to uncover hidden patterns or relationships between bike stations and nearby POIs.
* Collaborate with domain experts or stakeholders to gain deeper insights into the implications of the data as well as to understand the factors influencing bike availability at different locations.
