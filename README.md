# 🚗 Uber Trip Analysis Project

## 📊 Project Overview
This project analyzes Uber ride data to uncover insights into trip durations, distance patterns, timing trends, and usage by purpose. The goal is to identify patterns that can help optimize operations and understand rider behavior.

## 📁 Dataset
- **Records:** Number of trips: **1157**
- **Columns:** START_DATE, END_DATE, CATEGORY, START location, STOP location, MILES, PURPOSE.

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

## ❓ Key Business Questions Answered
1. What’s the average trip duration, and how does it vary by purpose?
2. Are there seasonal patterns in ride frequency or distance?
3. Do certain purposes always require long-distance travel?
4. Do business vs personal trips follow different timing patterns?

## 📈 Analysis & Insights
- Time-based trends in ride frequency and distance
- Trip duration clustering by purpose
- Weekday vs weekend patterns for business and personal trips
- Impact of rush hour on trip length and frequency

## 🛠️ Tools Used
- Excel, Power Query.
- Power BI.

## 📂 Repository Structure
