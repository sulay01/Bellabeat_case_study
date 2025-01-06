# Bellabeat-Case-Study-for-Data-Analysis-GOOGLE Data Analytics Professional -Cap Stone 

# Title Bellabeat-Case-Study-1 
Author Sulay Cay
Date 05-Jan-2025

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


## Tilte Bellabeat Case-Study 2
By Sulay Cay 
Date 05-Jan-2025


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

(https://github.com/sulay01/Bellabeat_case_study/blob/main/Total%20Steps%20vs%20Calories%20Burned.pdf)

**Explanation**:

- The graph shows a direct relationship between activity levels and calorie expenditure.
- Encouraging users to set daily step goals can promote increased activity and better calorie management.

---

### Sedentary Minutes vs Very Active Minutes

This visualization shows an inverse relationship between sedentary minutes and very active minutes, emphasizing the need for users to reduce sedentary time to improve overall health.

(https://github.com/sulay01/Bellabeat_case_study/blob/main/Sedentary%20Minutes%20vs%20Very%20Active%20Minutes%20(Filtered).pdf)

- Users with high sedentary minutes tend to have fewer very active minutes.
- Features like "move reminders" or gamification can encourage users to stay active throughout the day.

---

### Daily Trends in Activity

This line graph captures daily trends in total steps, calories burned, sedentary minutes, and very active minutes, providing insights into user behavior over time.

(https://github.com/sulay01/Bellabeat_case_study/blob/main/Daily%20Trends%20Steps%20and%20Calories%20.pdf)

**Explanation**:

- Peaks in very active minutes align with higher calorie burn.
- Sedentary behavior remains consistent, highlighting areas for improvement in user habits.
- Suggests opportunities for Bellabeat to engage users during low-activity periods.

---

## Updated R Code for Analysis and Visualizations

```R
# Load necessary libraries
library(ggplot2)
library(dplyr)
library(readr)

# Load datasets
daily_activity <- read_csv("datasets/dailyActivity_merged.csv")
daily_calories <- read_csv("datasets/dailyCalories_merged.csv")
daily_steps <- read_csv("datasets/dailySteps_merged.csv")
daily_intensities <- read_csv("datasets/dailyIntensities_merged.csv")

# Merge datasets
merged_data <- daily_activity %>%
  inner_join(daily_calories, by = c("Id", "ActivityDate")) %>%
  inner_join(daily_steps, by = c("Id", "ActivityDate")) %>%
  inner_join(daily_intensities, by = c("Id", "ActivityDate"))

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
  group_by(ActivityDate) %>%
  summarise(AvgSteps = mean(TotalSteps),
            AvgCalories = mean(Calories),
            AvgSedentary = mean(SedentaryMinutes),
            AvgVeryActive = mean(VeryActiveMinutes))
daily_trends_plot <- ggplot(daily_trends, aes(x = ActivityDate)) +
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
   git clone [https://github.com/sulay01/Bellabeat_case_study]
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

# You can access both presentations and make sure to click view raw 

1: [here](https://github.com/sulay01/Bellabeat_case_study/blob/main/Bellabeat_Case_Study_Presentation_.pptx).

2: [here](https://github.com/sulay01/Bellabeat_case_study/blob/main/Bellabeat_Case_Study_Complete_Presentation%20(Orange)(1).pptx).



## Title Bellabeat Case-Study-3

## Reference

1 <a href="#ask" id="toc-ask">Ask</a>

2 <a href="#prepare" id="toc-ask">Prepare</a>

3 <a href="#process" id="toc-ask">Process</a>

4 <a href="#analyze" id="toc-ask">Analyze</a>

5 <a href="#share" id="toc-ask">Share</a>

6 <a href="#act" id="toc-ask">Act</a>


## Scenario
Bellabeat is a high-tech manufacturer of health-focused products for women it believes that analyzing smart device fitness data could help unlock new growth opportunities for the company.
I have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices, then using these insights it will help guide the marketnig strategy for the company.

# Ask
Business Task: Analyzing the smart device usage data by Fitbit and get valuable insights then making recommendations based on these trend to help guide the marketing strategy.

#### Key Stakeholders

##### Primary
Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer.

Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team.

##### Secondary
Bellabeat marketing analytics team.

# Prepare
This Kaggle data set contains personal fitness tracker from thirty fitbit users https://www.kaggle.com/datasets/arashnic/fitbit by Mobius.

Thirty eligible Fitbit users consented to the submission of personal tracker data.
It contains 18 CSV files that iclude daily activity, daily steps, daily calories, daily intensities, hourly steps, hourly intensities, hourly calories, heartrat seconds, minute calories narrow and wide, minute intensities narrow and wide, minute steps narrow and wide, sleep day, and weight log info.

The data is stored in csv files, the data contains files that have data long and wide format but most of the csv files are long formated.
I measured the data and its credibility and it is not reliable as it only contains data about 30 fitbit users, which is not enough to make reliable insights.
the originality of the data is derived from 30 legit fitbit users who participated in a survey via Amazon Mechanical Turk between 3/12/2016 and 5/12/2016.
The data is biased and not comprehensive as the sample size is small and should have been bigger to make better predictions and eliminate the bias in the data, and the data also is outdated as it was collected in 2016 and it should contain data from march to may of 2016 but it only shows data for 31 one day from april to may so it has some missing data.

The data is not cited or lincenced.

# Process
What tools did i choose and why?

I cleaned the data using Excel and SQL because its easy to manipulate the data there and clean it because it is stored as csv files. 
I also did some cleaning in R that will be documented as well.

### Documantation of data cleaning in Excel :
---------------------------------------------
- I started by changing the data format for each file because the date was formated wrong as it was general and it was writen in a format dd/mm/yyyy which made the date to be for december and janury rather than being for april and may, i changed the format by using text to colmns and turned all the dates in the files to date in the correct format mm/dd/yyy.
- I sorted the data by date from oldest to newest.
- Then i checked for duplicated in each file ( Dailysteps had only 1 duplicate/ hourly calories had 987 duplicates/ hourly intensities had 1108 duplicated/ hourly steps had 1075 duplicates/ sleep day had 3 duplicates/ minute sleep had 629 duplicates ) and i removed them from the sheets.
- In the sleep day sheet i added a column named (hoursofsleep) by deviding the total minutes asleep by 60 to know how many ours each user sleeps.

### Documantation of data cleaned in SQL :
---------------------------------------------
- Then i used SQL to clean the data more and join some tables, i joined tables to see if there is any data that is not needed so i joined daily_activity with daily_steps and daily_intensitites and daily_clories. daily_activity had the same data that was in the other 3 tables so i dropped the other 3 tables (daily_steps - daily_calories - daily_intensities) because they wont be needed any more as daily_activity contains all of them combined.
- I used Count function in SQL to identify the distinct users in each table.
- The daily_activity, hourly_steps, hourly_calories and hourly_intensities tables showed {33} distinct users and sleep_day showed {24} distinct users , weight_loginfo showed only {8} distinct users.

### Documantation of data cleaned in RStudio
---------------------------------------------
- I start by incpecting the data and checking if there is anything that needs any adjustments.
```{r}
str(daily_activity)
glimpse(daily_activity)
colnames(daily_activity)
sapply(daily_activity, class)
```
- Change Data Type to Date in Dataframes

to change the data type of `ActivityDay` from `Chr` to `Date` i had to make a new column for the date because when i changed the date type the date gets `N/A` values so i had to add a new column with the right data type.
```{r}
daily_activity$new_date <- dmy(daily_activity$ActivityDay)
hourly_calories$new_date <- dmy(hourly_calories$ActivityDay)
hourly_intensities$new_date <- dmy(hourly_intensities$ActivityDay)
hourly_steps$new_date <- dmy(hourly_steps$ActivityDay)
minute_sleep$new_date <- dmy(minute_sleep$date)
sleep_day$new_date <- dmy(sleep_day$SleepDay)
weight_loginfo$new_date <- dmy(weight_loginfo$Date)
```
- Adding Column for Month

using the `month()` function to add column for month to be used in the analysis 

```{r}
daily_activity$month <- month(daily_activity$new_date)
hourly_calories$month <- month(hourly_calories$new_date)
hourly_intensities$month <- month(hourly_intensities$new_date)
hourly_steps$month <- month(hourly_steps$new_date)
minute_sleep$month <- month(minute_sleep$new_date)
sleep_day$month <- month(sleep_day$new_date)
weight_loginfo$month <- month(weight_loginfo$new_date)
```
- Add Column for Weekdays
Adding weekdays column to study the different habits of users during the week and see if there are any patterns. 

```{r}
daily_activity$week_days <- weekdays(daily_activity$new_date)
sleep_day$week_days <- weekdays(sleep_day$new_date)
```

- Changing Column Names to Lowercase

changing column names to lowercase letters using `rename_with`.

```{r}
daily_activity_new <- daily_activity %>%
  rename_with(tolower)
hourly_calories_new <- hourly_calories %>%
  rename_with(tolower)
hourly_intensities_new <- hourly_intensities %>%
  rename_with(tolower)
hourly_steps_new <- hourly_steps %>%
  rename_with(tolower)
minute_sleep_new <- minute_sleep %>%
  rename_with(tolower)
sleep_day_new <- sleep_day %>%
  rename_with(tolower)
weight_loginfo_new <- weight_loginfo %>%
  rename_with(tolower)
```
-Renaming Columns
renaming the table `activitydate` to `date` in all data frames that needs to be adjusted
```{r}
names(daily_activity_new)[names(daily_activity_new)== "activityday"] <- "date"
names(hourly_calories_new)[names(hourly_calories_new)== "activityday"] <- "date"
names(hourly_intensities_new)[names(hourly_intensities_new)== "activityday"] <- "date"
names(hourly_steps_new)[names(hourly_steps_new)== "activityday"] <- "date"
```
- Checking Updates
```{r}
names(daily_activity_new)
names(hourly_calories_new)
names(hourly_intensities_new)
names(hourly_steps_new)
```
- Delete N/A values 

I deleted column dateday in `daily_activity_new` and i also deleted the columns in `sleep_day_new` data frame that had no values in them and as well all the `N/A` values in other data frames.

```{r}
daily_activity_new <- subset(daily_activity_new, select = -dateday)
sleep_day_new <- subset(sleep_day_new, select = -...8)
sleep_day_new <- subset(sleep_day_new, select = -...9)
sleep_day_new <- na.omit(sleep_day_new)
weight_loginfo_new <- na.omit(weight_loginfo_new)
hourly_steps_new <- na.omit(hourly_steps_new)
hourly_intensities_new <- na.omit(hourly_intensities_new)
minute_sleep_new <- na.omit((minute_sleep_new))
```
After deleting the N/A values from the `weight_loginfo_new` there are only two users that are left with complete data so this data frame will not be used because it is unreliable.

- Drop Dataframes

now that i have the new updated and cleaned data frames i will delete the original once because they are not needed for the analysis, and i also deleted `weight_loginfo_new` and `minute_sleep_new` because they are not usefule in the analysis.
```{r}
rm(daily_activity)
rm(hourly_calories)
rm(hourly_intensities)
rm(hourly_steps)
rm(minute_sleep)
rm(sleep_day)
rm(weight_loginfo)
rm(weight_loginfo_new)
rm(minute_sleep_new)
```
# Analyze
First i start the analyzing by doing summary on all the data frames that i have using the `summary()` function to know the `min`, `max`, `median`, and `mean` of the data to get some valuble insights.

### Daily Activity
The average steps for users are 7638 step per day in an average distance of 5490 km.
The average very active distance is 1.5km in an average time of 21.16 minutes.
The max very active distance is 21.9 km in a max time of 3.5 hours.
The average moderately active distance is 0.5675 k, in an average time of 13.9 minutes.
The average sedentary active distance is 0.001606 and the average sedentary active distance is 17.6 hours or 1058 minutes.
The max sedentary distance is 0.110000 and the max sedentary minutes is 24 hours or 1440 minutes.
```{r}
 summary(daily_activity_new)
```
![Screenshot (129)](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/b5af4881-e1f9-48b3-a406-f230116e365a)
### Hourly Calories
Hourly minimum calories is 42 and the average calories per hour is 83, the max calories is 948 calories
```{r}
summary(hourly_calories_new)
```
![Screenshot (130)](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/e5c21c5b-467a-45d7-b92c-7fbe5f875729)
### Sleep Day
The minimum sleep records is 1 record and the max sleep record is 3 and the average is 1.12.
The min time asleep is 1 hour and the average time asleep is about 7 hours and the max time asleep is  13.3 hours.
```{r}
summary(sleep_day_new)
```
![Screenshot (131)](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/370e84f6-d35b-4502-acc0-ec50a9482d36)

### Hourly Steps
The average hourly steps is 333.5 step per hour.
The max recorded step is 10554.
```{r}
summary(hourly_steps_new)
```
![Screenshot (133)](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/240c1afc-b32b-4982-913d-a01e768f0a0e)

### Hourly Intensities
The average hourly intensities is 12.64.
The max hourly intensities is 180.
```{r}
summary(hourly_intensities_new)
```
![Screenshot (134)](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/d1f8f89b-0e10-4a0a-b1ae-16a44ffde34c)

# Share

### Daily Activity

##### Most Total Steps in Week Days

The next visualization shows what weekdays have the highest total steps to see when the users walked the, and as it shows using the `geom_smooth()` we can see that during  Sunday and Saturday had the highest total steps of all week days.
```{r}
ggplot(data = daily_activity_new, mapping = aes(x = totalsteps, y = week_days)) +
  geom_smooth(aes(color = week_days)) +
  labs(title = " Highest Total Steps in Weekdays") +
  labs(x = "Total Steps", y = "Week Days")
```
![Highest Total Steps in Weekdays](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/192b24e3-7be4-4676-9d9b-5a8562d71b28)

And this visualization shows week days with the most total steps, as you can see that Tuesday and Wednesday have the most total steps of the week days
i used the sum function to know which day has the most overall steps.
```{r}
ggplot(daily_activity_new, aes(x = week_days, y = sum(totalsteps), fill = week_days)) +
         geom_bar(stat = "identity") +
         labs(title = "Total Steps in Weekdays") +
         labs(x = "Week Days", y = "Total Steps")
```
![Total Steps in Weekdays](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/ef9b560a-fe5f-4fb7-96d0-b94fbcc17c90)

#### TotalSteps VS Calories

This visualization show the `TotalSteps vs Calories`as you can see that there is a positive  correlation between the total steps and the calories burned, as the steps increase the calorie burning increases, at the same time people could be in the same step range like others but burn more calories.
```{r}
ggplot(data = daily_activity_new, mapping = aes(x = totalsteps, y = calories, color = new_date)) +
  geom_point() + geom_smooth(aes(y = calories), color = "red") +
  labs(title = "Totalsteps vs Calories") +
  labs(x = "Total Steps", y = "Calories") +
  annotate("text", x = 32000, y = 2500, label = "Highst Total Steps") +
  annotate("text", x = 20000, y = 4700, label = "Highst Total Calories")
```
![TotalSteps VS Calories](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/fafc025a-4aef-4cb9-9b68-0739cef00464)

### Activiy Minutes vs Calories
These visualizations compare different types of activity minutes to the burned calories.
#### Lightly Active Minutes
The visualization shows how the lightly active minutes done by users affects the calories burned, you can see that when the minutes increase the calories being burned also increase.
But also it shows that some cases have more lightly activity minutes but at the same time they burn the same amount of calories as the users who did fewer minutes.

```{r } 
ggplot(data = daily_activity_new, mapping = aes(x = calories, y = lightlyactiveminutes, color = new_date)) +
  geom_point() +
  geom_smooth(aes(y = lightlyactiveminutes), color = "green") +
  labs(title = "Lightly Active Minutes vs Calories") +
  labs(x ="Calories", y = "LightlyActiveMinutes")
```
![Lightly Active Minutes](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/ac7f3b32-2001-4b0e-86f3-d0f0441ec938)
#### Very Active Minutes
This visualization compares the `Very Active Minutes` show that when the activity minutes increase the burned calories also increase indicating that there is a positive correlation between very active minutes and calories burned, but at the same time people with 0 minutes that are very active also burn calories a lot.
```{r}
ggplot(data = daily_activity_new, mapping = aes(x = calories, y = veryactiveminutes, color = new_date)) +
  geom_point() +
  geom_smooth(aes(y = veryactiveminutes), color = "yellow") +
  labs(title = "Very Active Minutes vs Calories") +
  labs(x = "Calories", y = "VeryActiveMinutes")
```
![Very Active Minutes](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/37304dd3-42e1-419d-9a11-95ced82b8a2e)
#### Fairly Active Minutes
There is also a positive correlation between fairly active minutes and calories burned, as the minutes increase the calories burned also increase.
```{R}
ggplot(data =daily_activity_new , mapping = aes(x = calories, y = fairlyactiveminutes, color = new_date)) +
  geom_point() +
  geom_smooth(aes(y = fairlyactiveminutes), color = "orange") +
  labs(title = "Fairly Active Minutes vs Calories") +
  labs(x = "Calories", y = "FairlyActiveMinutes")
```
![Fairly Active Minutes](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/24f17d98-f4bb-45dc-ae45-748e921a2bcd)
#### Sedentary Minutes
The visualizations indicates that people who spend little time in sedentary activity burn calories but it as well shows that people with higher sedentary minutes also burn the same amount of calories, so there is no correlation between sedentary minutes and burning calories. 
This could mean that the sedentary minutes in some cases affect the calories burned or doesn't affect it, it's hard to make that decision based on this information so i would not rely on it.
```{r}
ggplot(data = daily_activity_new, mapping = aes(x = calories, y = sedentaryminutes, color = new_date)) +
  geom_point() +
  geom_smooth(aes(y = sedentaryminutes), color = "red")+
  labs(title = "Sedentary Minutes vs Calories") +
  labs(x ="Calories", y = "SedentaryMinutes")
```
![Sedentary Minutes](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/3e21d788-db1e-48e4-8360-981ce4b4749f)

## Sleep Day
Merging two data frames together `sleep_day_new` and `daily_activity_new` to see if the sleeping hours affect the burning fo calories or not.
First merging the data using merge() and creating a new data frame called `sleep_X_activity`.
```{r}
sleep_X_activity <- merge(sleep_day_new, daily_activity_new, by = c('id', 'new_date'))
```
#### Sleeping Hours vs Calories
This visualization show that the sleeping hours has no impact on the calories burned as there is no clear pattern, it changes randomly so its not a direct factor.
```{r}
ggplot(data = sleep_X_activity, mapping = aes(x = hoursofsleep, y = calories, color = calorie))+
  geom_smooth(color = "red") +
  labs(title = "Hours of Sleep vs Calories") +
  labs(x = "HoursOfSleep", y = "Calories")
```
![Sleeping Hours vs Calories](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/555f7485-005a-4d45-ba8b-095a03fd8a67)


#### Total Minutes Asleep in Week Days
The visualization shows that Wednesday's are the most days in the week that users have the highest total minutes asleep in.
```{r}
ggplot(data = sleep_day_new, mapping = aes(x = week_days, y = totalminutesasleep, fill = week_days)) +
  geom_bar(stat = "identity") +
  labs(title = "Total Minutes Asleep in Week Days") +
  labs(x = "Week Days", y = "Minutes Asleep")
```
![Total Minutes Asleep in Week Days](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/d3ee6608-e2ad-48a2-b59e-b34145184d6a)

## Hourly Steps

#### Activity Hour With the Most Steps
With this visualization you can see what activity hour of the day the users do the most steps in, as you can see using the `geom_col()` the visualization shows that users do the most steps between 12pm and 7pm users do the most steps, and the lowest is between 12am and 4am.
```{r}
ggplot(data = hourly_steps_new, mapping = aes(x = activityhour, y = steptotal, fill = activityhour)) +
  geom_bar(stat = "identity")+
  labs(title = " Most Steps During The Day") +
  labs(x = "Activity Hour", y = "Step Total")
```
![Activity Hour With the Most Steps](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/a69ebbe3-855f-4831-853d-2f0a6d7b4f74)

## Hourly Calories
This visualization shows the hourly calories burned and as we can see that the most calories burned is between 4pm and 8pm and then gradualy goes down.
The lowest calorie burning is between 12am and 4am.
```{r}
ggplot(data = hourly_calories_new, mapping = aes(x = activityhour, y = calories, color = calories)) +
  geom_smooth(color = "red") +
  labs(title = "Hourly Calories Burned") +
  labs(x = "Activity Hour", y ="Calories")
```
![Hourly Calories](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/fdef219a-e165-48d6-8684-f80baf8c219d)
## Hourly Intensities
The intensities match the hourly burning calories as the highest intensities the user have during the day are between 12pm and 7pm and then starts to go down after that.
The lowest intensity is between 12am and 4am.
```{r}
ggplot(data = hourly_intensities_new, mapping = aes(x = activityhour, y = totalintensity, fill = activityhour))+
  geom_bar(stat = "identity") +
  labs(title = "Hourly Intensities") +
  labs(x = "Activity Hour", y = "Total Intensity")
```
![Hourly Intensities](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/482a4b5f-77c8-4991-a78b-9502fb2d3db2)

Now we will merge two data frames together to get insight about the calories burned and the intensities.
```{r}
calories_x_intensity <- merge(hourly_calories_new, hourly_intensities_new, by = c('id', 'new_date'))
```
As you can see when the total intensity goes higher the burned calories increas so there is a positive correlation between the two factors.
```{r}
ggplot(data = calories_x_intensity, mapping = aes(x = calories, y = totalintensity)) +
  geom_smooth()+
  labs(title = "Total Intensity vs Calories")+
  labs(x = "Calories", y= "Total Intensity")
```
![Calories vs Intensities](https://github.com/Karemelshimi/Bellabeat-Case-Study-for-Data-Analysis/assets/153403784/3147a8b5-5d40-4111-8110-591f83b64551)

# Act

After analyzing the data as you can see that fitbit can know their users habits and how active they are, how their day usualy looks like and how it organized by their activity as in light, fair, very, or just in sedentary. Knowing how the consumer sleeps and their habits and when they go to sleep , how much time do they take to actualy go to sleep all of this information can help them understand their user's. fitbit having this data can use it to actualy connect with their users and know them better and even help them in their daily life. Bellabeat should use the same information gathering methods, if bellabeat had access to same data for the users that they have they would help women by inetracting with them, telling them what they are lacking and what is best for them to improve their health and general life style, as well as connecting with them and creating strong customer bond and a great realtionship by making women trust them when they see a significant change in their life based on the recommendations that bellabeat can make for each one of them according to the user's statistics.

### Statistical summary of the analysis show these device usage trends :
- The highest total steps were on sunday's and saturday's.
- The most total steps of the week days were on tuesday's and wednesday's.
- The users spend 3 hours of their day in lightly activity which made them burn calories adn stay healthy.
- The users spend at least 20 minutes doing very active activity.
- The users spend an average of 13 min daily on fairly activity.
- On the average the users spend 16.5 hours in sedentary avtivity which is 68.7% of the day.
- users sleep on average 7 hours and they spend around 30 minutes in bed before they sleep and they sleep more hours on wednesday's.
- users are most active between 12pm and 7pm as they do the most steps that time.
- users tend to burn the most calories from 12pm and 7pm and the lowest calories they burn is between 12am and 4am, they match their calorie burning with their intensity hours, the highest intensity of their day is between 12pm and 7pm and the lowest intensity is between 12am and 4am.

### Recommendations

By using the wellnees tracker bellabeat can gather data to know their user's behavior like fitbit and using this information they can inform their users after watching their habit for a month with what they should adjust to make their life better and healthier For Example:

- Knowing their bad days of sleep and finding a pattern like for example they sleep less on monday's because they tend to stay up more and they go to bed late so they sleep less hours than the rest of the week, so bellabeat can find this pattern when gathering the data and build a health check summary every week for their users with the most impartant changes and stuff that affect their welnees to notify them about these changes and it can be used for alot of other stuff to notify them about not just the sleeping hours.
- They can inform their users if they are sitting long time by checking the step counter if it havent moved for specific amount of time and giving them notification on the app so they would know that they should be more active and get up.
- Letting them know that the day is almost ending if they haven't done their average steps for the day.
- showing the user's their intensity counter and setting a goal for them to achive it daily.
- Doing competitions on the app for example for hitting a max intensity or max steps and giving them a specific gift or just making it to creat a motivational environment for them to achieve what they need. Credits to findings to help with this case study as well goes to Karemel Shimi. Thank you hope you enjoyed these 3 case Studies and hope it adds value to Bellabeats ! 



### Not only did I like Karemels findings and case study but,  I also liked many others, one being xgabrielex provided their findings and analhysis below- I truly see that many has giving their all to complete this study here is another case study for Bellabeat that I am sharing below:


# Bellabeat-Data-Analysis-Case-Study-4

Bellabeat is a wellness brand for women with a variety of products and services focused on women’s health. The company develops wearables and accompanying products that monitor biometric and lifestyle data to help women better understand how their bodies work and make healthier choices. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women. By 2016, Bellabeat had opened offices around the world and launched multiple products. Bellabeat products became available through a growing number of online retailers in addition to their own e-commerce channel on their website. The company has invested in traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively.(https://bellabeat.com/)

### **Characters:**
* **Urška Sršen**: Bellabeat’s co-founder and Chief Creative Officer
* **Sando Mur**: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
* **Bellabeat marketing analytics team**: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’s mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.

### **Products:**
* **Bellabeat app**: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
* **Leaf**: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf Tracker connects to the Bellabeat app to track activity, sleep, and stress.
* **Time**: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
* **Spring**: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
* **Bellabeat membership**: Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health, beauty, and mindfulness based on their lifestyle and goals.

## **ASK**

### **Scenario**:
Urška Sršen, co-founder and Chief Creative Officer of Bellabeat believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. As a Junior Data Analyst, I have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. 

### **There are three main questions that need to be answered**:
1. What are some trends in smart device usage? 
2. How could these trends apply to Bellabeat customers? 
3. How could these trends help influence Bellabeat's marketing strategy?

### **Business task**
Perform data analysis on non-Beallabeat's products to discover consumer usage trends and provide founded insights and high-level recommendations to Bellabeat’s stakeholders Urška Sršen CCO and Sando Mur: Mathematician and Bellabeat’s cofounder.

## **PREPARE**

### **About the data**

The data source used in this analysis is a Kaggle data set. The crowd-sourced Fitbit dataset, dated 03.12.2016-05.12.2016, is in the form of 18 CSV files that were generated by respondents to a distributed survey via Amazon Mechanical Turk. It was placed in Zenodo, where it got a DOI and had a license of CC0: Public Domain.

The Digital Object Identifier DOI of this data is 10.5281/zenodo.53894. It was posted on Zenodo by Furberg, Robert; Brinton, Julia; Keating, Michael; Ortiz, Alexa. The data was collected through a survey so there are limitations on verifying its integrity, however, the data was used and uploaded in Zenodo, which is a safe and credible website operated by CERN and OpenAIRE to ensure that everyone can join in Open Science.

There are some issues with bias or credibility in this data. Data could be biased since there is no information about consumers who submitted the responses, we are not aware of their gender, age, and so on. The data is not from Bellabeat's product and the usage of FitBit could slightly differ from BellaBeat's products. Ideally, to make data-driven decisions and have data analysis for BellaBeat, we would have the data from the BellaBeat product.

### **Evaluation of ROCCC**

* **Reliable** - Data is not necessarily very reliable since it’s not Bellabeat’s data and it’s only 30 consumers' data.
* **Original** - The data is not original and was produced by a third party - Amazon Mechanical Turk.
* **Comprehensive** - The data is somewhat comprehensive since it has 18 datasets, that include calories, steps, sleep and so on which are relevant to our analysis.
* **Current** - The data is from 2016 so it’s not super current. At the time of the analysis, it’s 7 years old, which could mean that usage and trends during this time have changed.
* **Cited** – The data on Kaggle has been used many times by various analysts, in Zenodo, where it got the DOI, it was cited 3 times.

## **PROCESS**

### **Tools for the process**

To clean, manipulate, and analyze the data I have chosen **R programming language**. I will ensure data integrity by not making any changes to the actual data, but rather creating new data frames and manipulating data that way. Also, I will be keeping notes of all changes made and actions taken regarding this data.

### **Start of data processing**

I have uploaded the dataset to **RStudio**. Once all 18 CSV files have been uploaded, I have installed and uploaded tidyverse package and set the working directory.
```
# installing and uploading tidyverse
install.packages("tidyverse")
library(tidyverse)
# setting working directory
setwd("/cloud/project/Fitabase Data 4.12.16-5.12.16")
```

### **Choosing the files to work with**

I looked through the CSV files in the File pane and immediately decided not to use the following files: 

hourlyCalories_merged.csv, hourlySteps_merged.csv, minuteCaloriesNarrow_merged.csv, minuteCaloriesWide_merged.csv, minuteIntensitiesNarrow_merged.csv, minuteIntensitiesWide_merged.csv, minuteSleep_merged.csv, minuteStepsNarrow_merged.csv, minuteStepsWide_merged.csv, minuteMETsNarrow_merged.csv.

I chose to analyze daily patterns rather than minute and hour ones because I believe they will provide more useful insights. Then, I read the remaining CSV files and assigned them data frames.

```
#reading files in the data set and assigning them data frames
daily_activity<-read.csv('dailyActivity_merged.csv')
daily_calories <- read.csv('dailyCalories_merged.csv')
daily_intensities <- read.csv('dailyIntensities_merged.csv')
daily_steps <- read.csv('dailySteps_merged.csv')
heartrate_seconds <- read_csv('heartrate_seconds_merged.csv')
hourly_intensities <-read.csv('hourlyIntensities_merged.csv')
minute_METs <- read.csv('minuteMETsNarrow_merged.csv')
sleep_day <- read.csv('sleepDay_merged.csv')
weight_log_info <- read.csv('weightLogInfo_merged.csv')
```

After assigning CSV files data frames, I got familiar with the data, to see which CSV files I would be using for the analysis. I used head() and n_distinct() functions to get familiar with data frames daily_activity, daily_calories, daily_intensities, daily_steps.

```
#trying to get familiar with data 
head(daily_activity)
head(daily_calories)
head(daily_intensities)
head(daily_steps)
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_steps$Id)
```

<img width="651" alt="head1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/c815230a-dd72-4fac-acf5-b920303ff82f">
<img width="671" alt="head 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/e1323a5d-ad88-4e5a-99b5-025df65e4424">

From performing this code, it was obvious that daily_calories, daily_intensities, and daily_steps are already in the daily_activity data frame, so I will be using daily_activity data frame for further analysis. There are also 33 distinct Ids in all 4 data frames, where it should be 30.

Next, I got familiar with the remaining data frames.

```
# getting familiar with heartrate_seconds data frame
head(heartrate_seconds)
n_distinct(heartrate_seconds$Id)
```

<img width="192" alt="heart" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/28adee23-8a1e-439c-9e3b-f947c2ba103b">

After executing the code it was clear that there are less than half unique Id's than it should be, so this data frame will not be used for further analysis. Next, I got familiar with hourly_intensities and sleep_day data frames.

```
# getting familiar with hourly_intensities and sleep_day data frames
head(hourly_intensities)
n_distinct(hourly_intensities$Id) 
head(sleep_day)
n_distinct(sleep_day$Id)
```

<img width="429" alt="head 3" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/14c2efd2-1a71-4afb-9c88-1e20457cf62c">

After executing the code, it looks like these two data sets can be useful for further analysis.

```
# getting familiar with weight_log_info data frame
head(weight_log_info)
n_distinct(weight_log_info$Id)
```

<img width="434" alt="head 4" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/7b252bd1-0456-475f-bab1-25b78ba87551">

Unfortunately, after running the code it was clear that I could not use the data frame weight_log_info, since there are only 8 distinct Ids in this data frame. 

### **Files that will be used for processing and analysis:**

After reviewing all data frames, I have decided to use the following for further processing and analysis:

* **daily_activity**
* **hourly_intensities**
* **sleep_day**

### **Cleaning selected data frames - Daily Activity**

First, I've started with the **daily_activity** data frame. Running glimpse() and str() functions gave me basic information like the data frame has 940 rows and 15 columns, I was also presented with the data type of each variable. That is where I've noticed that ActivityDate is a character and not a date type of variable, which I would need to change.

```
# gathering basic information about daily_activity data frame
glimpse(daily_activity)
str(daily_activity)
```

<img width="642" alt="daily activity 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/38c39c34-ea55-4b71-96fa-5c320629e2c6">

I've checked to see how many distinct Ids there were, also if there were any NA values or duplicates. Distinct 33 Id, no NA or duplicate values were found.

```
# number of distinct Id in the daily_activity data frame
n_distinct(daily_activity$Id)

# checking to see if there is any null values in the data frame 
sum(is.na(daily_activity))

# checking for duplicates
sum(duplicated(daily_activity))
```
<img width="290" alt="daily activity 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/b216ba0c-6ab6-49fa-8152-d9b3e46b9c7c">

Since there were no NA values, and no duplicates, it was time to change the data type of ActivityDate. I've installed the necessary package lubridate and changed the data type.

```
# installing and leading needed package
install.packages("lubridate")
library(lubridate)
​
#changing ActivityDate data type
daily_activity$Date <- mdy(daily_activity$ActivityDate)
​
#checking to see if the data type has been changed correctly
str(daily_activity)
```

<img width="491" alt="daily activity 3" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/5f2b571a-3d6a-46cb-a73c-7abc33db86a0">

The next step was creating a new column from Date that would showcase Date in Weekday format. Also creating new columns transforming minutes to hours, changing data type of Calories and Total_Steps cleaning up column names, and making them neater. At last, I created a new data frame with only those columns that I intended to use.

```
# now I will be creating a new column for weekdays
daily_activity$Weekday <- wday(daily_activity$Date, label=TRUE)
head(daily_activity)

# creating active hours column combining all activities
daily_activity$ActiveHours <-((daily_activity$VeryActiveMinutes)+(daily_activity$FairlyActiveMinutes)+
                                (daily_activity$LightlyActiveMinutes))/60

# creating sedentary hours column
daily_activity$SedentaryHours <-(daily_activity$SedentaryMinutes)/60

# creating different active hours columns
daily_activity$VeryActiveHours <-(daily_activity$VeryActiveMinutes)/60
daily_activity$FairlyActiveHours <-(daily_activity$FairlyActiveMinutes)/60
daily_activity$LightlyActiveHours <-(daily_activity$LightlyActiveMinutes)/60

# making the column names neat
colnames(daily_activity) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(daily_activity))

#making calories and total steps as numeric 
daily_activity$Calories <- as.numeric(daily_activity$Calories)
daily_activity$Total_Steps <- as.numeric(daily_activity$Total_Steps)

# creating data frame from daily_activity with only columns that I will use
library(dplyr)
daily_activity2 <- daily_activity %>%
  select(Id, Date, Weekday, Calories, Total_Steps, Total_Distance, Very_Active_Distance, Moderately_Active_Distance, Light_Active_Distance, Active_Hours, Sedentary_Hours, Very_Active_Hours, Fairly_Active_Hours, Lightly_Active_Hours) 
head(daily_activity2)
```
<img width="691" alt="daily activity 4" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/5bcda388-d4f2-4fd2-86fb-12b9f74d4ad4">
<img width="712" alt="daily activity 5" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/b212e277-af6a-40ad-965e-1a0c4629f632">
<img width="742" alt="daily activity 6" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/42638763-f7a4-40fa-8eed-652fa2d1c62c">

Cleaning and manipulating daily activity was done. Next, it was time for another data frame.

### **Cleaning selected data frames - Hourly Intensities**

I've run head(), glimpse(), and str() for basic information about the data frame. The hourly intensities data frame consists of 4 columns and 22099 rows. ActivityHour contains date and time in one column, so I will separate them and change the data type of Time. Also, column names need some manipulation to make them neater.

```
# now lets dive in to another data set - hourly intensities
head(hourly_intensities)
str(hourly_intensities)
glimpse(hourly_intensities)

#checking for distinct Ids
n_distinct(hourly_intensities$Id)

# check if there is na values
sum(is.na(hourly_intensities))

# checking for duplicates
sum(duplicated(hourly_intensities))
```

I've also checked for unique Ids, NA values, and duplicates. The number of unique Ids is 33, and no Null values or duplicates were found. Then, I manipulated the column names and separated Activity_Hour column into 2 using the str_split_fixed() function. I've changed the Time data type and formatted it so that when I will need to make a chart the hours will go in order.

```
# after looking at the data set, we can see that we need to make col names neat

colnames(hourly_intensities) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(hourly_intensities))
glimpse(hourly_intensities)

