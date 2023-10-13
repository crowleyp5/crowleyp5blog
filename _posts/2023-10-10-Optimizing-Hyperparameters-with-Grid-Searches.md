---
layout: post
title:  "Optimizing Hyperparameters with Grid Searches"
author: Paul Crowley
description: "A basic tutorial for optimizing hyperparameters of machine learning models."
image: /assets/images/photo-1696946775093-96fcbd47213a.jpg
---
### What are Hyperparameters?
In the context of machine learning, hyperparameters are predefined input values used in a model's calculations. They are not derived from the data. For example, the number of decision trees in a random forest and the learning rate to be used in a gradient descent algorithm are hyperparameters. Before we start training a model, we have to provide the necessary hyperparameters. The values of these hyperparameters can significantly impact a model's predictive performance, and while we may not know intuitively what the optimal number of decision trees are for a given random forest model, we can use a hyperparameter optimization technique called a grid search to find the best values that lead to the most accurate predictions.

### Choose a Model
We can assume that we already have a preprocessed data set that we would like to analyze with a machine learning model. We must first decide on a machine learning model. For this demonstration, I have selected a lasso regression model. You can learn more about lasso [here](https://en.wikipedia.org/wiki/Lasso_(statistics)). In short, this is a regression model that simultaneously performs feature selection based on a hyperparameter.
```python
from sklearn.linear_model import Lasso
from sklearn.model_selection import train_test_split, GridSearchCV

# Initialize a Lasso regression model
lasso = Lasso()
```

## Identify Hyperparameters of Interest
The hyperparameter that dictates feature selection is called the regularization strength. If the regularization strength is too large, then we may be excluding important predictor variables in our model. If it is too small, then we could be including variables with negligible predictive capacity that essentially complicate our model with noise. We will use hyperparameter optimization techniques to avoid both problems.

## Define a Grid Based on Order of Magnitude
A grid is essentially a dictionary of parameters. Our dictionary will be simple because we only have one hyperparameter of interest, but there could be more. Each parameter is associated with a range of hyperparameter values for which we want to compare the model's performance. How do we know which values to test? There could be a big difference bewteen a regularization strengths of 0.1 and 0.0001. Both could be reasonable depending on the problem, but there are orders of magnitude difference between them. Testing too many values can be computationally expensive, so we can first test orders of magnitude to narrow down our search. We can use Numpy's logspace function to generate this array of values by order of magnitude, and then we define the grid.
```python
# Define a range of regularization strength values to search
alpha_values = np.logspace(-4, -1, 4)

Create a parameter grid
param_grid = {'alpha': alpha_values}
```

## Perform Grid Search
Now that we have a parameter grid, we can iteratively test every possible combination of values for our hyperparameters. Since we only have one hyperparameter in our grid, the total number of combinations is just the range of regularization strength values we want to test (This is why grid searches can get computationally expensive when there are mutltiple parameters). The grid search relies on [cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)#:~:text=Cross%2Dvalidation%20is%20a%20resampling,model%20will%20perform%20in%20practice.) to compare the resulting mean squared error at each combination.
```python
# Perform grid search with cross-validation (cv=5 indicates 5 iterations per combination)
grid_search = GridSearchCV(lasso, param_grid, cv=5, scoring='neg_mean_squared_error')

# Split data into train and validation sets (see cross validation link)
X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2, random_state=42)

# Fit the grid search to data
grid_search.fit(X_train, y_train)
```

## Identify Best Hyperparameter Value
After the grid search is complete you can get the best performing value.
```python
# Get the best alpha value from the grid search
best_alpha = grid_search.best_params_['alpha']
print(best_alpha)
```

## Repeat at Same Order of Magnitude
However, we only tested to find the ideal order of magnitude. We need to repeat the process around that order of magnitude to find the most optimal value. we can use Numpy's linspace function to generate a range of values around the identified order of magnitude.
```python
# Define new range and grid
alpha_values = np.linspace(best_alpha-0.0005, best_alpha+0.0005, 7)
param_grid = {'alpha': alpha_values}

# Repeat grid search
grid_search = GridSearchCV(lasso, param_grid, cv=5, scoring='neg_mean_squared_error')
X_train, X_val, y_train, y_val = train_test_split(features[:len(y)], y, test_size=0.2, random_state=42)
grid_search.fit(X_train, y_train)
best_alpha = grid_search.best_params_['alpha']
```

## Create Optimized Model
With the grid search complete, we now have an optimized lasso regression model that will appropriately perform feature selection for us without excluding important predictor variables or allowing too much noise into the model.
```python
best_lasso = Lasso(alpha=best_alpha)
```

## Conclusion
Grid searches are a powerful tool to improve predictive performance of machine learning models. We can narrow down the optimal order of magnitude for the hyperparameters and then find their optimal values. It is also important to recognize the computational time limitations of grid searches that test too many combinations.
