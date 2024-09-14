# House Price Prediction

## Project Overview

This project aims to predict house prices using the California housing dataset. We apply various machine learning techniques to build predictive models, evaluate their performance, and identify the most important factors affecting house prices. The dataset includes features such as location, income, number of rooms, population, and proximity to the ocean.

The project is structured into several steps, including data cleaning, feature engineering, model training, evaluation, and final predictions.

## Dataset

The dataset used in this project is sourced from the California Census in the 1990s:

- Source: [California Housing Dataset](https://raw.githubusercontent.com/ageron/handson-ml2/master/datasets/housing/housing.csv)
- Number of rows: 20,640
- Number of features: 10 (including target variable)

### Key features:

- longitude, latitude: Geographical coordinates
- housing_median_age: Median age of houses in the block
- total_rooms, total_bedrooms, households: Housing characteristics
- population: Total population in the block
- median_income: Median income of households
- median_house_value: Target variable (house price)
- ocean_proximity: Categorical data representing proximity to the ocean

## Project Structure

### 1.	Data Preprocessing
- Handle missing values in the total_bedrooms column.
- Encode categorical variable (ocean_proximity) using one-hot encoding.
- Apply log transformation to the target variable (median_house_value) to address skewed distribution.
### 2.	Exploratory Data Analysis
- Perform correlation analysis to explore the relationships between features.
- Create visualizations such as correlation heatmaps to identify strong predictors of house prices.
### 3.	Model Training
The following models were trained and evaluated:
- Linear Regression
- Random Forest Regressor
- Gradient Boosting Regressor

The models were trained using the processed data, and their performance was evaluated based on metrics such as:
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- R-squared (R²)
### 4.	Model Evaluation
After testing various models, Random Forest Regressor yielded the best performance with the following metrics:
- MAE: 0.157
- MSE: 0.0538
- R²: 0.834

Feature importance analysis revealed that:
- Median income was the most important feature, with an importance score of 0.49.
- Proximity to inland areas (ocean_proximity_INLAND) was the second most important feature with a score of 0.14.
- Geographical coordinates (longitude, latitude) also played significant roles.

## How to Use

### Requirements

To replicate this project, ensure you have the following Python libraries installed:
```python
pip install numpy pandas scikit-learn matplotlib seaborn
```
#### Running the Code

1.	Data Preprocessing: Load the dataset, handle missing values, encode categorical variables, and apply log transformation on median_house_value.
2.	Model Training: Train Random Forest, Gradient Boost, and Linear Regression models using the processed data.
3.	Model Evaluation: Evaluate model performance using MAE, MSE, and R².
4.	Prediction: Use the best-performing model (Random Forest) for predictions on new data.

#### Example Usage
```python
# Load the dataset
df = pd.read_csv("https://raw.githubusercontent.com/ageron/handson-ml2/master/datasets/housing/housing.csv")

# Preprocessing
df['total_bedrooms'].fillna(df['total_bedrooms'].median(), inplace=True)
df = pd.get_dummies(df, columns=['ocean_proximity'], drop_first=True)
df['log_median_house_value'] = np.log(df['median_house_value'])
df.drop(columns=['median_house_value'], inplace=True)

# Split and train models
X = df.drop(columns=['log_median_house_value'])
y = df['log_median_house_value']

# Train Random Forest
from sklearn.ensemble import RandomForestRegressor
rf_model = RandomForestRegressor(random_state=42)
rf_model.fit(X, y)

# Evaluate the model
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
y_pred = rf_model.predict(X)
mae = mean_absolute_error(y, y_pred)
mse = mean_squared_error(y, y_pred)
r2 = r2_score(y, y_pred)

print(f"MAE: {mae}, MSE: {mse}, R²: {r2}")
```

### Visualizations

#### Correlation Heatmap

To visualize the correlation between features and house prices:
```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlation Heatmap of Features')
plt.show()
```

*A heatmap showing correlation between each columns*

#### Residual Plot

A residual plot can be used to assess the model’s accuracy:
```python
sns.residplot(x=y_pred, y=y - y_pred, lowess=True)
plt.xlabel('Predicted')
plt.ylabel('Residuals')
plt.title('Residual Plot')
plt.show()
```

*Use residual plot to see how well the model predictions align with the actual values (showing prediction errors) *

## Conclusion
The Random Forest Regressor performed the best with an MAE of 0.157 and R² of 0.834. The most important features for predicting house prices were:

- Median income
- Ocean proximity (Inland vs. Coastal)
- Geographical coordinates (longitude, latitude)

The log transformation and feature engineering steps improved model performance and allowed for a more accurate prediction of house prices.

## Future Work
- Implement further hyperparameter tuning of the Random Forest model.
- Test additional models such as XGBoost or CatBoost.
- Explore more detailed feature engineering to capture nuances in the dataset.

## Acknowledgements

This project utilizes the pandas, scikit-learn, seaborn, and matplotlib libraries. Special thanks to the data providers and the open-source community for their contributions.