# create two separate columns from activity hour to have only hours and only date

library(stringr)

hourly_intensities[c('Date', 'Time')] <- str_split_fixed(hourly_intensities$Activity_Hour, ' ', 2)

#changing the format of new column Time

install.packages("chron")
library(chron)

hourly_intensities$Time <- strptime(hourly_intensities$Time, format = "%I:%M:%S %p")

# extract only the hours and format the result to include AM/PM
hourly_intensities$Time <- factor(format(hourly_intensities$Time, format = "%I %p"),
                                  levels = c("12 AM", "01 AM", "02 AM", "03 AM", "04 AM", "05 AM", 
                                         "06 AM", "07 AM", "08 AM", "09 AM", "10 AM", "11 AM", 
                                         "12 PM", "01 PM", "02 PM", "03 PM", "04 PM", "05 PM", 
                                         "06 PM", "07 PM", "08 PM", "09 PM", "10 PM", "11 PM"))

glimpse(hourly_intensities)
```
<img width="725" alt="hourly intensities 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/278ed693-bb40-4f4b-b4db-e150f1cecb80">
<img width="733" alt="hourly intensities 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/a451ebfe-8289-4f0e-acfe-d60b877d3990">

Cleaning and manipulating of **hourly intensities** data frame was done. Next, it was time to clean and manipulate **sleep day** data frame.

### **Cleaning selected data frames - Sleep Day**

I've run head(), glimpse(), and str() for basic information about the data frame. The sleep day data frame  consists of 5 columns and 413 rows. I've also checked for unique Ids, NA values, and duplicates. The number of unique Ids is 24, no Null values but 3 duplicates were found. I've removed duplicates with distinct() functions and manipulated column names.

```
# cleaning the sleep data data frame
head(sleep_day)
glimpse(sleep_day)
str(sleep_day)

