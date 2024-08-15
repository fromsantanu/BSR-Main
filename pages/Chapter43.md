# Chapter: Discriminant Analysis

## Introduction

Discriminant Analysis is a statistical technique used to classify observations into predefined categories or groups based on predictor variables. It is commonly used when the dependent variable is categorical, and the goal is to understand the relationship between the predictor variables and the group membership. Discriminant Analysis can be used both for classification and dimensionality reduction, similar to PCA but with a focus on maximizing the separation between groups.

There are two main types of Discriminant Analysis:
1. **Linear Discriminant Analysis (LDA)**: Assumes that the predictors are normally distributed and that each class has the same covariance matrix. LDA is used when the groups are linearly separable.
2. **Quadratic Discriminant Analysis (QDA)**: Like LDA, but does not assume that the covariance matrices of each class are the same, allowing for more flexible classification boundaries.

## Key Concepts

1. **Class Separation**: Discriminant Analysis aims to find the linear (in LDA) or quadratic (in QDA) combination of predictors that best separate the different classes.

2. **Discriminant Functions**: These are the functions derived from the predictors that are used to classify observations into groups.

3. **Prior Probabilities**: The probability that an observation belongs to each class before observing the data. This can be set based on the class proportions in the data or assumed to be equal.

4. **Decision Boundary**: The boundary that separates different classes in the predictor space. In LDA, this boundary is a straight line (in 2D) or a plane (in higher dimensions), while in QDA, it can be curved.

5. **Applications**:
   - **Medical Diagnosis**: Classifying patients into disease categories based on medical tests.
   - **Finance**: Predicting the risk category of investments based on financial indicators.
   - **Marketing**: Segmenting customers into groups based on their purchasing behavior.

## Example in Python

Let's explore how to perform Linear Discriminant Analysis (LDA) using Python's `scikit-learn` library.

### Python Code: Linear Discriminant Analysis (LDA)

```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis as LDA
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix

# Load the Iris dataset
data = load_iris()
X = data.data
y = data.target

# Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Apply LDA
lda = LDA()
lda.fit(X_train, y_train)
y_pred = lda.predict(X_test)

# Calculate accuracy
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy:.2f}')

# Confusion matrix
conf_matrix = confusion_matrix(y_test, y_pred)
print(f'Confusion Matrix:\n{conf_matrix}')

# Plot the decision regions for the first two features
plt.figure(figsize=(8, 6))
colors = ['red', 'green', 'blue']
markers = ['o', 's', 'D']
for i, color, marker in zip(np.unique(y), colors, markers):
    plt.scatter(X_test[y_test == i, 0], X_test[y_test == i, 1], color=color, label=data.target_names[i], marker=marker)

plt.xlabel(data.feature_names[0])
plt.ylabel(data.feature_names[1])
plt.title('LDA Decision Regions')
plt.legend()
plt.show()
```

### Explanation

- **Dataset**: We use the Iris dataset to demonstrate LDA. This dataset contains measurements of different flower species.
- **LDA Application**: LDA is applied to the training data to find the linear combinations of features that best separate the classes.
- **Prediction**: The trained LDA model is used to predict the classes of the test data.
- **Accuracy and Confusion Matrix**: The accuracy of the model and the confusion matrix are computed to evaluate performance.
- **Visualization**: The decision regions for the first two features are plotted to visualize the classification boundaries.

### Python Code: Quadratic Discriminant Analysis (QDA)

```python
from sklearn.discriminant_analysis import QuadraticDiscriminantAnalysis as QDA

# Apply QDA
qda = QDA()
qda.fit(X_train, y_train)
y_pred_qda = qda.predict(X_test)

# Calculate accuracy
accuracy_qda = accuracy_score(y_test, y_pred_qda)
print(f'QDA Accuracy: {accuracy_qda:.2f}')

# Confusion matrix
conf_matrix_qda = confusion_matrix(y_test, y_pred_qda)
print(f'QDA Confusion Matrix:\n{conf_matrix_qda}')
```

### Explanation

