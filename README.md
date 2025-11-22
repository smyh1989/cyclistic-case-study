# Cyclistic Bike-Share Case Study  
Google Data Analytics Capstone Project · R / tidyverse

## 1. Project Overview

This project is based on the **Google Data Analytics Capstone** and analyzes bike-share usage for a fictional company called **Cyclistic**.  

Cyclistic’s business team wants to **increase annual memberships**, because members provide more stable, long-term revenue. As a junior data analyst, my goal is to:

> Understand how **annual members** and **casual riders** use Cyclistic bikes differently,  
> and provide data-driven recommendations to convert casual riders into members.

I use **12 months of recent trip data (2024–2025)** and perform the full data-analysis process in **R**.

---

## 2. Business Task

- Compare usage patterns between:
  - **`member`** riders (annual members)  
  - **`casual`** riders (single-ride and day passes)
- Identify **when, where, and how** these groups ride differently.
- Provide **actionable marketing recommendations** to encourage casual riders to become annual members.

---

## 3. Data

- Source: Public Divvy / Cyclistic bike-share trip data (2024–2025), 12 monthly CSV files.
- Size: ~**5.6 million rows**, **13 columns** per file.
- Key variables:
  - `ride_id`, `rideable_type`
  - `started_at`, `ended_at`
  - `start_station_name`, `start_station_id`
  - `end_station_name`, `end_station_id`
  - `start_lat`, `start_lng`, `end_lat`, `end_lng`
  - `member_casual` (rider type)

> Note: Raw data files are large and may not be stored directly in this repository.  
> You can download the original data from the Divvy/Cyclistic public data portal.

---

## 4. Tools & Packages

- **Language:** R
- **IDE:** RStudio
- **Packages:**
  - `tidyverse` (data wrangling & visualization)
  - `lubridate` (date/time handling)
  - `knitr` / `rmarkdown` (for reporting)

---

## 5. Data Cleaning & Preparation

Steps performed in R:

1. **Import & combine**  
   - Loaded 12 monthly CSV files from a local folder.  
   - Combined them into a single dataframe (`trips_raw`) using `purrr::map_dfr()`.

2. **Convert date/time columns**  
   - `started_at` and `ended_at` converted to POSIXct using `lubridate::ymd_hms()`.

3. **Create ride length**  
   - `ride_length` = difference between `ended_at` and `started_at` in **minutes**.

4. **Filter out bad data**  
   - Removed negative or zero ride lengths.  
   - Removed trips longer than 24 hours (`ride_length < 1440`) to exclude outliers/unrealistic rides.

5. **Create time-based features**  
   - `day_of_week` (Monday–Sunday)  
   - `month` (January–December)  
   - `hour` (0–23, hour of day ride started)

The cleaned dataset is stored as `trips_clean`.

---

## 6. Analysis

I focused on comparing **member** vs **casual** riders.

### 6.1 Overall usage

- Total trips: ~5.5M  
- **Members** account for the majority of trips (approx. 3.6M).  
- **Casual riders** account for ~2.0M trips.

### 6.2 Ride duration

Summary of ride length:

- **Casual riders**
  - Longer rides on average (≈ 19 minutes)
  - Median ride length ≈ 11–12 minutes
- **Members**
  - Shorter rides on average (≈ 12 minutes)
  - Median ride length ≈ 8–9 minutes

**Interpretation:**  
Members use bikes for shorter, more frequent trips (likely commuting).  
Casual riders take longer, more recreational rides.

### 6.3 Day-of-week patterns

- **Members**:
  - Higher usage on **weekdays** (Monday–Friday).
  - Suggests regular commuting and routine trips.

- **Casual riders**:
  - Clear peaks on **weekends**, especially **Saturday and Sunday**.
  - Suggests leisure, tourism, and social activities.

### 6.4 Time-of-day patterns

- **Members**:
  - Two strong peaks around **morning (7–9am)** and **evening (4–6pm)**.
  - Typical “home ↔ work” commute behavior.

- **Casual riders**:
  - More rides during **midday and afternoon**.
  - Less pronounced commute peaks.

---

## 7. Visualizations

The analysis includes several visualizations (examples):

- **Number of rides by day of week** (member vs casual)
- **Number of rides by hour of day** (member vs casual)
- **Average ride length by day of week**
- **Monthly ride volume trends**

These charts were created with `ggplot2` and exported to the `outputs/` folder.

---

## 8. Key Insights

1. **Members ride more frequently but for shorter durations.**  
   - Strong weekday usage and commute patterns.

2. **Casual riders ride less often but for longer durations.**  
   - Strong weekend usage (Saturday/Sunday), suggesting recreational behavior.

3. **Time-of-day patterns differ clearly.**  
   - Members: Morning and evening peaks.  
   - Casual: Afternoon and weekend peaks.

4. **Seasonality and weather (if explored) can further influence demand**, especially for casual riders in warmer months.

---

## 9. Recommendations

Based on the analysis, Cyclistic can consider the following strategies to convert casual riders into annual members:

1. **Weekend-focused membership campaigns**  
   - Offer limited-time discounts or “weekend pass → membership” upgrades, targeting riders who frequently ride on Saturdays and Sundays.

2. **Target high-usage casual riders**  
   - Identify casual riders with repeated trips and send personalized emails or app notifications showing how a membership would save them money.

3. **Promote memberships at tourist & leisure stations**  
   - Use in-app banners and on-site signage at stations with high casual usage (parks, waterfront, tourist areas).

4. **Offer a 30-day trial membership**  
   - Allow casual riders to experience member benefits with a low-risk trial.

5. **Messaging focused on savings and convenience**  
   - Emphasize that members pay less per ride and can use bikes flexibly for commuting and errands.

---

## 10. Repository Structure

```text
cyclistic-case-study/
├── outputs/
│   └── cyclistic-case-study.html
├── rmd/
│   └── cyclistic-case-study.Rmd
├── .gitignore
├── LICENSE
└── README.md
