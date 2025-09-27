# Analysis of Soeul Bike Sharing Demand

1.	Introduction

Rental bikes have been introduced in numerous urban cities to enhance the convenience of mobility. Ensuring the availability and accessibility of rental bikes to the public at the right time is of paramount importance, as it reduces waiting times and contributes to a smoother urban transportation experience [3]. Consequently, maintaining a stable supply of rental bikes within the city becomes a significant concern.
A critical aspect in addressing this concern is accurately predicting the number of bikes required at each hour to ensure a stable supply of rental bikes [2]. To address this challenge, a dataset has been utilized, comprising over 8465 records of bike counts in Seoul, Korea. This dataset was sourced from the UCI Machine Learning Repository [1] and includes corresponding weather data and holiday information.
This analysis of Bike Sharing Demand aims to answer two key questions:
a) Is there an association between the season and the hour of the day with the count of rented bikes?
b) Which features or factors play the most crucial role in predicting bike counts accurately?

Data Set 
https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand

2.	Methods and Analysis
   
2.1.	Notation and Subsetting

Throughout this document, variable names in the dataset will be written in italics and abbreviated where appropriate, for example, Rented Bike Count will be referred to as BikeCount, Wind Speed as Wind and Dew Point Temperature as DewPoint.
The summary statistics for the variable FunctioningDay reveal that there are 295 instances of non-functioning days in the dataset. On these non-functioning days, the bike count consistently registers as zero. This is because, on non-functioning days, the bicycles are not available for rental, and consequently, no one can rent them, as illustrated in Figure 1. Therefore, the data points corresponding to non-functioning days have been removed from the dataset as they are not pertinent to our analysis. After this removal, the dataset now contains 8465 data points.
Analysis was done with the R programming language with Rstudio and packages such as MASS, ggplot2, dplyr, purrr, devtools, plyr, scales and bootstrap were used where required.

2.2.	Overview of the Data

Notably, the bike count data is right-skewed, indicating that there are more hours with lower demand for bike rentals than hours with higher demand. 

In Figure 2, the Hourly Bike Count Bar Plot, we can discern significant patterns in the demand for bike rentals over the course of a day. Notably, the hours between 1 am and 6 am consistently exhibit a low mean demand, with fewer than 500 bike counts, suggesting minimal bike rental activity during these early morning hours. In contrast, there are prominent spikes in demand at 8 am and 6 pm, corresponding to the morning and evening rush hours when people commute to and from work. This indicates a higher demand for bikes during these periods, underscoring their use for daily work commutes. Furthermore, there is a gradual increase in demand throughout the daytime hours, reaching its peak at 6 pm, mirroring work schedules. After 6 pm, demand diminishes, reaching its lowest point at 4 am, as individuals return home and activity decreases. These observations lead to the categorization of morning hours as low-demand periods and afternoon/evening hours as high-demand times, which holds significant implications for optimizing bike availability and distribution strategies.

