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
    >after revwing the average and stdDev the data is speread and the avgerage might be influnced by outlier
   > spectialy **(Meeting, Customer Visit, Temporary Site)** and we can ignore **(Charity($) , Commute)** because it only has one record , and **"NULL"** recordes because it might be any other purpose
   > and **"moving"** doesnt have any deffrence between average and median
   >
   > ![purpose trip duration distribution](https://github.com/user-attachments/assets/47efe038-bff5-442e-833a-4e8cbb7a9aef)
   >
   > so acording to this box plots for each purpose we needed to investigate its better go use median as measure of central tendency
   > 
   > **in conclution** : yes the average vary by purpose

### 2. Are there seasonal patterns in ride frequency?
   >![trip freq](https://github.com/user-attachments/assets/12e0055d-ac84-4b91-931d-f53d3cbdddab)
   >
   >This line chart displays monthly Uber trip counts categorized by purpose (Business and Personal) throughout a 12-month period
   >Business trips showed early strength with February peak (~100 rides) Gradual decline through March as personal trips slightly increased
   >April-May: Stable period with consistent low-moderate activity
   >June-August: Business trips incressed, reaching annual peak in August while personal trips increased like what happened in Feb-Mar
   >September 70% drop in business trips (130 → 40)
   >Q4 Sustained growth from October through December reached highest point of entire year (145 rides)

## 🛠️ Tools Used
- Excel, Power Query.
- Power BI.

## 📂 Repository Structure