- **QDA Application**: We use Quadratic Discriminant Analysis (QDA) to classify the data without assuming equal covariance matrices.
- **Accuracy and Confusion Matrix**: The performance of the QDA model is evaluated using accuracy and a confusion matrix.

## Example in R

Let's perform the same Discriminant Analysis using R.

### R Code: Linear Discriminant Analysis (LDA)

```r
# Load necessary libraries
library(MASS)
library(ggplot2)

# Load the Iris dataset
data(iris)
X <- iris[, 1:4]
y <- iris$Species

# Apply LDA
lda_model <- lda(Species ~ ., data=iris)

# Predict on the training data
lda_pred <- predict(lda_model, iris)

# Calculate accuracy
accuracy <- mean(lda_pred$class == y)
cat('Accuracy:', accuracy, '\n')

# Confusion matrix
conf_matrix <- table(lda_pred$class, y)
cat('Confusion Matrix:\n')
print(conf_matrix)

# Plot the decision regions
ggplot(iris, aes(x=Sepal.Length, y=Sepal.Width, color=Species)) +
  geom_point(size=3) +
  stat_ellipse(geom="polygon", alpha=0.2, aes(fill=Species)) +
  labs(title="LDA Decision Regions", x="Sepal Length", y="Sepal Width") +
  theme_minimal()
```

### Explanation

- **Dataset**: We use the Iris dataset in R to demonstrate LDA.
- **LDA Application**: LDA is applied to find the linear combinations of features that best separate the species.
- **Prediction**: The LDA model is used to predict the species and evaluate accuracy.
- **Confusion Matrix**: The confusion matrix is computed to evaluate model performance.
- **Visualization**: The decision regions are plotted using `ggplot2` to visualize the classification boundaries.

### R Code: Quadratic Discriminant Analysis (QDA)

```r
# Apply QDA
qda_model <- qda(Species ~ ., data=iris)

# Predict on the training data
qda_pred <- predict(qda_model, iris)

# Calculate accuracy
accuracy_qda <- mean(qda_pred$class == y)
cat('QDA Accuracy:', accuracy_qda, '\n')

# Confusion matrix
conf_matrix_qda <- table(qda_pred$class, y)
cat('QDA Confusion Matrix:\n')
print(conf_matrix_qda)
```

### Explanation

- **QDA Application**: We apply Quadratic Discriminant Analysis (QDA) to classify the species in the Iris dataset.
- **Accuracy and Confusion Matrix**: The performance of the QDA model is evaluated using accuracy and a confusion matrix.

## Interpretation of Discriminant Analysis

### Linear Discriminant Analysis (LDA)

- **Linear Boundaries**: LDA finds the linear combinations of features that maximize the separation between the classes. The decision boundaries are linear.
- **Assumptions**: LDA assumes that the classes have the same covariance matrices and that the features are normally distributed within each class.

### Quadratic Discriminant Analysis (QDA)

- **Quadratic Boundaries**: QDA allows for quadratic decision boundaries, making it more flexible than LDA.
- **Assumptions**: QDA does not assume that the covariance matrices of the classes are equal, allowing for more complex boundaries.

### Applications of Discriminant Analysis

- **Medical Diagnosis**: Classifying patients into different diagnostic categories based on test results.
- **Finance**: Predicting the creditworthiness of individuals based on financial metrics.
- **Marketing**: Segmenting customers into distinct groups based on purchasing behavior.

## Conclusion

Discriminant Analysis is a powerful tool for classification and dimensionality reduction, especially when the goal is to understand how predictor variables separate different classes. Both Linear Discriminant Analysis (LDA) and Quadratic Discriminant Analysis (QDA) offer valuable insights into the structure of the data, with LDA providing linear decision boundaries and QDA offering more flexibility with quadratic boundaries. Whether in medical diagnosis, finance, marketing, or other fields, Discriminant Analysis enables effective classification and interpretation of complex datasets. Both Python and R provide robust libraries for implementing these techniques, making them accessible for a wide range of applications.
