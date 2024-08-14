# Chapter: Logistic Regression

## Introduction

Logistic regression is a statistical method used for modeling the relationship between a dependent variable and one or more independent variables when the dependent variable is binary (i.e., it has only two possible outcomes). Unlike linear regression, which predicts a continuous outcome, logistic regression predicts the probability of an outcome that can take one of two values (e.g., 0 or 1, True or False).

## Key Concepts

1. **Dependent Variable (Y)**: The binary outcome variable, which can take values such as 0 or 1.
2. **Independent Variables (X1, X2, ..., Xn)**: The predictors or features that are used to predict the probability of the dependent variable being 1.
3. **Logistic Function (Sigmoid Function)**: The logistic function maps any real-valued number into the range (0, 1), which is interpreted as the probability:
   
   $\text{P}(Y=1|X) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_n X_n)}}$
   
   where:
   - $\beta_0$ is the intercept,
   - $\beta_1, \beta_2, \ldots, \beta_n$ are the coefficients associated with the independent variables.

4. **Log-Odds**: Logistic regression models the log-odds of the probability as a linear combination of the independent variables:
  
   $\log\left(\frac{\text{P}(Y=1|X)}{1 - \text{P}(Y=1|X)}\right) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_n X_n$


## Example in Python

Let's explore how to perform logistic regression using Python's `scikit-learn` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

# Sample data: hours studied, hours slept, and pass/fail outcome
np.random.seed(42)
data = pd.DataFrame({
    'Hours_Studied': np.random.rand(100) * 10,
    'Hours_Slept': np.random.rand(100) * 8 + 2
})
data['Pass'] = (2.5 * data['Hours_Studied'] + 1.5 * data['Hours_Slept'] + np.random.randn(100) * 2 > 25).astype(int)

# Independent variables (X) and dependent variable (Y)
X = data[['Hours_Studied', 'Hours_Slept']]
Y = data['Pass']

# Split the data into training and testing sets
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=42)

# Create a logistic regression model
model = LogisticRegression()

# Fit the model to the training data
model.fit(X_train, Y_train)

# Make predictions
Y_pred = model.predict(X_test)

# Evaluate the model
accuracy = accuracy_score(Y_test, Y_pred)
conf_matrix = confusion_matrix(Y_test, Y_pred)
class_report = classification_report(Y_test, Y_pred)

print(f"Accuracy: {accuracy:.2f}")
print("Confusion Matrix:")
print(conf_matrix)
print("Classification Report:")
print(class_report)
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied, hours slept, and a binary outcome (Pass/Fail). The outcome is based on a linear combination of hours studied and hours slept, with added noise.
- **Model Fitting**: We fit a logistic regression model using `LogisticRegression` from `scikit-learn`.
- **Model Evaluation**: We evaluate the model's performance using accuracy, confusion matrix, and classification report, which includes precision, recall, and F1-score.

## Example in R

Let's perform the same logistic regression analysis using R.

### R Code

```r
# Load necessary libraries
library(caret)

# Sample data: hours studied, hours slept, and pass/fail outcome
set.seed(42)
data <- data.frame(
  Hours_Studied = runif(100, min=0, max=10),
  Hours_Slept = runif(100, min=2, max=10)
)
data$Pass <- as.factor(ifelse(2.5 * data$Hours_Studied + 1.5 * data$Hours_Slept + rnorm(100, mean=0, sd=2) > 25, 1, 0))

# Split the data into training and testing sets
set.seed(42)
trainIndex <- createDataPartition(data$Pass, p = .8, 
                                  list = FALSE, 
                                  times = 1)
dataTrain <- data[ trainIndex,]
dataTest  <- data[-trainIndex,]

# Fit a logistic regression model
model <- glm(Pass ~ Hours_Studied + Hours_Slept, data = dataTrain, family = binomial)

# Make predictions on the test set
predictions <- predict(model, dataTest, type = "response")
predicted_classes <- ifelse(predictions > 0.5, 1, 0)

# Evaluate the model
conf_matrix <- confusionMatrix(as.factor(predicted_classes), dataTest$Pass)
print(conf_matrix)
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied, hours slept, and a binary outcome (Pass/Fail) using `runif()` and `rnorm()` functions.
- **Model Fitting**: We fit a logistic regression model using the `glm()` function with a binomial family, appropriate for binary outcomes.
- **Model Evaluation**: We use the `confusionMatrix()` function from the `caret` package to evaluate the model's performance, including accuracy, sensitivity, specificity, and other metrics.

## Interpreting the Results

### Model Parameters

- **Intercept (\(\beta_0\))**: The intercept represents the log-odds of the dependent variable being 1 when all independent variables are zero.
- **Coefficients (\(\beta_1, \beta_2\))**: The coefficients represent the change in the log-odds of the dependent variable being 1 for a one-unit change in the corresponding independent variable. A positive coefficient increases the log-odds, while a negative coefficient decreases it.

### Model Evaluation

- **Accuracy**: The proportion of correctly predicted outcomes (both 0 and 1) out of the total predictions.
- **Confusion Matrix**: A table that summarizes the performance of a classification model, showing the counts of true positives, true negatives, false positives, and false negatives.
- **Classification Report**: A summary of precision, recall, and F1-score for each class, providing a more detailed evaluation of the model's performance.

## Applications

Logistic regression is widely used in various fields:

- **Healthcare**: To predict the likelihood of a patient having a disease based on risk factors.
- **Marketing**: To assess the probability of a customer making a purchase based on demographic and behavioral data.
- **Finance**: To model the likelihood of loan default based on credit history and other factors.

## Conclusion

Logistic regression is a powerful and widely used tool for modeling binary outcomes. By understanding the model parameters, evaluating model performance, and interpreting the results, researchers and analysts can make informed predictions and decisions based on their data. Whether in healthcare, marketing, finance, or social sciences, logistic regression provides a robust framework for binary classification tasks.