# unique Ids
n_distinct(sleep_day$Id)

#checking for NA values
sum(is.na(sleep_day))

# checking for duplicates
sum(duplicated(sleep_day))

#removing duplicates
sleep_day <- distinct(sleep_day)
sum(duplicated(sleep_day))

#making col names neat
colnames(sleep_day) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(sleep_day))
View(sleep_day)
```

<br> <img width="734" alt="sleep day" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/bdac6788-ceb2-4058-962b-c0550d42c834">
<br> <img width="347" alt="sleep day 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/eb30edfa-1a87-414d-b1ac-efa45901b553">
<br> <img width="360" alt="sleep day 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/05e70d11-a160-4d76-9891-7ecaa929b521">

Cleaning of all three selected data frames was done. Now the time has come for analysis of the data.

## **ANALYZE**

### **Analysing daily_activity2 data frame**

I have started with a function summary() to obtain the statistical data of variables from daily_activity2.

```
# data analysis of daily activity starts
summary(daily_activity2)

# from this we get important information on mean of variables like
# daily calories, steps and distance
```
<img width="712" alt="analysis daily activity2 " src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/0daf19cb-000f-4e29-8316-74fdcf22f7de">

This provided me with the average daily calories burned 2304, which fits into the normal interval of burned calories per day. According to Cleaveland Clinic, humans burn 1300-2000 calories per day without working out, but that depends on age, sex, and so on. (https://health.clevelandclinic.org/calories-burned-in-a-day/)

Another statistic that I have observed is the average daily steps taken, which was 7638. The recommended step count per day is 8000 - 10000, so our consumers could do a little better in achieving that goal. (https://utswmed.org/medblog/how-many-steps-per-day/)

Next, I have created a graph to showcase which days of the week people were more active.

```
# now we will see which days in a week people are more active

