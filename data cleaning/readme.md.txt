# 🧹 Data Cleaning – YouTube Trending Videos (INvideos)

## 📌 Project Overview

This project demonstrates complete **data cleaning** on the **INvideos (Trending YouTube Video Statistics)** dataset.
Data cleaning is a crucial step in any analytics workflow. Messy or inconsistent data leads to wrong insights and poor model performance.

This project focuses on transforming a raw dataset into a clean, structured, and analysis-ready format by applying industry-standard data cleaning practices.

---

## 🎯 Objectives

* Ensure **data integrity**
* Handle **missing values**
* Remove **duplicates**
* Perform **standardization & formatting**
* Detect and handle **outliers**
* Convert and fix date formats (important challenge for this dataset)

---

## 📂 Dataset Description

**Dataset Name:** INvideos (Trending YouTube Video Statistics)
**Columns Included:**

* `video_id`
* `trending_date`
* `title`
* `channel_title`
* `category_id`
* `publish_time`
* `tags`
* `views`
* `likes`
* `dislikes`
* `comment_count`
* `thumbnail_link`
* `comments_disabled`
* `ratings_disabled`
* `video_error_or_removed`
* `description`

---

## 🔧 Data Cleaning Steps Performed

### ✔️ 1. Data Integrity Checks

* Verified dataset shape and data types
* Ensured valid numeric columns (`views`, `likes`, `dislikes`, `comment_count`)
* Checked for negative or impossible values
* Ensured uniqueness of `video_id` and removed duplicate entries

---

### ✔️ 2. Handling Missing Data

* Checked missing values using `isnull().sum()`
* Filled missing text fields (`title`, `tags`, `description`) with `"Unknown"`
* Filled missing categorical and boolean fields (`category_id`, `comments_disabled`, etc.)
* Identified invalid or missing `trending_date` entries after conversion
* Converted missing/invalid dates to `NaT` and handled them appropriately

---

### ✔️ 3. Fixing Date Formats

This dataset contains an unusual date format such as:

```
17.14.11  →  Year.Day.Month
```

Steps taken:

* Cleaned whitespace
* Applied correct conversion format:

  ```python
  pd.to_datetime(df['trending_date'], format='%y.%d.%m', errors='coerce')
  ```
* Identified remaining invalid dates (e.g., impossible dates like `18.02.30`)
* Handled NaT values appropriately

---

### ✔️ 4. Duplicate Removal

* Removed exact duplicates using `df.drop_duplicates()`
* Removed duplicate `video_id` entries (keeping the first occurrence)

---

### ✔️ 5. Standardization & Formatting

* Converted text columns (`title`, `channel_title`, `description`) to lowercase
* Trimmed whitespace
* Standardized boolean columns
* Converted `publish_time` into proper datetime and extracted `publish_year`

---

### ✔️ 6. Outlier Detection & Handling

Outliers handled using the **IQR method** for:

* `views`
* `likes`
* `dislikes`
* `comment_count`

Formula used:

```
IQR = Q3 - Q1  
lower = Q1 - 1.5*IQR  
upper = Q3 + 1.5*IQR
```

Extreme values outside the range were removed to reduce skewness.

---

### ✔️ 7. Saving the Cleaned Dataset

Final cleaned dataset saved as:

```
INvideos_cleaned.csv
```

---

## 🧪 Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Jupyter Notebook**

---

## 📘 How to Run

1. Clone the repository
2. Install dependencies
3. Open the Jupyter notebook
4. Run all cells to reproduce the cleaning workflow

---

## 📁 Project Structure

```
├── CleaningData P3L1.ipynb      # Jupyter notebook with full cleaning code
├── INvideos.csv                 # Raw dataset
├── INvideos_cleaned.csv         # Cleaned dataset
└── README.md                    # Project documentation
```

---

## 🚀 Result

A fully cleaned, standardized, and analysis-ready dataset that can be used for:

* Exploratory Data Analysis
* Machine Learning
* Visualization
* Trend analysis
* Feature engineering
