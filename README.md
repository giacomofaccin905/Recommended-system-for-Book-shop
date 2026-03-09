# Recommended-system-for-Book-shop
This project aims to build a recommender system for an online book shop. Starting from a couple of keywords, it scores and ranks books by recency, edition count, and Python relevance, returning the most suitable titles to the user.

---

#  Report challenge 1 

Author : Giacomo Faccin
Mat: 892389

--- 

#  Recommender System for a Book Shop

## 1. Data Loading and Initial Exploration

The analysis started by downloading the dataset:

**`Challenge 1 - data_ml_books_openlibrary.csv`**

The dataset was loaded using the **Pandas** library, followed by an initial Exploratory Data Analysis (EDA) to identify:

- Missing values (NaN)
- Inconsistent data
- Potential outliers
- Distribution issues in numerical variables

---

## 2. Handling Missing Values

The following missing values were identified:

- `subjects`: 198  observations present
- `description`: 34  observations present
- `first_publish_year`: 498  observations present

For the feature `first_publish_year`, I applied a domain-based assumption. According to the article *“A Brief History of Data Science”*, the first book explicitly related to Data Science dates back to 1974.  

To avoid unrealistic publication years and incorrect distributions, I replaced missing or inconsistent values with a default year of **1980**.

---

##  Exploratory Data Analysis (EDA)

During the EDA phase, I observed:

- An incorrect distribution of publication years  
- The presence of several outliers  
- Significant skewness in numerical features  

The scatter plot (`scatter_plot_series_2`) clearly showed a concentration of outliers that could negatively impact model performance.

---

##  Outlier and Skewness Treatment

To mitigate the impact of outliers and skewness, I applied:

- `RobustScaler` → to reduce sensitivity to outliers  
- `numpy.log1p(x)` → to stabilize variance and reduce skewness  

After applying these transformations, the distribution became:

- More uniform  
- Better centered  
- More suitable for machine learning modeling  

---

## 5. Feature Engineering

To improve the model’s performance and simplify ranking logic, I created a new feature:

### `Final_Score`

This feature aggregates:

- `first_publish_year`
- `edition_count`

The purpose of this feature was to:

- Improve KNN performance  
- Simplify sorting logic  
- Obtain more meaningful Top-5 recommendations  

---

##  Top 5 Books Based on Final Score

- **Aurélien Géron** | Year: 2019 | Editions: 4  
- **Wei-Meng Lee** | Year: 2019 | Editions: 3  
- **Tanay Agrawal** | Year: 2020 | Editions: 2  
- **Dipayan Sarkar, Vijayalakshmi Natarajan** | Year: 2019 | Editions: 2  
- **Sebastian Raschka** | Year: 2015 | Editions: 4  

---

#  KNN Recommender System for Online Shops


## Model Choice

I implemented a **K-Nearest Neighbors (KNN)** algorithm to build a **content-based recommender system** for an online bookshop.

The model was trained using:

- `first_publish_year`
- `edition_count`
- `Final_Score`

The objective was to recommend books with similar characteristics.

---

## Assumption

I assumed that a user is searching for books related to:

```python
Python
