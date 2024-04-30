## Final Project Submission

Please fill out:
* Student name: Matilda Odalo, Mark Bundi, Charles Kagwanja, Wycliffe Orimba
* Student pace:  part time 
* Scheduled project review date/time: 
* Instructor name: 
* Blog post URL: 


## Business Problem

The business problem in this scenario involves providing homeowners with advice on how to increase the estimated value of their homes through renovation projects. 

## Data Understanding

This project uses the King County House Sales dataset, which can be found in kc_house_data.csv. 

The data is used to create regression models that predict the trend of house prices in relation to specific varibles

he description of the column names can be found in column_names.md in the same folder. As with most real world data sets, the column names are not perfectly described, so you'll have to do some research or use your best judgment if you have questions about what the data means.

It is up to you to decide what data from this dataset to use and how to use it. If you are feeling overwhelmed or behind, we recommend you ignore some or all of the following features:

- date
- view
- sqft_above
- sqft_basement
- yr_renovated
- zipcode
- lat
- long
- sqft_living15
- sqft_lot15

## IMPORTED LIBRARIES

The following Python Libraries were imported and utilised in the  projects: 
- pandas
- numpy
- statsmodels.api
- matplotlib.pyplot
- seaborn as sns
- datetime as dt
- math
- sklearn.linear_model import LinearRegression
- scipy.stats as stats

### Summary of data

The data has six non-numeric columns that will need to be manipulated or removed before regression analysis: "date", "waterfront", "view", "condition", "grade", and "sqft_basement". We dropped certain columns that we won't be using in our model.

## Data Preparation
Waterfront and years_renovated have missing values. We converted the data type in the "Waterfront" and "Year_Renovated" columns to be either "1" or "0" in order to eleminiate "YES", "NO" and null values. 

### Outliers

When we ran the value_counts to check the unique values in all the columns, it was noted that there was a house with 33 bedrooms. We want to check if it makes sense. The house with 33 bedrooms is having square footage of living being 1620. It does not make sense to include the outlier. We tried convert the datatype of the sqf_basement column but an error occured stating could not convert string to float: '?'. Meaning some values are missing.The decision was to make another column that included values gotten from deducting sqft_above from sqft_living. We then filled the column with binary values 0 and 1, 0 representing houses without a basement and 1 with those with a basement.

## Categorised Metrics
This is how we categorised our metrics:
- categorical data: yr_renovated, waterfront,condition_num, grade_num,sqft_basement,bedrooms, bathrooms, floors.
- continuous data: price, sqft_living, sqft_above, sqft_lot, floors.


### Observations
Sqft_living had the highest positive correlation with price being 0.7 while condition_num had the lowest positive correlation with the price. We plotted regplots to conduct Linearity checks for the continuous data that will help us in spotting multicollinearity. We note that sqft_living has a high positive correlation with the price. This means that the high the square footage of living the higher the price. From the above regression plot, we note that sqft_above has a moderate correlaton with the price. As the value of sqft_above increases, there is a moderate increase in price. From the above, there is a low positive correlation between sqft_lot and the price. This means an increase in sqft_lot values has a minimum effect on the price. We note that sqft_living and sqft_above have high correlation between each other. We decide to drop sqft-above to avoid multicollinearity issues.
    
### Baseline Model
The baseline model is a simple model  used to contextualize the results of trained models. We create the basiline model to provide a reference point for measuring the performance of other models. We start with a simpler model as our base and work through it to make a much better base. In this instance we used y = price as the dependent variable and square foot living independent varible

### Observations
On our baseline model, we have an R-squared value of 0.601 meaning that 60.1% of variation in price is due to the independent variables. The RMSE of the train set is 232918.7 and the RMSE of test set is 229101.3.The baseline model also has a skew of 2.942 which means that it is positively skewed. This means the dataset has a high percentgae of outliers.
It has a high Kurtosis of 34.037 indicating the dataset has high outliers. We also note that Floor has a p-value of 0.418 which is greater than alpha(0.05) indicating that it is an insignificant feature.

Following removal of outliers and log transformation to normalize the data, we have an R-squared value of 0.491 meaning that 49.1% of variation in price is due to the independent variables. The RMSE of the train set is 0.3183210543467515 and the RMSE of test set is 0.31652284300899786. Model 1 also has a skew of -0.077 which is not very significant. The data is more normally distributed. It has a high Kurtosis of 2.910 indicating the dataset has few outliers.

## Conclusion 
The R-squared of model one is 0.491 compared to 0.493 of our baseline model. Though its a bit less than the baseline model, however the difference is not substantial. "Model one" is considered a better model than the "baseline model" for several reasons, despite a slightly lower R²:
- It has significantly lower kurtosis, indicating that its residuals are closer to a normal distribution, which is an assumption of linear regression.
- It also has lower skewness, suggesting a more symmetric distribution of residuals.


## Recomendations

From the regression model we can interpret that features that improve household value are in decending priority:

1. Squarefoot living 
2. Waterfront
3. Grade of the house
4. Renovation

The homeowner should focus on these features when renovating the house for maximum profits