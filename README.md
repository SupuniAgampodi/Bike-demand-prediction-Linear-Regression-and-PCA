# Analysis of Soeul Bike Sharing Demand
Rental bikes have been introduced in numerous urban cities to enhance the convenience of mobility. Ensuring the availability and accessibility of rental bikes to the public at the right time is of paramount importance, as it reduces waiting times and contributes to a smoother urban transportation experience. Consequently, maintaining a stable supply of rental bikes within the city becomes a significant concern.
A critical aspect in addressing this concern is accurately predicting the number of bikes required at each hour to ensure a stable supply of rental bikes. To address this challenge, a dataset has been utilized, comprising over 8465 records of bike counts in Seoul, Korea. This dataset was sourced from the UCI Machine Learning Repository and includes corresponding weather data and holiday information.
This analysis of Bike Sharing Demand aims to answer two key questions:

a) Is there an association between the season and the hour of the day with the count of rented bikes?

b) Which features or factors play the most crucial role in predicting bike counts accurately?


## Data Set 
https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand

## EDA


![image](https://github.com/user-attachments/assets/0d14b046-7e5d-4fc2-9ba4-152dceb01b32)


![image](https://github.com/user-attachments/assets/e8dfe819-1942-4c29-b59b-2d874277e97c)


![image](https://github.com/user-attachments/assets/f08cf0fa-fe13-40a6-9745-1afe8091a508)


## Principal Component Analysis

Model	
BikeCount ~ Seasons	

BikeCount ~ Hour	

BikeCount _Count ~ Seasons + Hour	

BikeCount ~ Seasons + Hour + DewPoint+ Humidity + Temp	

BikeCount ~ DewPoint + Humidity + Temp

BikeCount ~ Dew_Point + Humidity

BikeCount ~ DewPoint + Temp	

BikeCount ~ Humidity + Temp	

BikeCount ~ DewPoint	

BikeCount ~ Humidity	

BikeCount ~ Temp	

![image](https://github.com/user-attachments/assets/a4ad36bc-487f-4779-9c04-98b7d076f70b)

![image](https://github.com/user-attachments/assets/ed0dc1c4-38b2-4efa-b244-d8a42172c4b8)

