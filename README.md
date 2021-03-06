# Evaluating-Airbnb-in-New-York-City

# AIPI590
Readme<br />
Evaluating Airbnb in New York City<br />
Author: Jay Lin, Joanne Xiao, Ningyi Xue<br />
 <br />
Presentaion Slide Decks: AIPI Final Project.pdf

Business Understanding<br />
Problem to Solve<br />
- New York is most favorable places for tourists: 65.2 m visitors in 2018
- Help tourists to make decisions that fulfill their need and help them have a better experience during their trips in New York by adding new metrics: safety (crimes within 2 miles), convenience (subway stations within 5 miles), availability within a year
Current State
- Airbnb names can be misleading by containing certain characteristics in the listing description, like “close to subway”, “convenient”, “safe and quite”, etc.
- Airbnb booking system is inconsistent with unclear definition
- Recommends rooms partly based on the number of reviews and the ratings by customers; customer ratings might be biased: 
    - Owners of listings might offer incentives for customers for high review
    - The most reviews are more recommended but the less reviewed could offer better service
    - Customer ratings are given based on these metrics: Cleanliness, Staff & Service, Amenities, Property condition & facilities
Key Stakeholders<br />
- Tourists and business travelers that prefer at-home experience during their trips in New York
- Owners of the Airbnb listings and the hotels

Defining Business Success<br />
Quantifying Expected Impact
- By adding more information about each Airbnb listing, customers can use this tool to better determine what best fits their needs
- Customers’ satisfaction rate for each stay would increase, and Airbnb owners can better understand ways to improve their listing to attract more tourists
Success Metrics
- Technical: search tool to ask for users’ input for hotel names, search the name in database, and return the related information about that hotel
- Business: The revenue and profitability will likely both go up for some of the Airbnb listings. Because of the more accurate match of customers’ needs, there might be more higher reviews given by the customers. 
Constraint
- The tool cannot cover all the aspects in the real world, it can only give people more information to look at
Define success targets for metrics
- The new searching tool needs to better help customers find the stay fits their needs, therefore, the returning customers would increase.

Ethical<br />
We currently dropped all other columns except ‘Year of crime’, ‘Latitude’, ‘Longitude’, and ‘neighborhood/district’ of each crime, because we believe in this analysis, however, for different users, other attributes such as sex, gender, race may have different levels of impact of their search and corresponding result. 

We also did a random sampling to fairly decrease the size of the sample of crime to 10000 in order to perform some calculation and functions. However, this may also lead the result to an unfair outcome. 

Tools and Dataset<br />
Programming Languages & Packages
- Python<br />
    - Pandas<br /> 
    - Numpy  
    - Matplotlib.pyplot  
    - sklearn.neighbors  
    - Folium  
    - folium.plugins  
    - geopy  
Dataset
- Airbnb Dataset: http://insideairbnb.com/get-the-data.html
- Subway station : https://data.cityofnewyork.us/Transportation/Subway-Stations/arq3-7z49
- NYPD crimes : https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i

Steps of Running Codes<br />
I.	Airbnb
1.	We created a notebook called “Airbnb.ipynb”.
2.	We downloaded the dataset from the above-mentioned website and converted the data into a dataframe.
3.	We understood the data by displaying the columns and the shape of the dataframe.
4.	We identify outliers (zero availability and prices with z score > 3 or < -3). We dropped these outliers and dropped them.
5.	We dropped some unnecessary columns.
6.	We output the cleaned data to a csv file, called 'Cleaned_Airbnb.csv', for our next step.

II.	Crime
1.	We downloaded the dataset from above-mentioned website. The dataset is too large to upload to Github so we had to run this csv file locally. We attached the file in our zip for reference.
2.	We created a notebook called “Crime cleaning.ipynb”.
3.	We did some cleaning of the data to extract the key information we need from this project: latitude, longitude, patrol area (patrol_boro)
4.	Because the raw data was too large (over 100,000 instances), we couldn’t run the analysis. We came back to this file to do random sampling of 10,000 instances after our kernel failed to run.
5.	We output the cleaned data to a csv file, called 'sampled_crime.csv', for our next step.
![Image of Error](https://github.com/ningyixue/AIPI590/blob/main/error.png)

III.	Station
1.	We created a notebook called “station_the_geom.ipynb”.
2.	We downloaded the dataset from the above-mentioned website and converted the data into a dataframe.
3.	We dropped some unnecessary columns.
4.	We output the cleaned data to a csv file, called “station_geom.csv”, for our next step.

IV.	Others
1.	We made some other attempts to understand the data. For example, we reversed the longitude and latitude of the crime to find the addresses and zip codes with package “geopy”, and we tried to display crimes by zip codes. But later on, we realized it didn’t better refine our result or strengthen our understanding of the results, so we decided not to use it in our analysis. We put these in the folder called “other attempt”. 
2.	In efforts to understand the data, we did analysis of Airbnb data and the crime data. We displayed the data on heatmap and visualize the data through plots (bar, trends, boxplot, etc.). We found some interesting trends of these datasets and identify some outliers. Although this step to understand the datasets didn’t change our final result by a lot, it was important for us to understand the data so we can figure out what our next steps can be. 

V.	Calculation of The Distance Using Longitude and Latitude
1.	We created a notebook called “Calculation.ipynb”.
2.	We imported sklearn.neighbors. 
3.	We read the previous cleaned csv files: 'Cleaned_Airbnb.csv', 'sampled_crime.csv', and “station_geom.csv” and convert them into dataframes.
4.	We merged these dataframes and calculated the distances using the longitude and latitude information of these data.
5.	We filtered the subway stations within 0.5 miles of each Airbnb listings and the crimes within 0.3 miles of each Airbnb listings. 
6.	We output the incorporated information of subway stations and crimes for each Airbnb listings to a csv file, called “Airbnb_with_station_crime.csv”, for our next step.

VI.	Visualization
1.	We created a notebook called “visualization.ipynb”.
2.	We imported matplotlib.pyplot, folium, folium.plugins in preparation to display the Airbnb listings through an interactive map. 
3.	We read the previous cleaned csv files: 'Cleaned_Airbnb.csv', 'sampled_crime.csv', and “station_geom.csv” and convert them into dataframes.
4.	We created an interactive map and added the information on these dataframes on to the map, which allows people to zoom in and zoom out the check the Airbnb listings that they are interested in, while viewing the number of crimes and subway stations nearby.

VII.	Airbnb Scoring 
1.	We use the notebook “visualization.ipynb”.
2.	We read the previous cleaned csv files, “Airbnb_with_station_crime.csv” and convert them into dataframes.
3.	We normalized the number of subway stations and convert into score through this formula:  
![normalization](https://github.com/ningyixue/AIPI590/blob/main/normalization_1.png)<br />
We use this score to indicate the convenience of the Airbnb listings, 0 being least convenient and 10 being most convenient.
4.	We normalized the number of crimes and convert to score through this formula:
 ![normalization2](https://github.com/ningyixue/AIPI590/blob/main/normalization_2.png)<br />
We use this score to indicate the safeness of the Airbnb listings, 0 being least safe and 10 being safest.
5.	We repeated the previous step, visualization, in order to display the top recommended Airbnb by area. We created an interactive map and added the information on these dataframes on to the map, which allows people to zoom in and zoom out the check the Airbnb listings that they are interested in, while viewing the number of crimes and subway stations nearby.
