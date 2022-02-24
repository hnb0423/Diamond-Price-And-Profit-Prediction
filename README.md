# Diamond-Price-And-Profit-Prediction
Business problem:
The goal of this project is to predict diamond trade price and generate most amount of profit with $5,000,000 budget. 
 
## Data Processing:
I take seven steps to finish data processing.
	    
Step 1: Convert data type

After checking data types in the “training” and “offers” dataset, I convert variables, "Cert", "Clarity", "Color", "Cut", "Known_Conflict_Diamond", "Polish", "Regions", "Shape", "Symmetry", "Vendor", into categorical variables.  
 
Step 2: Convert null to N/A

For both datasets, I convert null values in “Cut” column to N/A
	    
Step 3: Count missing values

For both datasets, I count number of missing values (N/A) by each column
	    
Step 4: Handling missing values 

For numeric variables, “Depth” and “Table,” in both datasets, I replace the missing values with mean values of the columns. For categorical variables, “Cut”, “Polish”, “Cert”, and “Symmetry” in both datasets, I count the frequency of categories in each column. Then, I replace missing values in “Polish,” “Cert,” and “Symmetry” with most frequent classes in their columns. Since column “Cut” has almost 50% of missing value, I decide to create a new category called “Unknown” and replace the missing values with “Unknown” for both datasets.  
 
Step 5: Split Measurements column into separate columns 

For both datasets, I split the “Measurements” column into three separate columns called “m_length,” “m_depth,” and “m_width.”
 
Step 6: Drop not useful columns

In the “offers dataset, most values in the “Know_Conflict_Diamond” column are missing. Thus, I decide to drop the ““Know_Conflict_Diamond” column in both datasets.
 
Step 7: create profit and logprofit column in training dataset

I create “profit” and “Logprofit” columns through the calculation of column “Retail” minus “Price.”
 
## EDA on training data:
I conduct detailed vendor analysis in this section. First, I calculate profit margin through the formula (Retail – Price)/ Retail. I build a density plot of profit margin by each vendor to study the vendors who bring us low profit margins. In this way, I can determine which vendors are overcharging or undercharging. 
Next, I construct four histograms of price by each vendor to study price distribution. By doing so, I am able to see whether the vendors sell the same type of diamonds. If they sell diamonds with the same price ranges, it is highly possible that they sell similar types of diamonds. To further study the type of diamonds that vendors sell, I build a density plot of carats by each vendor. 

To study the relationship between Carat and diamond, I construct two scatterplots: one is “Carats vs Retail Price,” and the other is “Carats vs Log Retail Price,”
Finally, I construct a scatterplot matrix to study relationships among variables, and I find that there are strong correlations among predictors m_length, m_width, m_depth, and Carats which indicate multicollinearity. Thus, I decide to not use linear regression. Instead, I decide to use lasso and ridge regression. Both models apply regularization techniques, reducing variance by either introducing bias or prohibiting size of coefficient to close to zero. Lasso and ridge regression can effectively reduce the problem of overfitting.     

## Feature engineering:
I take six steps to complete feature engineering.

Step 1: Re-categorize columns

I notice that columns “Color,” “Clarity,” “Symmetry,” “Shape,” and “Polish” either have different categories or have typos for the training and offers datasets. So, I need to resolve this mismatch issue through re-categorization. I only keep top frequent categories for each column and replace the rest with “Other” categories. I also correct typos in “Shape” column. 

Step 2: Create dummy variables for both datasets 

I dummy code all categorical variables in both datasets.

Step 3& 4& 5 & 6:

I apply small adjustments to keep testing and training data to be consistent, and I split training datasets into one with predictors and another with response variables only. 

## Models Construction:
For price prediction, I use both linear and non-linear approaches. For linear approaches, I run lasso and ridge regression. I pick these two models because they add penalty terms to avoid overfitting, and they take collinearity among variables into consideration. For non-linear approaches, I run decision tree and random forest, as they can handle regression task without problem, even though they are tree-based models. By comparing the MSE, and RMSE across the four models, I find that random forest performs the best, with the smallest mean MSE(0.038) and mean RMSE(0.196). So, I decide to use random forest for diamond price prediction

For retail price prediction, I run both linear and non-linear models, including lasso regression, ridge regression, and random forest. I find that random forest also performs best across the three models with (0.24) mean MSE and (0.49) mean RMSE. Thus, I pick random forest for diamond retail price prediction as well. 

## Diamond Selection for Trading: 
After predicting the price and retail price for all diamonds in the “offers” dataset, I calculate the predicted profit and predicted profit margin for each diamond. Since I find that diamonds sold by Vendor 4 usually generate lower profit margin than others, and Vendor 4 has a negative mean profit margin, I decide to not take Vendor 4 into consideration for trading diamonds. 

After excluding Vendor 4, I select diamonds with at least 25% profit margin and sum the predicted price, which is $743 618. However, I only have a $5,000,000 budget. So, I decided to select diamonds based on profit margin in descending order. The higher the profit margin, the more cents of profit will be generated for each dollar of sale. I end up selecting 699 diamonds with a total price of $4,994,703. 
