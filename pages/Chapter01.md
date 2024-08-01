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
print(f"The mean is: {mean}")

