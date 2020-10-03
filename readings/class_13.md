## LINEAR REGRESSIONS IN PYTHON

_**Linear regression**_ is a basic and commonly used type of predictive analysis. The overall idea of regression is to examine two things: (1) does a set of predictor variables do a good job in predicting an outcome (dependent) variable? (2) Which variables in particular are significant predictors of the outcome variable, and in what way do they–indicated by the magnitude and sign of the beta estimates–impact the outcome variable? These regression estimates are used to explain the relationship between one dependent variable and one or more independent variables. The simplest form of the regression equation with one dependent and one independent variable is defined by the formula y = c + b\*x, where y = estimated dependent variable score, c = constant, b = regression coefficient, and x = score on the independent variable.

### Necessary modules

    import numpy as np
    import pandas as pd
    import scipy.stats as stats
    import matplotlib.pyplot as plt
    from sklearn.linear_model import LinearRegression
    from sklearn.model_selection import train_test_split

### Steps

- convert data into pd DF;
- make sure columns have meaningful names;
- set `Y` and `X`:

  - `Y` - “target” data;
  - `X` - all the other features (or independent variables);

- bring data
- find independent var
- assign X (independent) (X = salary['YearsOfExperience'].values)
- find dependent var
- y = salary['Salary'].values
- reshape data if needed X.reshape(-1, 1) --> X = [[1],[2],[3]]
- remove the outliers to
  X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.8, test_size=0.2, random_state=100)
- plt.scatter(x_train, y_train, color='red')  
  plt.xlabel('bbb')  
  plt.ylabel('vvv')  
  plt.title('ggg')  
  plt.show()
- lm = LinearRegression()
  lm.fit(x_train, y_train)
  y_predict = lm.predict(x_test)

  - to check accuracy train - lm.score(x_train, y_train), test - lm.score(x_test, y_test)

- to add prediction to the plot:
  plt.scatter(x_train, y_train, color='red')
  plt.plot(x_test, y_predict)
  plt.xlabel('bbb')  
   plt.ylabel('vvv')  
   plt.title('ggg')  
   plt.show()

### Useful LR methods

- `lm.fit()` - fits a linear model;
- `lm.predict()` - predict Y using the linear model with estimated coefficients;
- `lm.score()` - returns the coefficient of determination (R^2). A measure of how well observed outcomes are replicated by the model, as the proportion of total variation of outcomes explained by the model;
- `.coef_` - gives the coefficients;
- `.intercept_` - gives the estimated intercepts;

[Go back](../README.md)
