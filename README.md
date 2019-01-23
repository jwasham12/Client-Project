## Seven FEMA Lifelines
In the event of a disaster FEMA has identified seven different lifelines that require attention in an affected area.  Those are as follows:
- (1) Safety and Security
- (2) Food, Water, and Sheltering
- (3) Health and Medical
- (4) Energy (Power and Fuel)
- (5) Communication
- (6) Transportation
- (7) Hazardous Waste

## Problem Statement
The goal for this project is two fold.  Can data available on Yelp be used to:
- (1) Categorize businesses in an affected area by Lifeline
- (2) Estimate potential impact of a disaster on the area

## Notebooks
This repository contains the following notebooks that are best accessed in the order listed:
- 01_Yelp API
- 02_Data Cleaning
- 03_Combining Data
- 04_Regression Using PCA
- 05_K-means Clustering
- 06_Hierarchical Clustering
  
## Using Yelp to categorize businesses by Lifeline
This is something that can be done using Yelp's API.  In our notebook titled "Miami Lifelines" we demonstrate the necessary code to retrieve business information.  To ensure that we were returning relevant businesses we went through each of the 1,339 possible Yelp categories line by line (view them here: https://www.yelp.com/developers/documentation/v3/category_list) and the ones that we felt would return businesses that could serve as one of the lifelines.  The relevant categories are as follows:
- (1) Police Department, Fire Department
- (2) Homeless Shelters, Community Centers, Food Banks, Animal Shelters
- (3) Hospitals, Emergency Rooms, Emergency Medicine, Medical Centers
- (4) Utilities, Natural Gas Suppliers, Electric Suppliers, Water Suppliers, Fuel Docks, Service Stations
- (5) Telecommunications, Print Media, Radio Stations, Television Stations
- (6) Airlines, Bus Stations, Ferries, Metro Stations, Public Transportation, Trains, Taxis
- (7) Biohazard Cleanup, Hazardous Waste Cleanup

The code in the notebook can be used to return information within those categories for a business in any city, state, or zip code.  Some caveats to consider:
  * Categories can be passed as a parameter all at once.  As is shown in the notebook we separated them by lifeline to make it easier to label each business with the appropriate number.
  * Categories must be entered as a string, as one lower case word, and (if searching for multiple categories at a time) as a list.  For example when we searched for businesses that would be labeled as lifeline number seven, we did the following - 'categories': ['hazardouswastecleanup', 'biohazardcleanup'].
  * The 'radius' parameter can be a maximum of 40,000 meters (25 miles).  It is passed as - 'radius': 40000.
  * The maximum businesses the API will return in one search is 50.  The limit parameter is passed as - 'limit': 50.  If there are more than 50 businesses in a set of categories (as was the case in our health/medical and energy lifelines) than the offset parameter needs to be included the next time the code is run so that the second set of 50 businesses gets returned - 'offset': 50.  Each step throughout the entire process is further explained within the notebook.  We chose the city of Miami, Fl to demonstrate how the tool works.


## Beyond the Deliverable -- Estimating Disaster impact
Regarding the second part of our problem statement - there was a problem using the data available on Yelp to quantify potential disaster impact.  Aside from being able to get a count of how many potential lifelines there isn't much else in the way of information.

To go beyond the scope of Yelp to deliver disaster impact we sought information from the Florida Office of Economic and Demographic Research, the Florida Office of Insurance Regulation, and the Florida Hospital Association.  An example of additional data that these sources provided includes the following:
  * Number of businesses by industry - Natural Resource and Mining, Construction, Manufacturing, Trade/Transportation/Utilities, Information, Financial Activities, Professional Business Services, Education and Health, Leisure and Hospitality, and Government.
  * Infrastructure such as number of bridges and highway miles
  * Hospitals
  * State Facilities
  * Residential and Commercial Insurance Claims after Hurricanes Michael (2018), Irma (2017), Hermine (2016), Matthew (2016)

## Issues
The limited data from Yelp can only be collected by city, state, or zip code whereas all of our supplemental data is available only at the county level making us unable to cross reference the data.  Furthermore, the features available in our supplemental data did not prove to be reliable predictors for potential residential and commercial insurance claims which proved to be our only available target to predict with supervised learning.  Our attempts to group counties in a meaningful way also proved to be fruitless.


## Suggestions
If the goal is to have a tool that can categorize businesses by lifeline in a given state, city, or zip code by using Yelp data, that can be done.  However if a more tangible metric is desired for estimating impact beyond a count of businesses by lifeline, Yelp would have to make more information available such as:
  * Revenue
  * Number of Employees
  * Specific services provided
