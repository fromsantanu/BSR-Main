# Chapter: Percentiles and Quartiles

## Introduction

Percentiles and quartiles are statistical measures that divide a dataset into parts to provide insights into the distribution of the data. These measures are particularly useful for understanding the spread and concentration of values within a dataset.

1. **Percentiles**: Percentiles are values that divide a dataset into 100 equal parts. The nth percentile is the value below which n percent of the data falls.
2. **Quartiles**: Quartiles are specific percentiles that divide the data into four equal parts. The three main quartiles are:
   - **Q1 (First Quartile)**: The 25th percentile, below which 25% of the data falls.
   - **Q2 (Second Quartile or Median)**: The 50th percentile, below which 50% of the data falls.
   - **Q3 (Third Quartile)**: The 75th percentile, below which 75% of the data falls.

## Percentiles

Percentiles help to understand the relative standing of a value within a dataset. For example, if you score in the 90th percentile on a test, it means you scored better than 90% of the people who took the test.

### Example in Python

```python
# Import necessary library
import numpy as np

# Sample dataset
data = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

# Calculate 25th, 50th, and 75th percentiles
percentile_25 = np.percentile(data, 25)
percentile_50 = np.percentile(data, 50)
percentile_75 = np.percentile(data, 75)

print(f"25th Percentile: {percentile_25}")
print(f"50th Percentile (Median): {percentile_50}")
print(f"75th Percentile: {percentile_75}")
```

### Example in R

```r
# Sample dataset
data <- c(10, 20, 30, 40, 50, 60, 70, 80, 90, 100)

# Calculate 25th, 50th, and 75th percentiles
percentile_25 <- quantile(data, 0.25)
percentile_50 <- quantile(data, 0.50)
percentile_75 <- quantile(data, 0.75)

print(paste("25th Percentile:", percentile_25))
print(paste("50th Percentile (Median):", percentile_50))
print(paste("75th Percentile:", percentile_75))
```

## Quartiles

Quartiles divide the dataset into four equal parts. They provide a clearer understanding of the data spread by focusing on the quarters of the data distribution.

### Example in Python

```python
# Import necessary library
import numpy as np

# Sample dataset
data = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

# Calculate Q1, Q2 (Median), and Q3
Q1 = np.percentile(data, 25)
Q2 = np.percentile(data, 50)
Q3 = np.percentile(data, 75)

print(f"Q1 (25th Percentile): {Q1}")
print(f"Q2 (50th Percentile, Median): {Q2}")
print(f"Q3 (75th Percentile): {Q3}")
```

### Example in R

```r
# Sample dataset
data <- c(10, 20, 30, 40, 50, 60, 70, 80, 90, 100)

# Calculate Q1, Q2 (Median), and Q3
Q1 <- quantile(data, 0.25)
Q2 <- quantile(data, 0.50)
Q3 <- quantile(data, 0.75)

print(paste("Q1 (25th Percentile):", Q1))
print(paste("Q2 (50th Percentile, Median):", Q2))
print(paste("Q3 (75th Percentile):", Q3))
```

## Interquartile Range (IQR)

The Interquartile Range (IQR) is a measure of variability that describes the range within which the middle 50% of the data lies. It is calculated as the difference between the third quartile (Q3) and the first quartile (Q1).

### Formula

The formula for the IQR is:

$\text{IQR} = Q3 - Q1$

### Example in Python

```python
# Calculate IQR
IQR = Q3 - Q1
print(f"Interquartile Range (IQR): {IQR}")
```

### Example in R

```r
# Calculate IQR
IQR_value <- IQR(data)
print(paste("Interquartile Range (IQR):", IQR_value))
```

## Interpretation and Application

- **Percentiles**: Useful in identifying the relative standing of values within a dataset. For example, test scores are often reported in terms of percentiles to show how a student's performance compares to others.
- **Quartiles**: Help in understanding the spread and distribution of data. Quartiles are often used in box plots to visualize data distribution.
- **Interquartile Range (IQR)**: Provides a robust measure of spread by focusing on the middle 50% of the data, reducing the impact of outliers.

Percentiles and quartiles are valuable tools in data analysis, providing deeper insights into the distribution and variability of data. These measures are commonly used in various fields, including education, finance, and healthcare, to summarize and interpret data distributions effectively.