install.packages("ggplot2")
library(ggplot2)

Frequency_Weekdays <- ggplot(daily_activity2, aes(x = factor(format(Date, "%a"), levels = c("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")))) +
  geom_bar(fill = "lightpink") +
  labs(title = "Frequency on Weekdays",
       x = "Weekdays",
       y = "Frequency") +
  theme_classic()

print(Frequency_Weekdays)

ggsave("Frequency_Weekdays.png", plot = Frequency_Weekdays, device = "png")

# looks like people are mostly active on tues, wend, and thurs, and then the usage of 
# wellness app drops towards the weekend
```
<img width="535" alt="freq weekdays" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/e795e1f0-7812-4d30-9860-6b493e33a266">

The data suggests that people are mostly active on Tuesday, Wednesday, and Thursday. Then their activity slowly drops on the weekends and on Monday we observe a slight rise compared to Sunday. 

Next, I created a pie chart representing different activity hours logged during the day.

```
# now I will make a pie chart for active hours and sedentary hours 

# first I will calculate sums of all hours loged, sedentary and active

Total_Sedentary_Hours <- sum(daily_activity2$Sedentary_Hours)
Total_Very_Active_Hours <- sum(daily_activity2$Very_Active_Hours)
Total_Fairly_Active_Hours <- sum(daily_activity2$Fairly_Active_Hours)
Total_Lightly_Active_Hours <- sum(daily_activity2$Lightly_Active_Hours)