![image](https://github.com/user-attachments/assets/0d14b046-7e5d-4fc2-9ba4-152dceb01b32)

Fig 2. Hourly Bike Count Plot


Figure 3, the Seasonal Bike Count Plot, provides valuable insights into the seasonal variations in bike rental patterns. It is evident that weather conditions significantly influence people's preferences for cycling. During the summer, there is a notable surge in bike rentals, reflecting the preference for outdoor activities in favorable weather. Conversely, the winter season witnesses the lowest demand for bike rentals, with counts consistently falling below 500, likely due to cold weather and the possibility of snow. Notably, there are some outliers in the winter season with higher counts, indicating occasional days with more enticing weather. Surprisingly, autumn records higher bike rental demand than spring, which can be attributed to the prevalence of rainy days in spring, dissuading potential cyclists. This analysis underscores the strong correlation between weather conditions and bike rental trends, highlighting the significance of seasonality in shaping rental patterns.
<img width="940" height="466" alt="image" src="https://github.com/user-attachments/assets/21e1e555-255f-4895-8d9c-9083b2ad4bb4" />
Figure 3. Seasonal Bike Count Plot



Figure 4 provides valuable insights into bike rental demand concerning holidays. The analysis reveals that the demand for bikes is notably higher on non-holiday days, suggesting that most bike renters are likely using the service for purposes other than recreational activities. However, these will not be removed as they might not be actual outliers but instead, can be explained by other factors such as weather conditions and whether it is holiday or not, etc.
<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/87b970e1-39d8-438b-b31e-8d3980bddb52" />
Figure 4. Holiday Bike Count Plot



The histograms of continuous data variables shed light on the shape and distribution of these important factors. Lower temperatures, as suggested by the presence of hours below zero, are expected to correspond to reduced bike rental activity, which aligns with common weather-related preferences. Humidity follows a more normal distribution compared to other factors, suggesting a relatively even spread of humidity levels. Wind speed generally remains low, with a scarcity of extreme values, which is favourable for cycling. Good visibility is prevalent, and solar radiation tends to be minimal in most hours, with only a few exceptions. On the other hand, both rainfall and snowfall data exhibit strong right-skewness, indicating that high levels of precipitation are infrequent. Additionally, the temperature distribution hints at a bimodal pattern, suggesting the existence of two distinct temperature preferences within the dataset. These observations provide essential context for understanding the interplay between weather variables and bike rental demand, helping guide further analysis and modelling.
<img width="940" height="903" alt="image" src="https://github.com/user-attachments/assets/3ffe30e6-39a2-469d-a84c-dc0adabdc00f" />
Figure 5. Histograms of numerical explanatory variable.

2.3.	Linear Regression
The linear model for evaluating the relationship between BikeCount with Hour, and Season is specified as BikeCount ~ β0 + β1Season + β2Hour + ɛ (1). The analysis of the model's assumptions revealed some important insights.
Firstly, the Normality assumption was almost met, with most data points lying close to the straight diagonal line on the QQ plot. Although there were minor deviations at the tails, it can be safely assumed that the data follows a roughly normal distribution.
However, the Homoscedasticity assumption was clearly violated, as indicated by the funnel-shaped residuals plot. To address this issue, a log transformation was attempted on the dependent variable BikeCount, but this worsened the problem by causing deviations from normality in the QQ plot. Considering these challenges, the decision was made not to apply any transformation to the linear model. 

2.4.	Principal Component Analysis

To determine the most important features for predicting bike counts, a two-step approach was employed. First, Principal Component Analysis (PCA) was conducted on a set of meteorological variables, including Temperature, Humidity, Wind Speed, Dewpoint, Rainfall, Snowfall, Solar Radiation, And Visibility. The goal of PCA was to uncover underlying patterns and relationships in the data by transforming these variables into a new set of orthogonal variables known as principal components.
The scree plot analysis revealed that the elbow point occurred at the third principal component, signifying that the first three principal components collectively captured a significant portion of the total variance in the data. Retaining these three principal components was deemed reasonable for dimensionality reduction while preserving the most relevant information.
<img width="940" height="405" alt="image" src="https://github.com/user-attachments/assets/8a46805b-a5c4-41c5-a653-d7eba84a08cf" />
Fig 6: Scree Plot of Variance Accounted for each Principal Component


3.	Results and Discussion
3.1.	Part A
The variables Seasons and Hour are statistically significant according to R’s linear model summary of equation 1 in Figure 7.
<img width="695" height="787" alt="image" src="https://github.com/user-attachments/assets/39f6993e-1228-4ed4-af1b-1ab5dd7bef6e" />
Figure 7. R Summary output for the model equation 1.

According to the summary output, the linear model BikeCount ~ Seasons + Hour + ɛ provides valuable insights into the impact of different seasons and hours of the day on bike count. Here are some key findings from the model:
Seasonal Impact: The model indicates that different seasons have a significant influence on bike counts. Specifically, spring is associated with a decrease in bike counts, with an average decrease of 176.31 rentals. In contrast, summer is linked to an increase in bike counts, with an average increase of 111.51 rentals. However, winter is associated with a substantial decrease in bike counts, with an average decrease of 697.02 rentals. These findings underscore the strong seasonal variations in bike rental demand, with summer being the peak season, spring indicating a decline, and winter showing a significant drop in bike counts.
Hourly Impact: The model also reveals that the hour of the day plays a significant role in predicting bike counts. Various hours exhibit distinct coefficients, signifying their impact on bike counts. Hours from 7 to 18 have a substantial positive effect on bike counts, with the highest impact observed at 18:00 (hour18). This suggests that during these daytime hours, bike rental demand is notably higher. However, some predictors, such as hour10 and hour11, are not statistically significant (p > 0.05), indicating that they may not have a substantial impact on bike counts. This insight helps to pinpoint the critical hours for bike rental demand, enabling more effective allocation and management of bike resources.
In summary, the model highlights the importance of accounting for seasonal variations and the influence of different hours of the day in predicting bike counts. It demonstrates the significance of summer as a peak season for bike rentals, the decline in spring, and the substantial drop in winter. Additionally, it emphasizes the strong positive impact of daytime hours, particularly between 7 am and 6 pm, on bike rental demand. This information is crucial for optimizing bike sharing systems and ensuring efficient resource allocation.

3.2.	Part B
First, a linear regression model with all variables was fitted before performing PCA for dimensionality reduction and thereby performing cross validation on best subset of candidate models. Below is the R’s linear model summary.
<img width="564" height="736" alt="image" src="https://github.com/user-attachments/assets/a9fea3cc-227e-4a41-a1a3-7e8b55098807" />
Figure 8. R summary output for all variables.
The PCA results revealed that the first three principal components accounted for significant portions of the variance in the dataset, with loadings of 30.25%, 24.46%, and 13.21% for the first, second, and third components, respectively. These percentages represent the proportion of the total variance in the data that each principal component explains. By selecting these three principal components, it becomes possible to maintain most of the crucial information in the dataset while reducing its dimensionality.
<img width="940" height="401" alt="image" src="https://github.com/user-attachments/assets/bcd7ef28-394e-4b81-a432-2602a3fa7945" />
Figure 9. Cumulative Variance Explained by each Principal Component

The loadings associated with each variable on the first principal component (PC1) offer valuable insights into the contribution of each variable. DewPoint and Humidity exhibited the highest loadings on PC1, with values of 0.5466 and 0.5325, respectively. Temperature (0.3919), Visibility (0.3419), WindSpeed (0.2861), and Rainfall (0.2056) followed as variables with moderate loadings on PC1. In contrast, variables like Radiation (0.1470) and SnowFall (0.0373) had lower loadings on PC1. These loadings indicate that DewPoint and Humidity play a significant role in shaping the primary pattern revealed by the first principal component, making them essential variables to include in any model aiming to represent the primary data patterns effectively. According to Figure 8 we can examine that WindSpeed and Visibility, is not statistically significant and PCA results also confirms this.
After PCA, Cross validation was applied to 11 candidate models. Below table depicts the RMSE for each model. 

<img width="451" height="260" alt="image" src="https://github.com/user-attachments/assets/e8dd28eb-3e21-4fe2-89c7-2762bed2024e" />
The cross-validation results for various candidate models aimed at predicting BikeCount indicate that the model "BikeCount ~ Seasons + Hour + DewPoint + Humidity + Temp" performs the best, as it has the lowest Root Mean Square Error (RMSE) of 383.86. This model incorporates a combination of seasonal factors, time of day (Hour), as well as meteorological variables such as DewPoint, Humidity, and Temperature. The low RMSE suggests that this model provides the most accurate predictions for BikeCount among the alternatives.

<img width="730" height="780" alt="image" src="https://github.com/user-attachments/assets/231d865a-734c-417a-a2ee-346b01584730" />
Figure 10: R summary output for the best candidate model
Figure 10 presents the model summary output for the best candidate model. In comparing two linear regression models for predicting bike counts, first model, which includes all variables, outperforms the best candidate model which is a reduced model with fewer predictors. Model in Figure 8 exhibits a slightly higher R-squared value (0.6619), indicating a better explanation of variance in bike counts, and a lower residual standard error (374.3), indicating a better fit to the data. However, it is more complex with more predictors, which may raise concerns about overfitting. Cross-validation is a critical technique for selecting the most suitable model, evaluating its performance, and identifying potential overfitting issues. It helps in balancing the trade-off between predictive accuracy and model complexity while considering interpretability. Overall, the cross-validation results provide a more comprehensive assessment of the model's performance and its ability to generalize to different data subsets. While there's a slight reduction in accuracy compared to the initial result, cross-validation offers a more realistic view of how the model is likely to perform on unseen data, considering its variability and robustness.

4.	Conclusion
In conclusion, this analysis provides valuable insights into the factors influencing bike sharing demand in Seoul:
•	Season and hour of the day significantly impact bike rental counts, with summer and fall leading to increased demand, while winter and spring sees a notable decrease.
•	DewPoint, Temp and Humidity play crucial roles in predicting BikeCount, emphasizing the importance of weather conditions.
•	These findings can assist in optimizing bike sharing system operations and improving resource allocation.

References
1. https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand
2. https://www.koreatimes.co.kr/www/nation/2023/11/113_306366.html
3. https://www.globenewswire.com/en/news-release/2023/08/17/2727028/28124/en/Europe-Bike-Sharing-Market-Poised-for-Substantial-Growth-Expected-to-Reach-USD-7-98-Billion-by-2027.html


