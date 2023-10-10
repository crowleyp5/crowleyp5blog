---
layout: post
title:  "How to Optimize Hyperparameters"
author: Paul Crowley
description: "A basic tutorial for optimizing hyperparameters of machine learning models."
image: /assets/images/photo-1696946775093-96fcbd47213a.jpg
---
In the context of machine learning, hyperparameters are predefined input values for a model. They are not derived from the data. For example, the number of decision trees in a random forest and the learning rate of a regression model are hyperparameters. The values of these hyperparameters can significantly impact a model's predictive performance. Perhaps with some experience, we could essentially eyeball the context and make a fairly accurate guess as to what the optimal values would be for the hyperparameters in question. Alternatively, we can get a more precise estimate of the optimal hyperparameter if we test multiple candidate values and compare their performance.

My first exposure to this practice came from the house prices competition on Kaggle. I will use the data provided from this competition to demonstrate hyperparameter optimization techniques. Below is some code for preprocessing the data, although this is not the focus of this tutorial.

```python
import numpy as np
import pandas as pd

houses = pd.read_csv('train.csv')

# Load the data
train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')

# Store the test Ids because they need to be dropped before training but still needed for the submission file
test_ids = test['Id']

# Drop utilities and street because nearly all observations are the same value.
# Drop PoolQC because nearly all the data is missing.
train = train.drop(['Id', 'Utilities', 'Street', 'PoolQC'], axis = 1)
test = test.drop(['Id', 'Utilities', 'Street', 'PoolQC'], axis = 1)

# Drop SalePrice from training and set features equal to the columns.
# SalePrice already absent in test file to prevent cheating.
train_features = train.drop(['SalePrice'], axis=1)
test_features = test
features = pd.concat([train_features, test_features]).reset_index(drop=True)

# Select numeric columns by data type, then drop MSSubClass, MoSold, and YrSold.
numeric_cols = features.select_dtypes(exclude=['object']).columns
numeric_cols = numeric_cols.difference(['MSSubClass', 'MoSold', 'YrSold'])

# Assume that the missing values here are because the house does not have a garage, basement, etc. Replace them with 0.
for col in ('MasVnrArea', 'GarageYrBlt', 'GarageArea', 'GarageCars', 'MiscVal'):
    features[col] = features[col].fillna(0)

# Due to the skewness of the data, replace the rest of the missing numeric data with the median instead of the mean.
for col in numeric_cols:
    features[col].fillna(features[col].median(), inplace=True)

# Get target variable. Take the log transform to help satisfy regression assumptions
train["SalePrice"] = np.log1p(train["SalePrice"])
y = train['SalePrice'].reset_index(drop=True)

# We will likewise apply a log transform to the predictor variables
for col in numeric_cols:
    if not np.all(np.isfinite(features[col])):  # Check for non-finite values
        features[col] = np.log1p(features[col] - features[col].min() + 1)

# Select categorical columns by data type, then add MSSubClass, MoSold, and YrSold. These are categorical variables represented in the data as numbers.
categorical_cols = features.select_dtypes(include=['object']).columns
categorical_cols = categorical_cols.union(['MSSubClass', 'MoSold', 'YrSold'])

# These features are often missing if the house does not have a garage, basement, etc. We replace missing values with "None".
for col in ['GarageType', 'GarageFinish', 'GarageQual', 'GarageCond',
            'FireplaceQu', 'Alley', 'BsmtQual', 'BsmtCond', 'BsmtExposure',
            'BsmtFinType1', 'BsmtFinType2', 'Fence', 'MiscFeature',
            'MasVnrType']:
    features[col] = features[col].fillna('None')

# It does not make sense to replace the other missing values with "None", so we replace them with the mode.
for col in categorical_cols:
    features[col].fillna(features[col].mode()[0], inplace=True)

# Create dummy variables for categorical features
features = pd.get_dummies(features, columns=categorical_cols)
```