# then I will create a data frame where these calculations will be stored

hours_chart_data <- data.frame (
  Variable = c("Very Active Hours", "Fairly Active Hours","Lightly Active Hours", "Sedentary Hours"),
  Value = c(Total_Very_Active_Hours, Total_Fairly_Active_Hours, Total_Lightly_Active_Hours, Total_Sedentary_Hours))

# then I will create percentage values for better representation

percentages <- round(100 * hours_chart_data$Value / sum(hours_chart_data$Value), 1)

# create a vector of labels with percentages
labels_with_percentages <- paste(hours_chart_data$Variable, percentages, "%")

# to have nicer color themes I will use RColorBrewer package

install.packages("RColorBrewer")
library(RColorBrewer)
library(graphics)
# pick a pallet and pick label size and creating the pie chart

myPalette <- brewer.pal(5, "RdPu") 
label_size <- 0.6

png("pie.png")

pie <- pie(hours_chart_data$Value, 
           labels = labels_with_percentages, 
           main = "Percentage of Logged Hours", 
           cex.main = 1.2, 
           radius = 1, 
           border = "white", 
           col = myPalette, 
           cex = label_size)

# created a pie chart and saved it as pdf for better quality
# this data suggest that people mostly log sedentary hours, wich take up
# more than 81 % of all hours logged 

