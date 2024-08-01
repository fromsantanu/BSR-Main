# Chapter: Measures of Variability (Range, Variance, Standard Deviation)

## Introduction

Measures of variability are statistical metrics that describe the spread or dispersion of a set of data. They provide insights into how much the data points differ from the average value. The three most common measures of variability are the range, variance, and standard deviation.

1. **Range**: The range is the difference between the maximum and minimum values in a dataset.
2. **Variance**: The variance measures the average squared deviation of each data point from the mean.
3. **Standard Deviation**: The standard deviation is the square root of the variance, providing a measure of spread in the same units as the data.

## Range

The range is the simplest measure of variability, calculated as the difference between the largest and smallest values in the dataset.

### Formula

The formula for the range is:
$$ \text{Range} = x_{\text{max}} - x_{\text{min}} $$

### Example in Python
```python
# Sample dataset
data = [10, 15, 20, 25, 30]

# Calculate range
range_value = max(data) - min(data)
print(f"The range is: {range_value}")

