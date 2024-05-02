### Project Team members:  HEMANTH THUMMA (0992722), KUNA NAVEEN KUMAR (0983287)

# Bike sharing prediction

## Introduction

Bike sharing systems automate the entire process of bike rentals, from membership to return. These systems allow users to hire bikes from one location and return them to another. Currently, there are about 500 bike-sharing schemes worldwide with over 500 thousand bicycles. These systems are highly valued for their impact on traffic, the environment, and health issues. 

Bike sharing systems have a distinct advantage over traditional transportation services in that they record journey, departure, and arrival times, thereby creating a virtual sensor network for urban mobility. This data can be utilized to identify significant occurrences, making it appealing for research. Unlike other modes of transportation, these technologies may be utilized to monitor and analyze traffic patterns in cities.


##  Dataset

The dataset is downloaded from the kaggle

###  Fields Description

Before we begin reading the dataframe, below are the descriptors for the relevant columns.

instant - A unique sequential ID number for each row
dteday - The date of the rentals
season - The season in which the rentals occurred
yr - The year the rentals occurred
mnth - The month the rentals occurred
holiday - Whether or not the day was a holiday
weekday - The day of the week (as a number, 0 to 7)
workingday - Whether or not the day was a working day
weathersit - The weather (as a categorical variable)
temp - The temperature, on a 0-1 scale
atemp - The adjusted temperature
hum - The humidity, on a 0-1 scale
windspeed - The wind speed, on a 0-1 scale
casual - The number of casual riders (people who hadn't previously signed up with the bike sharing program)
registered - The number of registered riders (people who had already signed up)
cnt - The total number of bike rentals (casual + registered)

## Prediction Goal

Our target is to predict the total number of bikes people rented in a certain temperatures (cnt column).

Predictions regarding bike sharing can be used in production by bike sharing companies to improve operations. They can use predictions to predict demand, manage resources efficiently, and ensure there are enough bikes available in high-demand areas during peak periods. 

### EDA

In model 1:
X variables are : 'instant', 'season', 'yr', 'temp', 'atemp', 'casual', 'registered'.
Y variable are  : 'cnt'.

In model 2,3,4,5:
X varibles: 'instant','season','yr','mnth','hr','holiday','weekday','workingday','weathersit','temp','atemp','hum','windspeed'
Y variable : 'cnt'.

(17379, 17)

 There are a total of 17 features with a total of 17379 observations.

 ![alt text](image-7.png)

 instant       0.629896
season        0.404584
yr            0.569728
mnth          0.278191
holiday      -0.068764
weekday       0.067534
workingday    0.062542
weathersit   -0.295929
temp          0.627044
atemp         0.630685
hum          -0.098543
windspeed    -0.235132
casual        0.672123
registered    0.945411
cnt           1.000000
Name: cnt, dtype: float64

we won't use features like casual and registered because adding the two yields the cnt column. We want to estimate the total number of bikes hired in a particular hour. If we already know the casual and registered values, any prediction is basically useless.

Looking at the dataset, we can see that almost all the features are numerical, thus we won't have to do much cleaning.

### Model fitting:

The data is divided in 80 to 20 ratio where 80 percent consists of training data and 20 percent consists of test data

The data has no dataleakage issue as it is not a time series data

In this project we have used model like Linear regression,decision trees and random forest.

We can easily observe that several variables have moderate to strong correlations with the target variable. Hence, a Linear Regression Model will be a suitable fit. A Linear Regression model is an excellent choice when the variables are correlated but also independent, which means they do not alter meaning when combined.

The error is high with linear regression. It is safe to say that our model is not a good fit. So now let's take a look at another supervised machine learning algorithm: decision trees. One of the primary advantages of decision trees is their ability to detect nonlinear relationships between variables, whereas Linear Regression lacks.

While Decision Trees are better at predicting outcomes, they are prone to overfitting. There are some approaches for reducing overfitting in a decision tree. They are as follows:

Restrict the depth of the tree as we build it
Using ensembling to blend in predictions from multiple trees

We have tried models like multilinear regression but we had a very hard working with the rfe part.

We have tuned hyper parameters for the random forest. The tuning parameters are as follows:

param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [None, 10, 20],
    'min_samples_split': [2, 5, 10]
}

### Validation / metrics:

In our project we mainly focused on the metric called error as we primarily focused on reducing the error using different models with adding variations to it.


    Model	                                                  Error Value
0	LR - Restricted features	                             838431.716612
1	LR - Added Features	                                     796043.980231
2	Decision Tree - Same columns as LR Added Features        739959.534247	
3	Decision Tree - SF, Min Sample Leaf -                    721326.552281
4	Random Forest - SF Min Sample Leaf -                     488865.761871	

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)



### Production 

Mobile applications for Bike Sharing : Mobile bike sharing apps employ GPS technology to detect nearby bikes, unlock them, and track their trips. Users can hire and return bikes using the app, making the entire procedure simple and convenient. Furthermore, these apps frequently include functionality such as payment processing, route mapping, and customer assistance to improve the user experience.

### Going further

We can improve this model by restricting the depth of the tree as we build it and using ensembling to blend in predictions from multiple trees.We can continue to keep tweaking the model, features etc. to get the model with the best fit


