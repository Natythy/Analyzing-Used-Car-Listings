# Analyzing Used Car Listings - eBay Kleinanzeigen Dataset

This project analyzes a dataset of used cars from eBay Kleinanzeigen, the German eBay classifieds site. The goal is to clean the data and explore the factors that affect used car prices.

Dataset source:  
https://www.kaggle.com/datasets/thedevastator/uncovering-factors-that-affect-used-car-prices/data

---

## Project Steps

### 1. Data Loading

- The dataset is loaded using pandas from `autos.csv` (main data) and `autos_dict.csv` (data dictionary).
- The data dictionary provides descriptions for each column.

### 2. Initial Data Inspection

- The code inspects the dataframe's structure, types, and missing values.
- It prints out:
  - The number of columns and their data types.
  - How many columns have null values and the maximum percentage of missing data in any column.
  - A note that some columns store dates as strings.

### 3. Column Renaming

- The columns are renamed for clarity and consistency, matching the data dictionary.

### 4. Dropping Uninformative Columns

- Columns with the same value for almost all rows (`seller`, `offer_type`) and the `num_photos` column (which is always zero) are dropped, as they do not provide useful information for analysis.

### 5. Outlier Detection and Removal (Price)

- Outliers in the `price` column are detected using the Interquartile Range (IQR) method:
  - Calculate Q1 (25th percentile) and Q3 (75th percentile).
  - Compute IQR = Q3 - Q1.
  - Define outliers as values outside [Q1 - 1.5*IQR, Q3 + 1.5*IQR].
- Outliers are removed to create a cleaned dataset for further analysis.
- Box plots are generated before and after outlier removal using Plotly Express.

**Explanation:**  
The IQR method is a robust way to detect outliers, as it is not affected by extreme values. Removing outliers helps prevent skewed analysis and misleading visualizations.

### 6. Date Columns Handling

- Columns containing date information (`date_crawled`, `ad_created`, `last_seen`) are converted from string to pandas datetime objects for easier manipulation and analysis.

**Explanation:**  
Date columns are often stored as strings in raw data. Converting them to datetime allows for time-based filtering, grouping, and plotting.

### 7. Registration Year Cleaning

- The `registration_year` column is checked for implausible values (e.g., years far in the past or future).
- Outliers are detected and removed using the IQR method.
- Additional filtering ensures that `registration_year` does not exceed the year the ad was crawled.

**Explanation:**  
Some entries may have incorrect registration years due to data entry errors. Removing these ensures more accurate analysis of car age and its effect on price.

---

## Notebooks and Code

All analysis steps are documented in `notebook.ipynb`, with code cells and markdown explanations.

---

## Key Techniques Used

- **Pandas** for data manipulation and cleaning.
- **Plotly Express** for data visualization.
- **Outlier detection** using the IQR method.
- **Datetime conversion** for proper handling of date columns.

---

## How to Run

1. Install requirements:  
   `pip install pandas plotly termcolor`
2. Open `notebook.ipynb` in Jupyter or VS Code.
3. Run cells sequentially to reproduce the analysis.

---
## Project Status & Next Steps

**This repository is not finished yet.**

- The data cleaning process will be further refined to handle more edge cases and improve data quality.
- An in-depth analysis section will be added, including exploratory data analysis (EDA), visualizations, and insights into the factors affecting used car prices.

Stay tuned for updates as the project progresses!

---

## Notes

- The project focuses on data cleaning and exploratory analysis.
- Further steps could include feature engineering, modeling, or deeper statistical analysis.
