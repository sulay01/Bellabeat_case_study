# Bellabeat_case_study 
Sulay Cay
05-Jan-2025

Bellabeat How can a wellness company play it smart?
Welcome to the Bellabeat Case Study repository! This project is part of the Google Data Analytics Professional Certificate program, showcasing data analysis and visualization skills using R programming. The focus is on analyzing smart device data to provide insights for Bellabeat, a high-tech manufacturer of health-focused products for women.

## Table of Contents
- [Introduction](#introduction)
- [Business Task](#business-task)
- [Dataset](#dataset)
- [Tools Used](#tools-used)
- [Analysis Steps](#analysis-steps)
  - [1. Data Cleaning](#1-data-cleaning)
  - [2. Data Analysis](#2-data-analysis)
  - [3. Data Visualization](#3-data-visualization)
- [Key Insights](#key-insights)
- [Conclusion](#conclusion)

---

## Introduction

Bellabeat is a health-focused technology company that designs smart devices to track activity, sleep, stress, and more. This case study analyzes data to uncover trends and provide actionable insights for Bellabeat's marketing and product development.

## Business Task

The main objective is to analyze user activity data from smart devices to identify patterns that can guide Bellabeat's business strategy.

## Dataset

The dataset used in this case study comes from public domain fitness tracker data. It contains information on daily activity, sleep patterns, and heart rates.

- **Source**: [Dataset on Kaggle or other source]
- **Files Used**: 
  - `dailyActivity.csv`
  - `sleepDay.csv`
  - `weightLogInfo.csv`

## Tools Used

- **Programming Language**: R
- **Libraries**: 
  - `tidyverse`
  - `ggplot2`
  - `lubridate`
  - `dplyr`

## Analysis Steps

### 1. Data Cleaning

```r
# Load libraries
library(tidyverse)
library(lubridate)

# Load data
activity_data <- read.csv("dailyActivity.csv")
sleep_data <- read.csv("sleepDay.csv")
weight_data <- read.csv("weightLogInfo.csv")

# Data cleaning
activity_data <- activity_data %>%
  select(-ActivityId) %>%
  mutate(ActivityDate = as.Date(ActivityDate, format="%m/%d/%Y"))

sleep_data <- sleep_data %>%
  mutate(SleepDay = as.Date(SleepDay, format="%m/%d/%Y"))

weight_data <- weight_data %>%
  filter(!is.na(WeightKg))

# Combine datasets
merged_data <- activity_data %>%
  left_join(sleep_data, by = c("Id" = "Id")) %>%
  left_join(weight_data, by = c("Id" = "Id"))
```

### 2. Data Analysis

```r
# Summary statistics
summary(merged_data)

# Correlation between steps and sleep
correlation <- cor(merged_data$TotalSteps, merged_data$TotalMinutesAsleep, use="complete.obs")
correlation
```

### 3. Data Visualization

#### Steps vs. Calories Burned
```r
library(ggplot2)

# Plot
ggplot(merged_data, aes(x=TotalSteps, y=Calories)) +
  geom_point(alpha=0.6, color="blue") +
  geom_smooth(method="lm", color="red") +
  labs(title="Steps vs. Calories Burned",
       x="Total Steps",
       y="Calories Burned")
```

#### Sleep Patterns
```r
# Sleep patterns by day of the week
merged_data$Day <- weekdays(merged_data$SleepDay)

ggplot(merged_data, aes(x=Day, y=TotalMinutesAsleep)) +
  geom_boxplot(fill="skyblue") +
  labs(title="Sleep Patterns by Day of the Week",
       x="Day of the Week",
       y="Total Minutes Asleep")
```

---

## Key Insights

1. **Correlation**: Positive correlation between daily steps and calories burned.
2. **Sleep Trends**: Users tend to sleep longer on weekends compared to weekdays.
3. **Activity Levels**: High activity levels correlate with higher calorie burn.

## Conclusion

Bellabeat can enhance user engagement by tailoring marketing campaigns based on user activity patterns and promoting features related to sleep tracking and activity monitoring.
