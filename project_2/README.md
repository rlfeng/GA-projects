# Project 2 - Ames Housing Data and Kaggle Challenge


## Problem Statement

To create a regression model based on the Ames Housing Dataset that can predict the most accurate sale price vs other competitors. The success of the model is quantified by Root Mean Square Error(RMSE) method by comparing predicted sale price to actual values on Kaggle.com.

An accurate model could be deployed by real estate companies in developing their business strategy. This includes making recommendations to homeowners on how to increase the value of their homes.


## Methodology

### Data cleaning and EDA
1) Combined Train and Test data sets for the ease of consistent cleaning.

2) Imputed missing values as regression models cannot process np.nan values. Dropped features with high amount of missing values (>70%) as they should have limited influence on sale price. For the rest of the features with missing values, the missing values were not missing at random (e.g. houses do not have garage will have missing values for all features related to garage). Hence, missing values were replaced with 'none'(for strings) or zero (for numerical). However, this imputation had negatively skewed some of the feature distributions. Means or medians could be used to avoid this issue.

3) Converted ordinal data to integers as sub-categories of ordinal data were related to each other and this can reduce the number of features. Dummies were obtained for remaining categorical (nominal data) so they could be used in the regression model as linear regression only accepts numberical variables.

4) Rejected features with P-value higher than 0.05 through backward elimination using OLS by fitting individual features with target.

5) Evaluated top correlated features to target through heatmap. However, some features were not only correlated with target but also strongly correlated with each other. The use of Lasso regression could eliminate this issue. The distribution of sale price (target) was positively skrew due to small number of super expension houses.

6) Outliers were identified by plotting gr_liv_area (one of the features highly correlated with sale price) against sale price. Two outliers were spotted visually and dropped from the Train data set.

### Model
1) Splitted the cleaned data back to Train and Test sets. Performed train-test split on Train set.

2) Scaled data for both Train and Test sets.

3) Cross Validation using Linear Regression, Lasso and Ridge Regressions. Lasso obatained the highest score.
    - Linear regression score: -8.71x10^19
    - Lasso score: 0.83
    - Ridge score: 0.81


## Results

4) Lasso regression was selected for model fitting with optimum alpha  using X train data (train data set). The R squared for test data was slightly lower than train data. This meant Lasso model contain certain amount of variance and reasonable bias (R2~0.8).
    - Optimum alpha: 795
    - Lasso score for X_train_scaled and y_train: 0.89
    - Lasso eliminated 57.6% of the features (84 out of 198 features coefficients were non-zero)
    - Lasso score for X_test_scaled and y_test: 0.90
    - Calculated RMSE for y_test: 24856

5) Predicted target sale price. Same lasso model was fitted to test data set to predict target. Submitted result to Kaggle and scored 33,686.


## Business Recommendations

1) Based on Lasso's feature selection, the top 10 features most valuable to a home are listed below:
    1. GrLivArea: Above grade (ground) living area square feet
    2. OverallQual: Overall material and finish quality
    3. (NridgHt Northridge Heights) Neighborhood: Physical locations within Ames city limits
    4. (StoneBr Stone Brook) Neighborhood: Physical locations within Ames city 
    5. ExterQual: Exterior material quality
    6. BsmtExposure: Walkout or garden level basement walls
    7. (No Ridge) Neighborhood: Physical locations within Ames city limits
    8. KitchenQual: Kitchen quality
    9. GarageCars: Size of garage in car capacity
    10. ScreenPorch: Screen porch area in square feet
    

2) The top 5 features that could hurt the value of a home are: 
    1. MSSubClass: The building class (190 2 FAMILY CONVERSION - ALL STYLES AND AGES)
    2. MiscVal: $Value of miscellaneous feature
    3. BldgType: Type of dwelling (TwnhsE Townhouse End Unit) 
    4. PoolArea: Pool area in square feet
    5. (Edwards Edwards) Neighborhood: Physical locations within Ames city limits

3) Homeowners could renovate their houses to improve the overall quality of the home which is one of the most important feature that determines the value of the house.

4) A good investment is in NridgHt Northridge Heights.

5) The current model does take into account universal factors like space, number of bathrooms, home quality, etc. However, to extend the model to other cities, the model should also include features that could differentiate the cities:
    - Supply and demand
    - Interest rates
    - Economic growth
    - Demographics
    - Good/bad neighborhoods relevant to respective cities

reference: https://www.homeguru.com.au/house-prices
