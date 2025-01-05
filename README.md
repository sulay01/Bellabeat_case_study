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

## README_2 Addtional Bellabeat CASE_STUDY 
By Sulay Cay 05-Jan-2025

# Bellabeat Case Study

This repository contains the analysis, visualizations, and recommendations for the Bellabeat smart device data case study. The purpose of this study is to uncover trends in user activity, calorie expenditure, and behavioral patterns, providing actionable insights to refine Bellabeat's marketing strategies and empower users to lead healthier lives.

---

## Objective

The primary goal of this case study is to analyze trends in smart device usage to inform Bellabeat's product development and marketing strategy.

Key Questions:

1. What are the trends in smart device usage?
2. How do these trends relate to Bellabeat’s customers?
3. How can Bellabeat use these trends to improve user engagement and refine its marketing strategies?

---

## Repository Structure

```
Bellabeat-Case-Study/
|-- README.md                   # Project overview and summary
|-- Bellabeat_Case_Study.Rmd    # Full analysis in R Markdown
|-- datasets/                   # Folder for datasets
|   |-- dailyActivity_merged.csv
|   |-- dailyCalories_merged.csv
|   |-- dailySteps_merged.csv
|   |-- dailyIntensities_merged.csv
|-- outputs/                    # Visualizations and charts
|   |-- steps_vs_calories.png
|   |-- sedentary_vs_active.png
|   |-- daily_trends.png
|-- presentation/               # PowerPoint presentation
|   |-- Bellabeat_Case_Study_Presentation.pptx
```

---

## Visualizations and Explanations

### Total Steps vs Calories Burned

This chart highlights the positive correlation between total steps taken and calories burned. Users who are more active consistently burn more calories.

![Steps vs Calories](outputs/steps_vs_calories.png)

**Explanation**:

- The graph shows a direct relationship between activity levels and calorie expenditure.
- Encouraging users to set daily step goals can promote increased activity and better calorie management.

---

### Sedentary Minutes vs Very Active Minutes

This visualization shows an inverse relationship between sedentary minutes and very active minutes, emphasizing the need for users to reduce sedentary time to improve overall health.

![Sedentary vs Active Minutes](outputs/sedentary_vs_active.png)

**Explanation**:

- Users with high sedentary minutes tend to have fewer very active minutes.
- Features like "move reminders" or gamification can encourage users to stay active throughout the day.

---

### Daily Trends in Activity

This line graph captures daily trends in total steps, calories burned, sedentary minutes, and very active minutes, providing insights into user behavior over time.

![Daily Trends in Activity](outputs/daily_trends.png)

**Explanation**:

- Peaks in very active minutes align with higher calorie burn.
- Sedentary behavior remains consistent, highlighting areas for improvement in user habits.
- Suggests opportunities for Bellabeat to engage users during low-activity periods.

---

## R Code for Analysis and Visualizations

```R
# Load necessary libraries
library(ggplot2)
library(dplyr)

# Load datasets
daily_activity <- read.csv("datasets/dailyActivity_merged.csv")
daily_calories <- read.csv("datasets/dailyCalories_merged.csv")
daily_steps <- read.csv("datasets/dailySteps_merged.csv")
daily_intensities <- read.csv("datasets/dailyIntensities_merged.csv")

# Merge datasets
merged_data <- daily_activity %>%
  inner_join(daily_calories, by = c("Id", "ActivityDay")) %>%
  inner_join(daily_steps, by = c("Id", "ActivityDay")) %>%
  inner_join(daily_intensities, by = c("Id", "ActivityDay"))

# Visualization 1: Steps vs Calories
steps_calories_plot <- ggplot(merged_data, aes(x = TotalSteps, y = Calories)) +
  geom_point(color = "blue") +
  labs(title = "Total Steps vs Calories Burned",
       x = "Total Steps",
       y = "Calories Burned") +
  theme_minimal()
ggsave("outputs/steps_vs_calories.png", steps_calories_plot)

# Visualization 2: Sedentary vs Active Minutes
sedentary_active_plot <- ggplot(merged_data, aes(x = SedentaryMinutes, y = VeryActiveMinutes)) +
  geom_point(color = "green") +
  labs(title = "Sedentary Minutes vs Very Active Minutes",
       x = "Sedentary Minutes",
       y = "Very Active Minutes") +
  theme_minimal()
ggsave("outputs/sedentary_vs_active.png", sedentary_active_plot)

# Visualization 3: Daily Trends
library(tidyr)
daily_trends <- merged_data %>%
  group_by(ActivityDay) %>%
  summarise(AvgSteps = mean(TotalSteps),
            AvgCalories = mean(Calories),
            AvgSedentary = mean(SedentaryMinutes),
            AvgVeryActive = mean(VeryActiveMinutes))
daily_trends_plot <- ggplot(daily_trends, aes(x = ActivityDay)) +
  geom_line(aes(y = AvgSteps, color = "Steps")) +
  geom_line(aes(y = AvgCalories, color = "Calories")) +
  geom_line(aes(y = AvgSedentary, color = "Sedentary Minutes")) +
  geom_line(aes(y = AvgVeryActive, color = "Very Active Minutes")) +
  labs(title = "Daily Trends in Activity",
       x = "Date",
       y = "Average Values") +
  theme_minimal()
ggsave("outputs/daily_trends.png", daily_trends_plot)
```

---

## Key Insights

1. **Steps and Calories Burned**:

   - Users who take more steps consistently burn more calories.
   - Encouraging daily step goals can promote better activity levels.

2. **Sedentary vs Active Minutes**:

   - High sedentary minutes correlate with reduced very active minutes.
   - Introducing "move reminders" and gamified challenges can help reduce sedentary behavior.

3. **Daily Trends**:

   - Peaks in active minutes align with higher calorie burn.
   - Sedentary behavior remains consistent, highlighting an opportunity for improvement.

---

## Recommendations

1. **Personalized Activity Goals**:

   - Set tailored daily step and calorie targets within the Bellabeat app to motivate users.

2. **Gamified Challenges**:

   - Implement engaging challenges and rewards to encourage activity and reduce sedentary time.

3. **Weekly Summaries**:

   - Provide weekly insights and progress reports to users, linking activity levels with health outcomes.

4. **Marketing Campaigns**:

   - Promote success stories and testimonials to engage users and showcase Bellabeat’s value.

---

## How to Run the Analysis

1. Clone this repository:

   ```bash
   git clone https://github.com/YourUsername/Bellabeat-Case-Study.git
   ```

2. Open the R Markdown file `Bellabeat_Case_Study.Rmd` in RStudio.

3. Ensure the necessary libraries are installed:

   ```R
   install.packages(c("ggplot2", "dplyr"))
   ```

4. Knit the `.Rmd` file to generate the full report.

---

## Conclusion

By leveraging data-driven insights, Bellabeat can enhance user engagement and refine its marketing strategies. Personalized activity goals, gamification, and integrated insights provide clear pathways for growth while empowering users to lead healthier lives.

Next Steps:

1. Implement these recommendations within Bellabeat’s app and marketing platforms.
2. Monitor and refine strategies based on user feedback and additional data analysis.

---

## PowerPoint Presentation

The PowerPoint presentation provides a visual summary of the Bellabeat case study findings and recommendations. It includes:

1. Overview of the analysis objectives.
2. Key insights and trends from the data.
3. Visualizations of steps vs. calories burned, sedentary vs. active minutes, and daily trends.
4. Recommendations for Bellabeat’s app and marketing strategies.

You can access the presentation [here](https://github.com/sulay01/Bellabeat_case_study/blob/main/Bellabeat_Case_Study_Presentation_.pptx).

