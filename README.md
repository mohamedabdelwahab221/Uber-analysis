# 🚗 Uber Trip Analysis Project

## 📊 Project Overview
This project analyzes Uber ride data to uncover insights into trip durations, distance patterns, timing trends, and usage by purpose. The goal is to identify patterns that can help optimize operations and understand rider behavior.

## 📁 Dataset
- **Records:** Number of trips: **1157**
- **Columns:** START_DATE, END_DATE, CATEGORY, START location, STOP location, MILES, PURPOSE.

## ❓ Key Business Questions Answered
1. What’s the average trip duration, and how does it vary by purpose?
2. Are there seasonal patterns in ride frequency?
3. Do business vs personal trips follow different timing patterns?
4. Do business trips get longer during rush hours?
5. Do certain purposes always require long-distance travel?

## 🧹 Data Cleaning & EDA & Feature engineering
- Identified missing values; all of them were in the purpose column.
- There was an error in one row because it was an aggregation instead of a record
- Handled duplicates
- Converted date/time columns to appropriate formats
- Checked for the percentage of business trips vs personal trips
- Checked for outliers in duration and distance using histograms & boxplots
- Performed initial exploration of categorical variables (purpose, category)
- Performed Descriptive statistics
- Extracted Features (START_HOUR, START_TIME, END_HOUR, END_TIME, Month_Name, DAY_OF_WEEK, Time of Day, TRIP_DURATION_TYPE, Route)