Now that we have the data ready to work with, we can initialize a model of our choice. One model I used in my
analysis was the Lasso regression model. This model helps with feature selection by setting the some of
the less influential variable coefficients to zero. We can control the threshold for the model to reduce a coefficient
to zero with the regularization parameter. If we set this hyperparameter to 0.01, then all coefficients with a value of
less than 0.01 will be reduced to zero. This may or may not be optimal because we could be setting some coefficients to
zero that actually contribute to the predictions, or we could be including some coefficients that do not improve the
predictions. Even with the context of the problem, it remains unclear what the optimal value should be.
However, we can define a range of candidate values and test the models accuracy with each of them. We then
perform cross validation to iteratively evaluate the models performance at each value as measured by the
mean squared error and use the best performing hyperparameter in our final model.

```python
from sklearn.linear_model import Lasso
from sklearn.model_selection import train_test_split, GridSearchCV

# Initialize a Lasso regression model
lasso = Lasso()

# Define a range of alpha values to search
alpha_values = [0.0001, 0.0005, 0.001, 0.005, 0.01]

# Create a parameter grid with alpha values, grids are useful if there is more
# than one hyperparameter we want to test, which is often the case.
param_grid = {'alpha': alpha_values}

# Perform grid search with cross-validation with 5 folds
grid_search = GridSearchCV(lasso, param_grid, cv=5, scoring='neg_mean_squared_error')

# Split data into train and validation sets for hyperparameter tuning
X_train, X_val, y_train, y_val = train_test_split(features[:len(y)], y, test_size=0.2, random_state=42)

# Fit the grid search to your data
grid_search.fit(X_train, y_train)

# Get the best alpha value from the grid search
best_alpha = grid_search.best_params_['alpha']
print(best_alpha)

# Initialize a Lasso regression model with the best alpha value
best_lasso = Lasso(alpha=best_alpha)
```

Running the code above will yield a best regularization parameter of 0.0005. I knew this
before writing this post, which is why I defined the range as I did. You will notice that
my range of values contained more than one value at different orders of magnitude. If we are
unsure about what order of magnitude is appropriate for the parameter, it would be wise to test
those orders of magnitude and then test a range of values from the optimal order of magnitude.
We can accomplish this easily with the Numpy logspace and linspace functions.

```python
# Redefine paramater grid for order of magnitude
param_grid = {'alpha': np.logspace(-4, -1, 4)}
print(param_grid)

# Perform grid search with cross-validation with 5 folds
grid_search = GridSearchCV(lasso, param_grid, cv=5, scoring='neg_mean_squared_error')

# Split data into train and validation sets for hyperparameter tuning
X_train, X_val, y_train, y_val = train_test_split(features[:len(y)], y, test_size=0.2, random_state=42)

# Fit the grid search to your data
grid_search.fit(X_train, y_train)

# Get the best alpha value from the grid search
best_alpha = grid_search.best_params_['alpha']
print(best_alpha)


# Redefine paramater grid for precise estimate
param_grid = {'alpha': np.linspace(0.0005, 0.005, 7)}
print(param_grid)

# Perform grid search with cross-validation with 5 folds
grid_search = GridSearchCV(lasso, param_grid, cv=5, scoring='neg_mean_squared_error')

# Split data into train and validation sets for hyperparameter tuning
X_train, X_val, y_train, y_val = train_test_split(features[:len(y)], y, test_size=0.2, random_state=42)

# Fit the grid search to your data
grid_search.fit(X_train, y_train)

# Get the best alpha value from the grid search
best_alpha = grid_search.best_params_['alpha']
print(best_alpha)
```

The output here is {'alpha': array([0.0001, 0.001 , 0.01  , 0.1   ])} with best_alpha equaling 0.001 for the logspace
interval and {'alpha': array([0.0005 , 0.00125, 0.002  , 0.00275, 0.0035 , 0.00425, 0.005  ])} with best_alpha equaling
0.0005 for the linspace interval. This is an effificient way to get the right result when our intuition does not
indicate what the value should approximately be.

If we are interested in other hyperparameters in addition to the regularization strength, we can simply
add the argument name with the values to test to the param_grid dictionary. It is also
important to note that more parameters will exponentially increase computing time. This
technique can quickly become computationally expensive if we test too many parameters and too
many values for each parameter. What is considered too much varies based on hardware, but we can
consider the time taken to train the model with one set of parameters and multiply that time by the
number of parameter combinations that are possible. I would encourage you to try this technique out with
this or any other data set. Pick a model and experiement with different parameters and grids. Print
the results frequently to see how minor adjustments affect the results. Doing so will help improve
your model accuracy.