dev.off()

# dev.off() function for closing plots
```
<img width="665" alt="pie" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/cab32d7d-5037-45cd-a407-74fdf7450040">

The data suggest that users mostly log sedentary hours, which added up to 81.3%. This could either be the fault of not being active enough or simply forgetting to log a workout or activity in the tracker. According to Fitbit, it takes at least 15 min for the tracker to start recording activity, so this could be one of the reasons that the user is mostly unactive during the day.

The next graph that I've decided to create was Steps vs Calories. This was done to see if there is any positive relationship between these two metrics.

```
# now I will create a scatter plot to see if there is any relationship 
# between steps and calories 

Steps_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Total_Steps, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Steps Taken vs Calories Burned") +
  xlab("Calories") + ylab("Steps")+
  scale_color_gradient(low = "pink", high = "pink3")

print(Steps_vs_Calories)

ggsave("Steps_vs_Calories.png")

# as we can see there is positive correlation in the graph, showing that for 
# every Id the more steps taken the more calories are burned, which was expected
```
<img width="424" alt="steps vs calories" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/2cc54e0d-13dd-4d67-ac94-a4a35420a211">

I observed a positive relationship between steps taken and calories burned per day. This means that for the most part, the more steps were taken the more calories were burned.

Next, I wanted to see how calories correlated with active and sedentary hours. I have made two graphs called Active Hours vs Calories and Sedentary Hours vs Calories.

```
#now let see if there is any correlation between active hours and calories

