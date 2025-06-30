# 🚗 Uber Trip Analysis Project

## 📊 Project Overview
This project analyzes Uber ride data to uncover insights into trip durations, distance patterns, timing trends, and usage by purpose. The goal is to identify patterns that can help optimize operations and understand rider behavior.

## 📁 Dataset
- **Records:** Number of trips: **1,157**
- **Columns:** START_DATE, END_DATE, CATEGORY, START location, STOP location, MILES, PURPOSE

## ❓ Key Business Questions Answered
1. What's the average trip duration, and how does it vary by purpose?
2. Are there seasonal patterns in ride frequency?
3. Do business vs personal trips follow different timing patterns?
4. Do business trips get longer during rush hours?
5. Do certain purposes always require long-distance travel?

## 🧹 Data Cleaning & EDA & Feature Engineering
- Identified missing values; all of them were in the PURPOSE column
- Found an error in one row because it was an aggregation instead of a record
- Handled duplicates
- Converted date/time columns to appropriate formats
- Checked for the percentage of business trips vs personal trips
- Checked for outliers in duration and distance using histograms & boxplots
- Performed initial exploration of categorical variables (purpose, category)
- Calculated descriptive statistics
- Extracted features (START_HOUR, START_TIME, END_HOUR, END_TIME, Month_Name, DAY_OF_WEEK, Time of Day, TRIP_DURATION_TYPE, Route)

## 📈 Analysis & Insights

### 1. What's the average trip duration, and how does it vary by purpose?
The average trip duration is **23 minutes**, but the distribution of trip duration is right-skewed.

