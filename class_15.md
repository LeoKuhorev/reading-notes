## Machine Learning Intro

### General:

_**ML**_ - the practice of teaching computers how to learn patterns from data, often for making decisions or predictions

ML Libraries:

- Scikit learn
- Tensor Flow

Supervised Learning: Collect training data -> Train Classifier -> Make Prediction

Terminology:

- _Model_ - a set of patterns learned from data;
- _Algorithm_ - a specific ML process used to train a model;
- _Training data_ - the dataset from which the algorithm learns the model;
- _Test data_ - a new dataset for reliably evaluating model performance;
- _Features_ - Variables (columns) in the dataset used to train the model;
- _Target variable_ - A specific variable you're trying to predict;
- _Observations_ - Data points (rows) in the dataset.

_**Supervised Learning**_ - includes tasks for "labeled" data (i.e. you have a target variable), used for prediction and classification;  
_**Unsupervised Learning**_- includes tasks for "unlabeled" data (i.e. you do not have a target variable), used for clustering.

### Exploratory analysis

Just review the dataset to answer simple questions like:

- Do the columns make sense?
- Do the values in those columns make sense?
- Are the values on the right scale?
- Is missing data going to be a big problem based on a quick eyeball test?

Then create a few plots to get an idea about:

- Distributions that are unexpected
- Potential outliers that don't make sense
- Features that should be binary (i.e. "wannabe - indicator variables")
- Boundaries that don't make sense
- Potential measurement errors

Study Correlations

- Positive correlation means that as one feature increases, the other increases. E.g. a child’s age and her height.
- Negative correlation means that as one feature increases, the other decreases. E.g. hours spent studying and number of parties attended.
- Correlations near -1 or 1 indicate a strong relationship.
- Those closer to 0 indicate a weak relationship.
  0 indicates no relationship.

In general, you should look out for:

- Which features are strongly correlated with the target variable?
- Are there interesting or unexpected strong correlations between other features?

### Data cleaning

- First we need to remove unwanted observations: this includes duplicate or irrelevant observations.
- Fix Structural Errors (something like typos or inconsistent capitalization)
- Filter Unwanted Outliers. In general, if you have a legitimate reason to remove an outlier, it will help your model’s performance. However, outliers are innocent until proven guilty. You should never remove an outlier just because it’s a "big number." That big number could be very informative for your model.
- Handle Missing Data. First, just to be clear, you cannot simply ignore missing values in your dataset. Two ways of solving this:

  - Dropping observations that have missing values
  - Imputing the missing values based on other observations

    - for categorical data just create a 'missing' class;
    - for numeric data:
      - Flag the observation with an indicator variable of missingness.
      - Fill the original missing value with 0 just to meet the technical requirement of no missing values.

### Feature engineering

Feature engineering is about creating new input features from your existing ones.

This is often one of the most valuable tasks a data scientist can do to improve model performance, for 3 big reasons:

- You can isolate and highlight key information, which helps your algorithms "focus" on what’s important.
- You can bring in your own domain expertise.
- Most importantly, once you understand the "vocabulary" of feature engineering, you can bring in other people’s domain expertise!

_Create Interaction Features:_  
Let's say we already had a feature called 'num_schools', i.e. the number of schools within 5 miles of a property.
Let's say we also had the feature 'median_school', i.e. the median quality score of those schools.
However, we might suspect that what's really important is having many school options, but only if they are good.
Well, to capture that interaction, we could simple create a new feature 'school_score' = 'num_schools' x 'median_school'

_Combine Sparse Classes:_  
As a rule of thumb, we recommend combining classes until each one has at least ~50 observations. As with any "rule" of thumb, use this as a guideline (not actually as a rule).

_Add Dummy Variables:_  
Dummy variables are a set of binary (0 or 1) variables that each represent a single class from a categorical feature.
The information you represent is exactly the same, but this numeric representation allows you to pass the technical requirements for algorithms.

_Remove Unused Features:_

- ID columns
- Features that wouldn't be available at the time of prediction
- Other text descriptions

After completing Data Cleaning and Feature Engineering, you'll have transformed your raw dataset into an analytical base table (_**ABT**_).

### Algorithm selection

Linear Regression is pretty far from being the best algorithm for ML because:

- It's prone to overfit with many input features.
- It cannot easily express non-linear relationships.

Regularized Regression Algos:

- Lasso Regression
- Ridge Regression
- Elastic-Net

**_Decision trees_** model data as a "tree" of hierarchical branches. They make branches until they reach "leaves" that represent predictions.

Flaw - individual _unconstrained_ decision trees are very prone to being overfit.​

_**Tree Ensembles**_ are machine learning methods for combining predictions from multiple separate models. There are a few different methods for ensembling, but the two most common are:

- Bagging (attempts to reduce the chance overfitting complex models) - _Random forests_
- Boosting (attempts to improve the predictive flexibility of simple models) - _Boosted trees_

### Model training

Split Dataset - set the data for training and testing the model. After splitting your data, don’t touch your test set until you’re ready to choose your final model! If the model performs very well on the training data but poorly on the test data, then it’s _**overfit**_.

_**Model parameters**_ can be learned directly from the training data while _**hyperparameters**_ cannot.

_**Model parameters**_ are learned attributes that define individual models (they can be learned directly from the training data):

- regression coefficients
- decision tree split locations

_**Hyperparameters**_ express "higher-level" structural settings for algorithms (They are decided before fitting the model because they can't be learned from the data):

- strength of the penalty used in regularized regression
- the number of trees to include in a random forest

_**Cross-validation**_ is a method for getting a reliable estimate of model performance using only your training data. The most common one, _**10-fold cross-validation**_, breaks your training data into 10 equal parts (a.k.a. folds), essentially creating 10 miniature train/test splits.
These are the steps for 10-fold cross-validation:

- Split your data into 10 equal parts, or "folds".
- Train your model on 9 folds (e.g. the first 9 folds).
- Evaluate it on the 1 remaining "hold-out" fold.
- Perform steps (2) and (3) 10 times, each time holding out a different fold.
- Average the performance across all 10 hold-out folds.

_**Fit and Tune Models**_ - Basically, all we need to do is perform the entire cross-validation loop detailed above on each set of _**hyperparameter**_ values.

    For each algorithm (i.e. regularized regression, random forest, etc.):
        For each set of hyperparameter values to try:
            Perform cross-validation using the training set.
            Calculate cross-validated score.

    For each algorithm:
        Keep the set of hyperparameter values with best cross-validated score.
        Re-train the algorithm on the entire training set (without cross-validation).

Performance Metrics:

- For regression tasks, we recommend _Mean Squared Error (MSE)_ or _Mean Absolute Error (MAE)_. (Lower values are better)
- For classification tasks, we recommend _Area Under ROC Curve (AUROC)_. (Higher values are better)

[Go back](./README.md)