Active_hours_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Active_Hours, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Active Hours vs Calories") +
  xlab("Calories") + ylab("Active Hours")+
  scale_color_gradient(low = "lightblue1", high = "lightblue3")

print(Active_hours_vs_Calories)

ggsave("Active_hours_vs_Calories.png")

# there is a positive correlation to more active hours per day, more calories are burned

Sedentary_hours_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Sedentary_Hours, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Sedentary Hours vs Calories") +
  xlab("Calories") + ylab("Sedentary Hours")+
  scale_color_gradient(low = "seagreen1", high = "seagreen4")

print(Sedentary_hours_vs_Calories)

ggsave("Sedentary_hours_vs_Calories.png")

# we can see that really sedentary hours does not have much of correlation with 
# calories burned during the day, as long as you are moving at least a little bit,
# you will be burning calories and the rest of the day with sedentary life style will 
# have no effect
```

<img width="518" alt="active hours vs calories" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/6ed586a7-67de-4f61-bc7d-7a5c04b045de">
<img width="634" alt="sedentary hours vs calories" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/24208005-946f-4936-8a34-d6ac13f6377b">

The data suggest that as predicted active hours have a positive relationship with calories, so the more active you are the more calories you burn. The sedentary hours have, for the most part, no relationship with burned calories. This would mean that no matter how sedentary your lifestyle is if you are active for a short period of time, you can burn calories during the day.

The next relationship that I wanted to explore was how activity differences affected distance.

```
#now lets see how does activity differences translates to  distance 

library(dplyr)

activity_distance <- daily_activity2 %>%
  summarize(
    distance = c(sum(Very_Active_Distance), sum(Moderately_Active_Distance), sum(Light_Active_Distance)),
  active_hours = c(sum(Very_Active_Hours), sum(Fairly_Active_Hours), sum(Lightly_Active_Hours)))

#creting new column  
activity_types= c("Very Active", "Fairly Active", "Lightly Active")
activity_distance$activity_types = activity_types
activity_distance$ratio <- activity_distance$distance/activity_distance$active_hours

View(activity_distance)

# form this table we can see that very active hours has largest ratio, meaning 
# that that 1 active hour is giving 4 miles in comparison lightly active hour gives us only 1 mile
```

<img width="226" alt="activity distance" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/d6fe28ed-14fc-4e76-bcc5-9f458b31f266">

From the table above we can see that very active hours have the largest ratio, which means that 1 active hour gives 4 miles of distance, in comparison lightly active hour gives us only 1 mile distance. This ratio suggests that you could reach your distance goals and have a more productive workout with higher intensity.

Next, I wanted to see different activity types of hours in correlation with burned calories.
```
# now let's see how activity type affects calories

install.packages("ggpubr")
library(ggpubr)

Very_Active_Hours_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Very_Active_Hours, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Very Active Hours vs Calories") +
  xlab("Calories") + ylab("Very Active Hours")+
  scale_color_gradient(low = "palevioletred1", high = "palevioletred4")

Fairly_Active_Hours_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Fairly_Active_Hours, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Fairly Active Hours vs Calories") +
  xlab("Calories") + ylab("Fairly Active Hours")+
  scale_color_gradient(low = "paleturquoise1", high = "paleturquoise4")

Lightly_Active_Hours_vs_Calories <- ggplot(daily_activity2, aes(x=Calories, y=Lightly_Active_Hours, color=(Id)))+
  geom_point()+
  geom_smooth(method="loess", se=TRUE, fullrange=FALSE, level=0.95, color="black")+
  ggtitle("Lightly Active Hours vs Calories") +
  xlab("Calories") + ylab("Lightly Active Hours")+
  scale_color_gradient(low = "palegreen", high = "palegreen4")

ggarrange(Very_Active_Hours_vs_Calories, Fairly_Active_Hours_vs_Calories, Lightly_Active_Hours_vs_Calories, 
          ncol = 2, nrow = 2)
```

<img width="669" alt="diff active hours" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/bf49c933-b2fa-4f02-b2b4-5224afa11ff0">

With the graphs above we are watching an interesting correlation. As expected, the very active hours burn calories with the highest positive correlation. Fairly active hours have a slow rise of burned calories compared to hours passed and could mean a very weak positive correlation, but lightly active hours show a rapid rise and then at around 2000 cal, 4 hours, the curve is linear, which would mean that there is no correlation between two metrics.

### **Analysing hourly_intensities data frame**

With this data set, I wanted to see which hours of the day were mostly logged and therefore the most active. First I grouped the data set by Time variable. 

```
time_intensity<- hourly_intensities %>%
  group_by(Time) %>%
  summarize(Sum_Total_Intensity=sum(Total_Intensity))

View(time_intensity)
```

Then I created a chart to observe the relationship between intensity and hours in the day.

```
intensity_vs_hour <- ggplot(time_intensity, aes(x = Time, y = Sum_Total_Intensity))+
  geom_col(fill = "lightpink") +
  labs(title = "Hourly Intensity",
       x = "Time",
       y = "Intensity") +
  theme_classic()
print(intensity_vs_hour)  
```

<img width="605" alt="hourly intensities graph" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/bf35cc08-d210-468a-8f7e-8f088393b607">

The graph suggests that users had the highest intensity logged from 5 PM to 7 PM. As expected we see very low activity from 11 PM until 5 AM. From 5 AM the intensity is rising steadily. The second highest wave is observed around 12 PM - 2 PM.

### **Analysing sleep_day data frame**

I wanted to figure out how many hours on average users sleep per night and how long does it take for them to fall asleep.
```
#how many hours on average sleeps
summary(sleep_day)
mean(sleep_day$Total_Minutes_Asleep)/60

#how many minutes spends in bed before falling asleep
sleep_day$Minutes_Awake <- sleep_day$Total_Time_In_Bed - sleep_day$Total_Minutes_Asleep

average_minutes_awake <- mean(sleep_day$Minutes_Awake, na.rm = TRUE)

