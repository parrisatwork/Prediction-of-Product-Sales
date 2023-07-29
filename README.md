# **Prediction of Product Sales**
- **Author:** Parris Trimingham

# Business problem:
Since our end goal is to increase sales, we can produce a few charts that will help us to see the properties of products, and trends, that play a crucial role for the company. There are many factors that can be used to promote the sales of an outlet item. Does weight or fat content play a role? We can analyze the past, to predict the future. Will history repeat itself?

# Data Dictionary:
![image](https://user-images.githubusercontent.com/128560277/236364869-aae3c407-9332-4f99-95a5-0a22af222a47.png)

For this dataset, there are 8523 rows, and 12 columns.

# Exploratory Data Analysis
- A boxplot and histogram are used to help visualize for each numeric datatype column. 
- And a barplot is uses to visialize for each categorical column.
- This gives a good baseline for all of the numeric and categorical columns for univariate EDA.

# Analyzing Item Outlet Sales versus Item Weight
![image](https://user-images.githubusercontent.com/128560277/236365991-b7d5b3ca-e986-4ccb-9090-158f8c2fd448.png)

This histogram shows that the majority of the Outlet Sales are around the 12.5 item weight.

# Analyzing Total Items Sales, by Type
![image](https://user-images.githubusercontent.com/128560277/236366154-1932d869-6162-45d8-8371-bc190bc8c194.png)

This barplot shows that Fruits and Vegetable has the most Outlet Sales.

The top five highest item sales are as follows:
- Fruits and Vegetables
- Snack Foods
- Household
- Frozen Foods
- Dairy

# Recommendations:
By using the Decision Tree with the R Squared (R2), the score came to a 1.0. We can utilize that to make future predictions. And then ,we can focus on Item Sales.

***
# Project 1 - Revisited Part 2: Explaining Models with SHAP

## Summary Bar Plot RandomForestRegressor
![summary_bar_plot_rf_reg](https://github.com/jonnunez92/Prediction-of-Product-Sales/blob/main/Data/summary_plot_bar_rf_reg.png?raw=true)

### Comparison with RandomForest Regressor Feature Importance

#### Default Feature Importances
![rf_default_importances](https://github.com/jonnunez92/Prediction-of-Product-Sales/blob/main/Data/rf_default_importances.png)

#### Permutation Feature Importances
![rf_perm_importances](https://github.com/jonnunez92/Prediction-of-Product-Sales/blob/main/Data/rf_perm_importances.png)

#### Differences
- Default and Permutation Importances have the same top 5 features

- SHAP Plot Summary differs in that:
    - 'Item_Visibility' is ranked lower (5th instead of 3rd)
    - 'Outlet_Type_Supermarket Type 3' takes the place of 'Item_Weight' (ranked 4th)
    - 'Outlet_Identifier_OUT027' is ranked higher (3rd instead of 5th)

 ## Summary Dot Plot RandomForestRegressor
 ![summary_plot_dot_rf_reg](https://github.com/jonnunez92/Prediction-of-Product-Sales/blob/main/Data/summary_plot_dot_rf_reg.png?raw=true)

 ### Summary Dot Plot Interpretation

**Interpret Top 3 Features**

- 'Item_MRP':
    - As the value of the item's MRP increases (gets redder), the target value ('Item_Outlet_Sales') increases as well (moves right)


- 'Outlet_Type_Grocery_Store' (true/false):
    - Being a Grocery Store (red/true) will decrease (move left) the target value ('Item_Outlet_Sales')
    - Not being a Grocery Store (blue/false) will increase (move right) the target value ('Item_Outlet_Sales')
    
    
- 'Outlet_Identifier_OUT027' (true/false):
    - Being Outlet OUT027 (red/true) will increase (move right) the target value ('Item_Outlet_Sales')
    - Not being a Outlet OUT027 (blue/false) will only marginally affect (keep center at 0 or slightly move left) the target value ('Item_Outlet_Sales')

***

# Local Explanations
- Comparing 'High' and 'Low' sales stores. In order to express the main differences between a store that performs well and a store that doesn't perform well.

## SHAP Local Force Plot

### High Sales
![force_plot_high_sales](https://github.com/parrisatwork/Prediction-of-Product-Sales/blob/main/force_plot_high_sales.png)
- Significant 'push' towards the right indicating higher sales
    - Major features:
        - 'Item_MRP'
        - 'Item_Visibility'
        - 'Item_Weight'
        
- Only one feature pushing left (lower sales):
    - 'Outlet_Type_Supermarket Type3'
 
### Low Sales
![force_plot_low_sales](https://github.com/parrisatwork/Prediction-of-Product-Sales/blob/main/force_plot_low_sales.png)
- Significant 'push' to the left (lower) indicating lower sales
    - Major features:
        - 'Outlet_Type_Grocery Store'
        - 'Item_MRP'        
        
- Seems to be no features pushing right (higher sales)

## Lime Tabular Explanation

### High Sales
![lime_high_sales](https://github.com/parrisatwork/Prediction-of-Product-Sales/blob/main/lime_high_sales.png)
- Predicted Value is 6693.23 where True Value is 8323.8316

- Interpreting our Features with the 'negative' and 'positive' bar chart
    - Positive (higher sales) include:
        - 'Outlet_Type_Grocery Store' (not a Grocery Store)
        - 'Item_MRP' (greater than 180.25 at 219.35)
    - Negative (lower sales) include:
        - 'Outlet_Identifier_OUT027' (not this Outlet)
        - 'Outlet_Type_Supermarket Type3' (not this Outlet Type)
    - Even though the Feature Names are cutoff, they can be seen in the bottom graph (Feature/Value)
 
### Low Sales
![lime_low_sales](https://github.com/parrisatwork/Prediction-of-Product-Sales/blob/main/lime_low_sales.png)
- Predicted Value is 63.42 where True Value is 36.62

- Interpreting our Features with the 'negative' and 'positive' bar chart
    - Negative (lower sales) include:
        - 'Outlet_Type_Grocery Store' (is a Grocery Store)
        - 'Item_MRP' (less than or equal to 90.72 at 35.22)
        - 'Outlet_Identifier_OUT027' (is not this Outlet)
        - 'Outlet_Type_Supermarket Type3' (is not this Outlet Type)
    - Positive (higher sales) include:
        - 'Item_Type_Seafood' (is not this Item Type)
        - 'Outlet_Identifier_OUT045' (is not this Outlet)
    
    - Even though the Feature Names are cutoff, they can be seen in the bottom graph (Feature/Value)

# For further information
For any additional questions, please contact parrisatwork@gmail.com.
