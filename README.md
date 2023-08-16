# 🇩🇪 Germany Rental Analysis, Prediction.

## 🧐 Project Overview 
- Create virtualization to have a better understanding of the data of the rental cost in Germany.
Engineered features from the original variable to create a better and understanding of the factor that impacts the rental price cost in Germany.
##  📕 skills
- Data cleaning to clear the outliers and remove columns by using statistics method.
- Create virtualization to have a better understanding of the data trend of the rental in Germany.
- Create a tool that estimates the house cost predicted by using only basic variables.

## 👨‍💻 Code and Resources Used
**Requirement**: Python, Tableau

**Packages**: np, pandas, plotly, matplotlib, lightgbm, json and more.

# 🧼 Data Clearning

## Missing Values
After scraping the data, I needed to clean it up to be usable for the model. I made many changes to make the data have a better understanding.
- Removes rows that don't correlate to the Rental Price.
- Adding new columns: Price Per Square Meter, Additional Cost.
- Eliminate outliers by using statistic method such as empirical rule.
- Fill in missing numerical values by using categorical as the reference. I could know what could be the best reference by using Correlation Matrix(Heatmap) to find the best correlation to the dataset
- Fill in categorical missing value by using mode and other factors.


## Feature Engineering
- Create 'Price Per Square Meter' by using Rental and Living Space
- Create 'Addition Cost' or cost of electricity, heating, water and other miscellaneous.

Example:
```Python
# Create new variables such as  `Price Per Square Meter`
df['Pricepm2'] = df['baseRent'] / df['livingSpace']
df['additioncost'] = df['totalRent'] - df['baseRent']

# Remove outliers from service charge cost more than 1,000 euro
df = df[(df['serviceCharge'] < 1000)]
```
```Python
# Empirical Rule
for cols in df.columns:
    if df[cols].dtype == 'int64' or df[cols].dtype == 'float64':
        upper_range = df[cols].mean() + 3 * df[cols].std()
        lower_range = df[cols].mean() - 3 * df[cols].std()
        
        indexs = df[(df[cols] > upper_range) | (df[cols] < lower_range)].index
        df = df.drop(indexs)
```

# 📷 EDA
To understand the model that we want to create the prediction model. We should analyze for better understanding and might clean to have a better dataset. I cannot illustrate all of the data in this overview. Instead, I will show some of the visualizations from the notebook files.

## Data Visualization
### Distribution
Distribution Plot of 'totalRent.'
![03distribution](https://github.com/northpr/GermanyRentalPrice/blob/main/model/data/markdown_image/distribution.png)


### Correlation with heatmap
Heatmap to check the correlation between variables
![04correlationmap](https://github.com/northpr/GermanyRentalPrice/blob/main/model/data/markdown_image/correlation.png)

### Scatter plot
Average rental per month by using city to seperate
![05cityratio](https://github.com/northpr/GermanyRentalPrice/blob/main/model/data/markdown_image/average_rental_per_month.gif)

### Geographical map
 [Source](https://www.kaggle.com/code/jonaslneri/german-rent-avg-by-postal-code)

Average rental per month by using Postleitzahl to seperate.
![06rentalsqm](https://github.com/northpr/GermanyRentalPrice/blob/main/model/data/markdown_image/germany_map.png)

Interactive plot to check each of the average rental price by using Postal Code.
![07rentalsqm](https://github.com/northpr/GermanyRentalPrice/blob/main/model/data/markdown_image/germany_average_map.gif)

We could do more virtualization to understand more in a specific city or room type depending on what purpose you're trying to use this work in, such as focusing in only Berlin.


# Summary
We could do a lot more such as specified in one city such as Berlin, or create other variables for the users to input. This work could develop more such as improving the interface or others.