## 📈 Analysis & Insights
### 1. What’s the average trip duration, and how does it vary by purpose?
   > The average trip duration is **23**, but the distribution of the trip duration is right-skewed
   > 
   > ![Trip duration distribution](https://github.com/user-attachments/assets/128574bc-68e2-42d5-81e4-8d521bf763f8)
   > 
   > The median is a better measure of central tendency because it's not influenced by the extreme values that make the mean misleading
   > so the average (median) = **16**
   >
   > | Purpose | Min of TRIP_DURATION | Max of TRIP_DURATION | StdDev of TRIP_DURATION | Average of TRIP_DURATION | median |
   > |---------|---------------------|---------------------|------------------------|--------------------------|--------|
   > | Errand/Supplies | 2 | 57 | 10 | 13 | 10.00 |
   > | Moving | 11 | 21 | 5 | 15 | 14.00 |
   > | Meal/Entertain | 3 | 64 | 10 | 16 | 13.50 |
   > | Between Offices | 8 | 65 | 16 | 26 | 23.00 |
   > | Temporary Site | 5 | 103 | 18 | 26 | 20.00 |
   > | Airport/Travel | 15 | 34 | 10 | 26 | 29.00 |
   > | Charity ($) | 27 | 27 | #DIV/0! | 27 | 27.00 |
   > | Meeting | 5 | 166 | 27 | 30 | 22.00 |
   > | Customer Visit | 2 | 330 | 43 | 33 | 21.00 |
   > | Commute | 185 | 185 | #DIV/0! | 185 | - |
   >
   > After reviewing the average and standard deviation, the data is spread, and outliers might influence the average
   > spectialy **(Meeting, Customer Visit, Temporary Site)** and we can ignore **(Charity($) , Commute)** because it only has one record , and **"NULL"** recordes because it might be any other purpose
   > and **"moving"** doesn't have any difference between average and median
   >
   > ![purpose trip duration distribution](https://github.com/user-attachments/assets/47efe038-bff5-442e-833a-4e8cbb7a9aef)
   >
   > So, according to this, box plots for each purpose we needed to investigate, it's better to use the median as a measure of central tendency
   > 
   > **in conclusion**: yes, the average varies by purpose and its better to use median as measure of central tendency

### 2. Are there seasonal patterns in ride frequency?
   >![trip freq](https://github.com/user-attachments/assets/12e0055d-ac84-4b91-931d-f53d3cbdddab)
   >
   >This line chart displays monthly Uber trip counts categorized by purpose (Business and Personal) throughout 12 months
   >Business trips showed early strength with February peak (~100 rides), Gradual decline through March as personal trips slightly increased
   >April-May: Stable period with consistent low-moderate activity
   >June-August: Business trips increased, reaching annual peak in August, while personal trips increased as happened in Feb-Mar
   >September 70% drop in business trips (130 → 40)
   >Q4 Sustained growth from October through December reached the highest point of the entire year (145 rides)
   >
   >![trip freq per category feb-apr](https://github.com/user-attachments/assets/3d761bbd-bc9c-471b-aa65-8bf4f0a0027d)
   >
   >so after zooming in the line chart to investigate the personal trips from **feb-apr** during feburay and aprail the personal trips happen on week ends
   >but during march personal trips happens with busniss trips stoping
   >
   >![image](https://github.com/user-attachments/assets/dae5f267-a58d-4bcd-a47c-43baf6757677) ![image](https://github.com/user-attachments/assets/7b33a6dd-b174-4454-9dcb-ab881c78ee22)
   >
   >and this trip didnt have any record of its purpose so This could be due to Spring Break or Holy Week, when employees may take vacation, resulting in fewer business-related rides.
   >
   >![image](https://github.com/user-attachments/assets/3dbc242c-d0d5-4cf6-8ac7-fc1841cff567)
   >
   >and for july there were trips with purpose recored that happen in the weekends and the time period between 12-20 july
   >it might be related to vication Mid-July is prime summer tourism season, especially after a holiday weekend which happend that 4th july is The Independence Day in USA
   >
### 3. Do business vs personal trips follow different timing patterns?
   >
>![image](https://github.com/user-attachments/assets/6f426cae-09a0-45e0-a3cf-521e6ba02aac)
>
>**Business Trips (Right Chart)**
>
>Peak Hours: 7 AM - 6 PM (Standard Business Hours).
>
>Morning rush: Strong activity from 7-10 AM
>
>Sustained high activity: 90+ trips consistently from 2-6 PM
>
>Evening decline: Sharp drop after 6 PM as business day ends
>
>Minimal night activity: Very low usage from 7 PM - 6 AM
>
>**Personal Trips (Left Chart)**
>
>Peak Hour: 10-11 AM (11+ trips)
>
>Late morning peak: Maximum activity around 10 AM (weekend/leisure timing)
>
>Sustained daytime activity: Moderate levels throughout afternoon (4-7 trips)
>
>Evening activity: Continues into evening hours (unlike business trips)
>
>Night presence: Some activity even in late evening/night hours
>

### 4. Do business trips get longer during rush hours?
>
>![image](https://github.com/user-attachments/assets/98c0def6-fb0c-4187-b495-d8d3d79e8663)
>
>if we look at the histogram we fined that most trips happen between 8 to 21 and after revewing the box blot
>we see that we hit the peak of rush hour at 9 in the start of the day and then at 16 at the end of the day
>

### 5. Do certain purposes always require long-distance travel?
>
>| Purpose | Average of MILES | PURPOSE frequency | Min of MILES | Max of MILES | StdDev of MILES |
>|---------|------------------|-------------------|--------------|--------------|-----------------|
>| Commute | 180.2 | 1 | 180.2 | 180.2 | #DIV/0! |
>| Customer Visit | 20.7 | 101 | 0.8 | 310.3 | 40.6 |
>| Meeting | 15.3 | 186 | 0.7 | 201.0 | 25.2 |
>| Charity ($) | 15.1 | 1 | 15.1 | 15.1 | #DIV/0! |
>| Between Offices | 10.9 | 18 | 1.9 | 39.2 | 8.5 |
>| Temporary Site | 10.5 | 50 | 1.8 | 48.2 | 7.8 |
>| Meal/Entertain | 5.7 | 160 | 0.6 | 36.5 | 5.0 |
>| Airport/Travel | 5.5 | 3 | 4.1 | 7.6 | 1.9 |
>| Moving | 4.6 | 4 | 3.3 | 6.1 | 1.2 |
>| Errand/Supplies | 4.0 | 128 | 0.5 | 22.3 | 3.5 |
>
>as we can see here in this table **(Meeting, Temporary Site, Customer Visit, between offices)**
>that have high to moderate stdDev and a big deffrence between min and max values
>
>![image](https://github.com/user-attachments/assets/36b6dd88-6c82-4a7c-8fb9-06178f99f1cf)
>
>from that we see that this purposes average is highly influnced by outliers from the histogram we see that they are
>right skewed so for **(Meeting, Temporary Site, Customer Visit)** its better to use median as measure of central tendency
>and for **between offices** its oky to use average but we cant say for sure because we only have 18 record of this purpose
>so after we have more data we can decide for sure



## 🛠️ Tools Used
- Excel, Power Query.
- Power BI.

## 📂 Repository Structure
