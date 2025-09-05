# 🏨 Hotel Booking Cancellations - Data Cleaning & Preprocessing

## 📌 Project Overview
This project is part of **GTC ML Project 1 - Data Cleaning & Preprocessing Challenge**.  
We are provided with raw hotel booking data (`hotel_bookings.csv`) directly from the Property Management System (PMS).  

The **objective** is not to build the final prediction model, but to **prepare a clean, ML-ready dataset** that can be used to train models for predicting hotel booking cancellations.  

---

## 🎯 Business Problem
Last-minute booking cancellations have a significant impact on hotel revenue.  
The revenue team wants to **predict cancellations in advance** to minimize losses.  

Our role here is to ensure that the dataset is **well-cleaned, consistent, and free of data leakage** before modeling.

---

## 📂 Project Phases

### **Phase 1: Exploratory Data Analysis (EDA)**
- Loaded the dataset and checked basic info (`.info()`, `.describe()`).
- Identified missing values and visualized them using **missingno** (heatmap, bar plots).
- Detected outliers in key columns (`adr`, `lead_time`) using **boxplots** and the **IQR method**.
- Documented main data quality issues:
  - Missing values in `agent`, `company`, `country`, `children`.
  - Presence of outliers in `adr` and `lead_time`.
  - Duplicate rows in the dataset.

---

### **Phase 2: Data Cleaning**
- **Missing Values**:
  - `company`, `agent`: replaced with `"None"` or `0`.
  - `country`: filled with mode or `"Unknown"`.
  - `children`: imputed with median.
- **Duplicates**: Removed exact duplicate rows.
- **Outliers**:
  - Capped `adr` values at 1000.
  - Capped `lead_time` values at 500.
- **Data Types**:
  - Converted `reservation_status_date` to datetime.
  - Created a proper `arrival_date` column from year, month, and day.

---

### **Phase 3: Feature Engineering & Preprocessing**
- **New Features**:
  - `total_guests = adults + children + babies`
  - `total_nights = stays_in_weekend_nights + stays_in_week_nights`
  - `is_family = Yes/No` depending on presence of children or babies
- **Encoding Categorical Variables**:
  - One-Hot Encoding for low-cardinality columns (`meal`, `market_segment`, `deposit_type`, etc.).
  - Grouped rare categories in high-cardinality features (`country`, `agent`, `company`) into `"Other"`.
- **Remove Data Leakage**:
  - Dropped `reservation_status` and `reservation_status_date`.
- **Train-Test Split**:
  - Final dataset split into training and testing sets (`test_size=0.2`, `random_state=42`).

---

## 🛠️ Tech Stack
- **Python** (pandas, numpy, matplotlib, seaborn, missingno, scikit-learn)
- **Jupyter Notebook**

---

## 🚀 How to Run
1. Clone the repository or download the notebook.
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn missingno scikit-learn