print(average_minutes_awake)
```
<img width="470" alt="sleep day 3" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/e30c5180-4ba9-4f48-98da-ac9c1c120bf1">

On average users sleep 6.9 hours per night, which according to NIH is a little bit too little. To meet the minimum recommended hours of sleep adults should sleep 7-9 hours per night. (https://www.nhlbi.nih.gov/health/sleep/how-much-sleep)

When talking about minutes spent in bed before falling asleep, the Sleep Foundation recommends that it should take 15-20 min. In our case, it takes around 40 minutes (https://www.sleepfoundation.org/sleep-faqs/how-long-should-it-take-to-fall-asleep#:~:text=Most%20healthy%20people%20fall%20asleep,fall%20asleep%20easily%20every%20night)

## **SHARE**

![all visual](https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/4e05e311-27ef-4e41-86e2-ff1c763db06c)

### **Analysis Summary**

* The average daily calories burned is 2304. This exceeds the normal interval of burned calories per day, which is 1300-2000 calories per day. 
* The average daily steps taken is 7638. Users have not reached the recommended steps per day, which is 8000-10000.
* Most days that users logged their activity were Tuesday, Wednesday, and Thursday. The activity dropped over the weekend and started to slowly rise on Monday. 
* 81.3% of hours logged were sedentary, this could either be the fault of not being active enough or simply forgetting to log a workout or activity in the tracker.
* As expected, the daily steps and daily burned calories relationship has a positive correlation, meaning the more steps were taken the more calories were burned during the day. In the same way, active hours and daily calories have a positive correlation, the more active hours logged during the day the more calories burned. While sedentary hours and calories do not have any correlation. This is kind of expected but still exciting news, as no matter how sedentary our lifestyle is, if we move at least a little, calories will be burned.
* The ratio between different active hours and distance was highest in the very active hours type, which was 1 active hour to 4 miles of distance, in comparison 1 lightly active hour gave a 1-mile distance. This ratio suggests that users could reach their distance goals and have a more productive workout with higher intensity.
* When talking about different activity hours and their relationship with burned calories, as with distance metric, very active hours have a positive correlation, meaning the more active hours users logged the more calories were burned. I've noticed a trend that up until the 1-hour mark and around 3000, it's a super slow rise of hours, but calories are being burned fast. Once it hits that mark, the hours needed to burn calories rise significantly, and users have to stay very active for a longer time to burn more than 3000 calories. With fairly active hours it's a pretty weak positive correlation, and interestingly enough with lightly active hours, there is a positive correlation up until around 4 hours and 2000 calories mark, and then I observed no correlation at all. This would suggest that shorter, higher-intensity work would be beneficial for those who are trying to lose some weight.
* Hourly intensities logged during the day suggest that users had the highest intensity from 5 PM to 7 PM, which is typical after-work hours. As expected we see very low activity from 11 PM until 5 AM, as it is night time. From 5 AM the intensity is rising steadily. The second highest wave is observed around 12 PM - 2 PM, which is probably people who work night shifts and who are going to work out, or there is some waking done during lunch at work.
* Regarding sleep data, on average users sleep 6.9 hours per night, which according to NIH is not enough. To meet the minimum recommended hours of sleep adults should sleep 7-9 hours per night. 
* When talking about minutes spent in bed before falling asleep, the Sleep Foundation recommends that it should take 15-20 min. In our case, it takes around 40 minutes for users to fall asleep, which could mean that they either have some trouble falling asleep, or staying on their phones, etc.

## **ACT**

Bellabeat is a wellness brand for women with a goal to help women improve their health by developing wearables and accompanying products that monitor biometric and lifestyle data. After performing an analysis on non-Bellabeat products, I have identified user trends that can help not only Bellabeat's users but also influence the company's marketing strategy. 

As my assignment was to produce recommendations towards one of Bellabeat's products, I've chosen the Bellabeat app, which collects the activity, sleep, stress, menstrual cycle, and mindfulness habits of its users. This data closely resembles the type of data collected from Fitbit users (which was analyzed in this project) and therefore can be used in drawing conclusions regarding users of Bellabeat's app.

Before presenting the main conclusions and recommendations to stakeholders Urška Sršen CCO and Sando Mur, Mathematician, and Bellabeat’s cofounder, regarding Beallabeat's app, I would like to mention that the data that I have worked with was limited. It only had 24-33 unique users in datasets, there was no information on whether the users were women, their age, and so on. The data was also collected through external sources and came from non-Bellabeat products.

For the future, I would suggest continuing the analysis of user trends, however, the source of the data should be the Bellabeat app, the metadata would be important and the scope should be much larger than 30 users.

### **Conclutions**

According to the CDC (Centers for Disease Control and Prevention) living a non-active lifestyle can lead to heart disease, obesity, high blood pressure, high blood cholesterol, type 2 diabetes, and various cancers. Regular physical activity is one of the most important factors in improving people's health and it benefits everyone, regardless of their age, sex, race, ethnicity, or current fitness level. That being said, our analysis has shown that most logged hours (81.3%) of our users were sedentary, they were not hitting the recommended step count and had trouble falling asleep and sleeping the recommended 7-9 hours per day. It is truly important to encourage Bellabeats users to lead a more active lifestyle and understand its benefits. 

### **Recomendations**

**1. Reminder notifications**

Users have not reached the recommended steps per day, which is 8000-10000, the reached number was 7638. Notification could help users remember their step goal if they have one, or just by default target 10000 per day.

**2. Weekend challenge** 

Since I have observed users' activity declines on weekends, a "weekend fitness challenge" could be a great way to encourage people to be more active and log their activity on the weekends.

**3. The activity report**

During the analysis of users' logged hours, it was clear that striking 81.3% of logged time was sedentary. To avoid this in the Bellabeat app it is important to have clear communication with the user about the importance of logging their activity as it helps form recommendations, predictions, and suggestions for their healthy habits. After a month of usage, the user could get a monthly report with a short analysis of their data, however, the report would clearly communicate which days the app was not used and what percentage of accuracy the report is, this would help the user to understand that by logging the active time they are actually helping themselves.

**4. Move a little**

During the analysis, I learned that steps taken and active hours have a positive correlation with burned calories and that sedentary hours have no correlation. This is expected but still exciting news. With this information, the Bellabeat app could have a "Move a little" notification which would be prompted after a long period of sedentary activity logged on the app. It would encourage people to as it says move at least a little bit because that's all it takes to get closer to fitness goals or get those steps in.

**5. Recommended HITT workouts**

For someone who is trying to lose weight or reach a certain distance daily, data suggest that shorter higher intensity workouts would be the key. The Bellabeat app could have a recommended workouts section depending on the activity logged and preferences pre-defined by the user. 

**6. Motivation boost**

As I've learned from data analysis, the most active hours of the day are 12 PM to 2 PM and 5 PM to 7 PM. During this time people are most likely to be active therefore Bellabeat app could have "Motivational boost" notifications during these hours. If the person was working out and received a motivational message, it would validate their work, and if not, it would work as a reminder to be more active.

**7. Evening meditation**

User data suggest that people are not getting enough sleep and having a harder time falling asleep. To try and solve this issue Bellabeat app could have an "Evening meditation" integration which would recommend users a 5-minute meditation before sleep. This could potentially help users fall asleep and get the recommended 7-9 hours of sleep per day.

### **Recourses**

* FitBit Fitness Tracker Data (https://www.kaggle.com/datasets/arashnic/fitbit)
  
* Cleaveland Clinic "Here’s How Many Calories You Naturally Burn in a Day" (https://health.clevelandclinic.org/calories-burned-in-a-day/)
  
* UTSouthwestern Medical Center "Focusing on 10,000 steps a day could be a misstep" (https://utswmed.org/medblog/how-many-steps-per-day/)
  
* National Heart, Lung, and Blood Institute "How Much Sleep Is Enough?" (https://www.nhlbi.nih.gov/health/sleep/how-much-sleep)
  
* Sleep Foundation "How Long Should It Take to Fall Asleep?" (https://www.sleepfoundation.org/sleep-faqs/how-long-should-it-take-to-fall-asleep#:~:text=Most%20healthy%20people%20fall%20asleep,fall%20asleep%20easily%20every%20night)
  
* CDC "Physical Inactivity" (https://www.cdc.gov/chronicdisease/resources/publications/factsheets/physical-activity.htm#:~:text=Not%20getting%20enough%20physical%20activity%20can%20lead%20to%20heart%20disease,cholesterol%2C%20and%20type%202%20diabetes)



## The END :)
