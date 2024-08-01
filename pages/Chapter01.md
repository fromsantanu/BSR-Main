# Chapter: Measures of Central Tendency (Mean, Median, and Mode)

## Introduction

Measures of central tendency are statistical metrics used to summarize a set of data by identifying the center point or typical value of that dataset. The three most common measures of central tendency are the mean, median, and mode.

1. **Mean**: The mean, often referred to as the average, is the sum of all data points divided by the number of data points.
2. **Median**: The median is the middle value in a dataset when the numbers are arranged in ascending or descending order.
3. **Mode**: The mode is the value that appears most frequently in a dataset.

Each measure of central tendency provides different insights into the nature of the data distribution, and the choice of measure depends on the specific characteristics of the dataset.

## Mean

The mean is calculated by summing all the values in a dataset and then dividing by the number of values. It is sensitive to outliers, which can skew the mean significantly.

### Formula

\[ \text{Mean} = \frac{\sum_{i=1}^{n} x_i}{n} \]

where \( x_i \) represents each value in the dataset and \( n \) is the number of values.

### Example in Python
```python
# Import necessary library
import numpy as np

# Sample dataset
data = [10, 15, 20, 25, 30]

# Calculate mean
mean = np.mean(data)

### Example in R
```r
# Sample dataset
data <- c(10, 15, 20, 25, 30)

# Calculate mean
mean_value <- mean(data)
print(paste("The mean is:", mean_value))
```
## Median
The median is the middle value of a dataset when it is ordered. If the dataset has an even number of observations, the median is the average of the two middle numbers. The median is less sensitive to outliers compared to the mean.

### Example in Python
```python
# Import necessary library
import numpy as np

# Sample dataset
data = [10, 15, 20, 25, 30]

# Calculate median
median = np.median(data)
print(f"The median is: {median}")
```

### Example in R
```r
# Sample dataset
data <- c(10, 15, 20, 25, 30)

# Calculate median
median_value <- median(data)
print(paste("The median is:", median_value))
```

## Mode
The mode is the value that appears most frequently in a dataset. A dataset may have one mode, more than one mode, or no mode at all if all values are unique.

### Example in Python
```python
# Import necessary library
from scipy import stats

# Sample dataset
data = [10, 15, 20, 25, 25, 30]

# Calculate mode
mode = stats.mode(data)
print(f"The mode is: {mode.mode[0]}")
```

### Example in R
```r
# Function to calculate mode
calculate_mode <- function(x) {
  uniq_x <- unique(x)
  uniq_x[which.max(tabulate(match(x, uniq_x)))]
}

# Sample dataset
data <- c(10, 15, 20, 25, 25, 30)

# Calculate mode
mode_value <- calculate_mode(data)
print(paste("The mode is:", mode_value))
```

## Comparison and Application
**Mean**: Best used for data without outliers, providing a general average.
**Median**: Ideal for skewed distributions or data with outliers, representing the center point.
**Mode**: Useful for categorical data or identifying the most common value in a dataset.
Choosing the appropriate measure of central tendency depends on the nature of the data and the specific analysis objectives. Each measure provides unique insights, and using them in combination can offer a comprehensive understanding of the data distribution.


