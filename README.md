# Cohort Analysis

Cohort analysis is valuable for businesses as it allows them to understand user behavior in a more granular and actionable way. Below is the process I followed for the task of Cohort Analysis:

## Process Followed
1. Defined the cohorts based on a specific characteristic or event. For example, in an e-commerce platform, cohorts could be defined based on the month of a user’s first purchase.
2. Gathered relevant data for analysis.
3. Determined the time intervals to analyze.
4. Grouped users into cohorts based on the defined characteristic or event.
5. Chose the key performance metrics to analyze.
6. Calculated the chosen metrics for each cohort over the specified time periods.
7. Created visualizations to present the findings effectively.

A dataset for Cohort Analysis typically includes user or customer data, such as registration date, purchase history, engagement metrics, or any other data points relevant to the analysis.

## Cohort Analysis using Python
Now, I got started with the task of Cohort Analysis by importing the necessary Python libraries and the [dataset](https://statso.io/cohort-analysis-case-study/).

### Checking for Missing Values
```python
missing_values = data.isnull().sum()
print(missing_values)
```
```
Date               0
New users          0
Returning users    0
Duration Day 1     0
Duration Day 7     0
dtype: int64
```
### Checking Data Types
```python
data_types = data.dtypes
print(data_types)
```
```
New users            int64
Returning users      int64
Duration Day 1     float64
Duration Day 7     float64
dtype: object
```
The `Date` column was in object (string) format. For effective analysis, especially in cohort analysis, I converted this to a datetime format:
```python
# Convert 'Date' column to datetime format
data['Date'] = pd.to_datetime(data['Date'], format='%d/%m/%Y')
```

### Descriptive Statistics
```python
# Display the descriptive statistics of the dataset
descriptive_stats = data.describe()
print(descriptive_stats)
```
```
         New users  Returning users  Duration Day 1  Duration Day 7
count    30.000000        30.000000       30.000000       30.000000
mean   3418.166667      1352.866667      208.259594      136.037157
std     677.407486       246.793189       64.730830       96.624319
min    1929.000000       784.000000       59.047619        0.000000
25%    3069.000000      1131.500000      182.974287       68.488971
50%    3514.500000      1388.000000      206.356554      146.381667
75%    3829.500000      1543.750000      230.671046      220.021875
max    4790.000000      1766.000000      445.872340      304.350000
```

The descriptive statistics provided the following insights:
- **New Users:** The average number of new users is around 3,418 with a standard deviation of approximately 677. The minimum and maximum new users recorded are 1,929 and 4,790, respectively.
- **Returning Users:** On average, there are about 1,353 returning users, with a standard deviation of around 247. The minimum and maximum are 784 and 1,766, respectively.
- **Duration Day 1:** The average duration on the first day is about 208 seconds with a considerable spread (standard deviation is around 65).
- **Duration Day 7:** The average 7-day duration is lower, around 136 seconds, with a larger standard deviation of about 97. The range is from 0 to 304.

### Trend of New and Returning Users Over Time
![New and Returning Users Trend](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Trend%20of%20New%20and%20Returning%20Users%20Over%20Time.png)

### Trend of Duration Over Time
![Duration Trend](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Trend%20of%20Duration%20(Day%201%20and%20Day%207)%20Over%20Time.png)

### Correlation Between Variables
![Correlation Matrix](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Correlation%20Matrix%20of%20Variables.png)

The strongest correlation is between the number of new and returning users, indicating a potential trend of new users converting to returning users.

## Performing Cohort Analysis using Python
For the task of Cohort Analysis, I grouped the data by the week of the year to create cohorts. Then, for each cohort (week), I calculated the average number of new and returning users, as well as the average of Duration Day 1 and Duration Day 7. 

### Grouping Data by Week and Calculating Averages
```python
# Grouping data by week
data['Week'] = data['Date'].dt.isocalendar().week

# Calculating weekly averages
weekly_averages = data.groupby('Week').agg({
    'New users': 'mean',
    'Returning users': 'mean',
    'Duration Day 1': 'mean',
    'Duration Day 7': 'mean'
}).reset_index()

print(weekly_averages.head())
```
```
   Week    New users  Returning users  Duration Day 1  Duration Day 7
0    43  3061.800000      1267.800000      220.324375      225.185602
1    44  3503.571429      1433.142857      189.088881      168.723200
2    45  3297.571429      1285.714286      198.426524      143.246721
3    46  3222.428571      1250.000000      248.123542      110.199609
4    47  4267.750000      1616.250000      174.173330        0.00000
```

### Weekly Average of New and Returning Users and Duration
![Weekly Averages](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Weekly%20Average%20of%20New%20vs.%20Returning%20Users.png)
![Weekly Average of Duration (Day 1 vs. Day 7)](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Weekly%20Average%20of%20Duration%20(Day%201%20vs.%20Day%207).png)

### Cohort Chart for Weekly Averages
![Cohort Matrix](https://github.com/Sourabh1710/Cohort-Analysis/blob/main/images/Cohort%20Matrix%20of%20Weekly%20Averages.png)

From the cohort chart, I observed:
- The number of new users and returning users fluctuates from week to week.
- There was a significant increase in both new and returning users in Week 47.
- The average duration of user engagement on Day 1 and Day 7 varies across the weeks.
- The durations do not follow a consistent pattern concerning the number of new or returning users, suggesting that other factors might be influencing user engagement.

## Summary
Cohort Analysis is a data analysis technique used to gain insights into the behavior and characteristics of specific groups of users or customers over time. It is valuable for businesses as it allows them to understand user behavior in a more granular and actionable way.

---

## Author
Sourabh Sonker <br>
Data Scientist