![Trip duration distribution](https://github.com/user-attachments/assets/128574bc-68e2-42d5-81e4-8d521bf763f8)

The median is a better measure of central tendency because it's not influenced by extreme values that make the mean misleading, so the average (median) = **16 minutes**.

| Purpose | Min Duration | Max Duration | StdDev Duration | Mean Duration | Median |
|---------|-------------|-------------|----------------|---------------|--------|
| Errand/Supplies | 2 | 57 | 10 | 13 | 10.00 |
| Moving | 11 | 21 | 5 | 15 | 14.00 |
| Meal/Entertain | 3 | 64 | 10 | 16 | 13.50 |
| Between Offices | 8 | 65 | 16 | 26 | 23.00 |
| Temporary Site | 5 | 103 | 18 | 26 | 20.00 |
| Airport/Travel | 15 | 34 | 10 | 26 | 29.00 |
| Charity ($) | 27 | 27 | N/A | 27 | 27.00 |
| Meeting | 5 | 166 | 27 | 30 | 22.00 |
| Customer Visit | 2 | 330 | 43 | 33 | 21.00 |
| Commute | 185 | 185 | N/A | 185 | 185.00 |

After reviewing the mean and standard deviation, the data shows high variability, and outliers significantly influence the average, especially for **(Meeting, Customer Visit, Temporary Site)**. We can ignore **(Charity($), Commute)** because they only have one record each, and **"NULL"** records because they might represent any other purpose. **"Moving"** doesn't show significant difference between average and median.

![Purpose trip duration distribution](https://github.com/user-attachments/assets/47efe038-bff5-442e-833a-4e8cbb7a9aef)

According to the box plots for each purpose, it's better to use the median as a measure of central tendency due to the presence of outliers.

**Conclusion**: Yes, the average trip duration varies significantly by purpose, and median is the better measure of central tendency for this dataset.

### 2. Are there seasonal patterns in ride frequency?

![Trip frequency](https://github.com/user-attachments/assets/12e0055d-ac84-4b91-931d-f53d3cbdddab)

This line chart displays monthly Uber trip counts categorized by purpose (Business and Personal) throughout 12 months:

- **February**: Business trips peaked (~100 rides), with gradual decline through March as personal trips slightly increased
- **April-May**: Stable period with consistent low-moderate activity
- **June-August**: Business trips increased, reaching annual peak in August, while personal trips also increased
- **September**: 70% drop in business trips (130 → 40)
- **Q4**: Sustained growth from October through December, reaching the highest point of the entire year (145 rides)

![Trip frequency per category Feb-Apr](https://github.com/user-attachments/assets/3d761bbd-bc9c-471b-aa65-8bf4f0a0027d)

After zooming into the line chart to investigate personal trips from **Feb-Apr**, during February and April, personal trips happen on weekends, but during March, personal trips occur when business trips stop.

![March Analysis](https://github.com/user-attachments/assets/dae5f267-a58d-4bcd-a47c-43baf6757677) ![March Details](https://github.com/user-attachments/assets/7b33a6dd-b174-4454-9dcb-ab881c78ee22)

These trips didn't have any purpose recorded. This could be due to Spring Break or Holy Week, when employees may take vacation, resulting in fewer business-related rides.

![July Analysis](https://github.com/user-attachments/assets/3dbc242c-d0d5-4cf6-8ac7-fc1841cff567)

For July, there were trips with recorded purposes that happened on weekends and during the period between July 12-20. This might be related to vacation time, as mid-July is prime summer tourism season, especially after the July 4th Independence Day holiday weekend.

### 3. Do business vs personal trips follow different timing patterns?

![Business vs Personal Timing](https://github.com/user-attachments/assets/6f426cae-09a0-45e0-a3cf-521e6ba02aac)

**Business Trips (Right Chart):**
- Peak Hours: 7 AM - 6 PM (Standard Business Hours)
- Morning rush: Strong activity from 7-10 AM
- Sustained high activity: 90+ trips consistently from 2-6 PM
- Evening decline: Sharp drop after 6 PM as business day ends
- Minimal night activity: Very low usage from 7 PM - 6 AM

**Personal Trips (Left Chart):**
- Peak Hour: 10-11 AM (11+ trips)
- Late morning peak: Maximum activity around 10 AM (weekend/leisure timing)
- Sustained daytime activity: Moderate levels throughout afternoon (4-7 trips)
- Evening activity: Continues into evening hours (unlike business trips)
- Night presence: Some activity even in late evening/night hours

### 4. Do business trips get longer during rush hours?

![Rush Hour Analysis](https://github.com/user-attachments/assets/bb902c88-1290-42b5-88c6-25414c54f8f3)


Looking at the histogram, we find that most trips happen between 8 AM and 9 PM. After reviewing the box plot, we see that we hit peak rush hour at 9 AM at the start of the day and then at 4 PM at the end of the day.

| Hour | Average Trip Duration | Count of Trips |
|------|----------------------|----------------|
| 0 | 14.29 | 17 |
| 1 | 18.40 | 5 |
| 2 | 73.50 | 2 |
| 3 | 25.00 | 3 |
| 5 | 14.75 | 4 |
| 6 | 23.00 | 4 |
| 7 | 23.08 | 12 |
| 8 | 24.44 | 34 |
| 9 | 24.94 | 50 |
| 10 | 19.53 | 60 |
| 11 | 21.13 | 61 |
| 12 | 23.54 | 70 |
| 13 | 23.67 | 89 |
| 14 | 22.02 | 83 |
| 15 | 25.68 | 91 |
| 16 | 31.50 | 84 |
| 17 | 23.74 | 90 |
| 18 | 19.02 | 89 |
| 19 | 21.87 | 63 |
| 20 | 22.00 | 67 |
| 21 | 22.35 | 48 |
| 22 | 26.57 | 30 |
| 23 | 28.76 | 21 |

Comparing the average trip duration in rush hours vs non-rush hours (we will ignore hours 2 and 3 because they only have 2-3 trips), we can clearly see from the box plot and the table of hours that rush hours show peak trip averages of the day. During the night from 1 AM to 7 AM, the trip duration on average is less than during the day from 7 AM to 11 PM.

**Rush Hour Analysis:**
- **Morning Rush Hour (7-9 AM)**: Average 23.08-24.94 minutes
- **Evening Rush Hour (3-6 PM)**: Peak at 4 PM (16:00) with **31.50 minutes** - the highest duration of the day
- **Off-Peak Hours (10 AM-2 PM)**: Lower averages (19.53-23.67 minutes)
- **Night Hours (12 AM-6 AM)**: Significantly lower durations (14.29-23.00 minutes, excluding outlier at 2 AM)
- **Late Evening (10-11 PM)**: Higher durations (26.57-28.76 minutes)

**Key Observations:**
- **Highest Duration**: 4 PM (31.50 minutes) during evening rush hour
- **Lowest Duration**: 12 AM (14.29 minutes) and 5 AM (14.75 minutes)
- **Clear Pattern**: Rush hours (7-9 AM, 3-6 PM) consistently show longer durations than off-peak hours
- **Evening Rush Impact**: Most pronounced at 4 PM, likely due to heavy traffic and longer routes

**Statistical Comparison:**
- **Rush Hours Average**: ~27 minutes (7-9 AM, 3-6 PM)
- **Off-Peak Hours Average**: ~21 minutes (10 AM-2 PM, 7-11 PM)
- **Night Hours Average**: ~18 minutes (12-6 AM, excluding outliers)

**Conclusion**: Yes, business trips do get significantly longer during rush hours, with evening rush hour (particularly 4 PM) showing the most dramatic increase in trip duration. The 4 PM slot shows a 65% increase compared to the typical off-peak duration.

### 5. Do certain purposes always require long-distance travel?

| Purpose | Average Miles | Frequency | Min Miles | Max Miles | StdDev Miles |
|---------|---------------|-----------|-----------|-----------|--------------|
| Commute | 180.2 | 1 | 180.2 | 180.2 | N/A |
| Customer Visit | 20.7 | 101 | 0.8 | 310.3 | 40.6 |
| Meeting | 15.3 | 186 | 0.7 | 201.0 | 25.2 |
| Charity ($) | 15.1 | 1 | 15.1 | 15.1 | N/A |
| Between Offices | 10.9 | 18 | 1.9 | 39.2 | 8.5 |
| Temporary Site | 10.5 | 50 | 1.8 | 48.2 | 7.8 |
| Meal/Entertain | 5.7 | 160 | 0.6 | 36.5 | 5.0 |
| Airport/Travel | 5.5 | 3 | 4.1 | 7.6 | 1.9 |
| Moving | 4.6 | 4 | 3.3 | 6.1 | 1.2 |
| Errand/Supplies | 4.0 | 128 | 0.5 | 22.3 | 3.5 |

As we can see, **(Meeting, Temporary Site, Customer Visit, Between Offices)** have high to moderate standard deviations and a significant difference between min and max values.

![Distance Distribution](https://github.com/user-attachments/assets/36b6dd88-6c82-4a7c-8fb9-06178f99f1cf)

From the histogram, we see that these purposes are right-skewed, meaning their averages are highly influenced by outliers. For **(Meeting, Temporary Site, Customer Visit)**, it's better to use median as a measure of central tendency. For **Between Offices**, the average might be acceptable, but we can't be certain because we only have 18 records for this purpose. After collecting more data, we can make a more definitive decision.

## 🔍 Key Findings Summary
- **Trip Duration**: Median duration is 16 minutes; varies significantly by purpose with business-related trips generally taking longer
- **Seasonal Patterns**: Clear seasonal trends with Q4 showing highest activity; March shows unique pattern possibly due to spring break
- **Timing Patterns**: Business trips follow standard work hours (7 AM-6 PM), while personal trips peak mid-morning and extend into evening
- **Rush Hour Impact**: Peak activity occurs at 9 AM and 4 PM, but further analysis needed to determine impact on trip duration
- **Distance by Purpose**: Customer visits and meetings show highest variability in distance; most purposes show right-skewed distributions

## 🎯 Business Recommendations
- **Capacity Planning**: Increase driver availability during Q4 and reduce during March spring break period
- **Pricing Strategy**: Consider dynamic pricing for high-variability purposes (Customer Visit, Meeting)
- **Service Optimization**: Focus on business hour coverage (7 AM-6 PM) for maximum utilization
- **Route Planning**: Implement better route optimization for variable-distance purposes

## 🛠️ Tools Used
- **Data Processing**: Excel, Power Query
- **Visualization**: Power BI
- **Analysis**: Statistical analysis using descriptive statistics and distribution analysis

## 📂 Repository Structure
```
├── data/
│   ├── raw_data.xlsx
│   └── cleaned_data.xlsx
├── analysis/
│   ├── exploratory_analysis.pbix
│   └── statistical_analysis.xlsx
├── visualizations/
│   └── charts_and_graphs/
├── README.md
└── requirements.txt
```
