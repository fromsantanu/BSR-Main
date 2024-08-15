# Chapter: Life Tables

## Introduction

Life tables are a statistical tool used to summarize the mortality and survival patterns of a population over time. They are widely used in demography, actuarial science, public health, and epidemiology to estimate life expectancy, survival probabilities, and other vital statistics. Life tables provide a detailed account of the mortality experience of a population by age, gender, or other demographic factors.

## Key Concepts

1. **Life Table Components**:
   - **Age Interval ($x$ to $x+n$)**: The age range for which survival data is analyzed.
   - **Number of Survivors ($l_x$)**: The number of individuals surviving to the beginning of each age interval.
   - **Number of Deaths ($d_x$)**: The number of individuals who die during each age interval.
   - **Mortality Rate ($q_x$)**: The probability of dying within each age interval.
   - **Survival Probability ($p_x$)**: The probability of surviving through each age interval, calculated as $p_x = 1 - q_x$.
   - **Life Expectancy ($e_x$)**: The average number of years remaining for an individual at the beginning of each age interval.

2. **Types of Life Tables**:
   - **Complete Life Table**: Provides mortality and survival data for every single year of age.
   - **Abridged Life Table**: Groups ages into intervals (e.g., 5-year intervals) to provide a summary of mortality data.

3. **Applications**:
   - **Demography**: Estimating life expectancy and analyzing mortality trends in populations.
   - **Actuarial Science**: Calculating insurance premiums and pension liabilities based on mortality risks.
   - **Public Health**: Evaluating the impact of diseases or interventions on population survival.

## Example in Python

Let's explore how to create a simple life table using Python.

### Python Code

```python
# Import necessary libraries
import pandas as pd

# Sample data: mortality rates for a hypothetical population
age_intervals = [0, 1, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85]
mortality_rates = [0.005, 0.001, 0.002, 0.003, 0.004, 0.005, 0.006, 0.007, 0.008, 0.009,
                   0.010, 0.015, 0.020, 0.030, 0.040, 0.050, 0.060, 0.080, 0.100]

# Initialize life table DataFrame
life_table = pd.DataFrame({'Age': age_intervals, 'Mortality Rate (qx)': mortality_rates})

# Calculate survival probability (px)
life_table['Survival Probability (px)'] = 1 - life_table['Mortality Rate (qx)']

# Calculate number of survivors (lx), assuming starting population of 100,000
life_table['Number of Survivors (lx)'] = 100000 * life_table['Survival Probability (px)'].cumprod()

# Calculate number of deaths (dx)
life_table['Number of Deaths (dx)'] = life_table['Number of Survivors (lx)'].shift(1) - life_table['Number of Survivors (lx)']
life_table['Number of Deaths (dx)'].iloc[0] = 100000 - life_table['Number of Survivors (lx)'].iloc[0]

# Calculate life expectancy (ex) - simplified version
life_table['Life Expectancy (ex)'] = life_table['Number of Survivors (lx)'] / life_table['Number of Deaths (dx)']

# Display the life table
print(life_table)
```

### Explanation

- **Sample Data**: We use hypothetical mortality rates for different age intervals.
- **Life Table Calculation**: We calculate the survival probability ($p_x$), number of survivors ($l_x$), number of deaths ($d_x$), and life expectancy ($e_x$) for each age interval.
- **Output**: The life table is displayed, showing the calculated values for each age interval.

## Example in R

Let's perform the same analysis using R.

### R Code

```r
# Load necessary libraries
library(dplyr)

# Sample data: mortality rates for a hypothetical population
age_intervals <- c(0, 1, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85)
mortality_rates <- c(0.005, 0.001, 0.002, 0.003, 0.004, 0.005, 0.006, 0.007, 0.008, 0.009,
                     0.010, 0.015, 0.020, 0.030, 0.040, 0.050, 0.060, 0.080, 0.100)

# Initialize life table data frame
life_table <- data.frame(Age = age_intervals, qx = mortality_rates)

# Calculate survival probability (px)
life_table <- life_table %>%
  mutate(px = 1 - qx)

# Calculate number of survivors (lx), assuming starting population of 100,000
life_table <- life_table %>%
  mutate(lx = 100000 * cumprod(px))

# Calculate number of deaths (dx)
life_table <- life_table %>%
  mutate(dx = lag(lx) - lx) %>%
  mutate(dx = ifelse(is.na(dx), 100000 - lx, dx))

# Calculate life expectancy (ex) - simplified version
life_table <- life_table %>%
  mutate(ex = lx / dx)

# Display the life table
print(life_table)
```

### Explanation

- **Sample Data**: We use hypothetical mortality rates for different age intervals in R.
- **Life Table Calculation**: We calculate the survival probability ($p_x$), number of survivors ($l_x$), number of deaths ($d_x$), and life expectancy ($e_x$) for each age interval.
- **Output**: The life table is displayed, showing the calculated values for each age interval.

## Interpretation of Life Tables

### Key Metrics

- **Number of Survivors ($l_x$)**: Indicates how many individuals out of the original population are expected to survive to each age interval.
- **Number of Deaths ($d_x$)**: Reflects the expected number of deaths within each age interval.
- **Mortality Rate ($q_x$)**: Represents the probability of dying within each age interval.
- **Life Expectancy ($e_x$)**: Provides an estimate of the average number of years remaining for an individual at the start of each age interval.

### Applications of Life Tables

- **Public Health**: Life tables are used to assess population health, estimate life expectancy, and evaluate the impact of diseases or interventions on survival.
- **Actuarial Science**: Life tables are critical for calculating insurance premiums, pension liabilities, and other financial products that depend on mortality risk.
- **Demography**: Life tables are used to study population dynamics, including fertility, mortality, and migration patterns.

## Conclusion

Life tables are a fundamental tool in survival analysis, providing a detailed summary of the mortality and survival patterns of a population. By calculating key metrics such as the number of survivors, mortality rates, and life expectancy, life tables offer valuable insights into population health, demographic trends, and actuarial risks. Both Python and R provide powerful libraries and functions for constructing and analyzing life tables, making them accessible for researchers, actuaries, and public health professionals alike.
