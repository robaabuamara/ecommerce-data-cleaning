<img width="704" height="393" alt="gross_sales_after png" src="https://github.com/user-attachments/assets/f7f68290-6ed6-496c-a334-18af7969d1ac" /># E-Commerce Data Cleaning & Preprocessing

This project applies practical data cleaning and preprocessing techniques to an e-commerce dataset using Python and Pandas.

The goal was not only to remove missing values, but to understand **why the data was missing**, determine whether those missing values were valid, and prepare the dataset for further analysis or machine learning.

## Dataset

The project uses the **E-Commerce Sales & Customer Analytics** dataset from Kaggle.
**Dataset Source:** [E-Commerce Sales & Customer Analytics on Kaggle](https://www.kaggle.com/datasets/datascikhan/e-commerce-sales-and-customer-analytics)

The original dataset contains:

* **138,116 rows**
* **46 original columns**
* Customer information
* Order and delivery details
* Payment information
* Marketing data
* Sales and profit metrics
* Customer reviews and ratings

A cleaned sample of 1,000 rows is included in this repository as `sample_ecommerce_data.csv`.

The full original dataset is not included because of its large file size.

**Dataset Source:** Add the original Kaggle dataset link here.

## Data Cleaning Steps

### 1. Initial Data Inspection

The dataset was first explored using `head()`, `shape`, `columns`, `info()`, and duplicate checks.

The dataset contained:

* **138,116 records**
* **0 fully duplicated rows**

### 2. Missing Values Analysis

Missing values were analyzed based on the meaning of each feature rather than being removed automatically.

| Column | Missing Values | Percentage |
|---|---:|---:|
| return_status | 128,654 | 93.15% |
| return_reason | 128,654 | 93.15% |
| coupon_code | 110,502 | 80.01% |
| campaign_name | 83,233 | 60.26% |
| delivery_days | 24,557 | 17.78% |
| estimated_delivery_days | 24,557 | 17.78% |
| customer_rating | 24,557 | 17.78% |
| customer_review | 24,557 | 17.78% |
| review_sentiment | 24,557 | 17.78% |

The following changes were made:

* Missing `return_status` values were replaced with **"Not Returned"**
* Missing `return_reason` values were replaced with **"Not Applicable"**
* Missing `coupon_code` values were replaced with **"No Coupon"**
* Missing `campaign_name` values were replaced with **"Unknown Campaign"**

The remaining missing values in `delivery_days`, `estimated_delivery_days`, `customer_rating`, `customer_review`, and `review_sentiment` were intentionally kept as `NaN` because they corresponded to cancelled deliveries where these values did not logically exist.

### 3. Date and Time Parsing

The `order_date` column was converted from an `object` data type to `datetime64[ns]`.

The `order_time` column was also parsed into time values.

This makes it easier to perform future analysis based on year, month, day, or time.

### 4. Text Consistency Checks

Several categorical columns were inspected using `value_counts()`, `unique()`, and temporary lowercase and whitespace normalization with `.str.lower()` and `.str.strip()` to detect inconsistent entries.

Columns checked included:

- `order_status`
- `gender`
- `payment_method`
- `customer_country`
- `customer_city`
- `customer_state`
- `sales_channel`
- `customer_segment`

No major inconsistencies in capitalization, spacing, or category naming were found.

### 5. Numerical Data Validation

Numerical columns such as `customer_age`, `quantity`, and `gross_sales` were checked for unrealistic or invalid values.

The values were found to be within reasonable ranges.

### 6. Gross Sales Normalization

The original `gross_sales` distribution was positively skewed.

A **Box-Cox transformation** was applied to make the distribution more symmetric.

The original `gross_sales` column was preserved, while the transformed values were stored in a new column called `gross_sales_normalized`.

**Skewness before transformation:** `1.91`  
**Skewness after transformation:** `-0.03`

#### Distribution Before Transformation

![Gross Sales Before Box-Cox](gross_sales_before.png)

#### Distribution After Box-Cox Transformation

![Gross Sales After Box-Cox](gross_sales_after.png)
### 7. Feature Scaling

Min-Max Scaling was applied to:

* `customer_age`
* `customer_lifetime_value`

The scaled values were stored in:

* `customer_age_scaled`
* `customer_lifetime_value_scaled`

Both features were transformed to a range between **0 and 1** while preserving the original values.

## Final Dataset

After preprocessing, the dataset contained:

* **138,116 rows**
* **49 columns**
* **0 duplicate rows**

The final cleaned dataset was saved as `ecommerce_cleaned.csv`.

The full cleaned file is not included in this repository because of its size.

## Repository Structure

ecommerce-data-cleaning/
├── README.md
├── e-commerce-dataset-cleaning.ipynb
└── sample_ecommerce_data.csv

## Technologies Used

* Python
* Pandas
* NumPy
* SciPy
* Scikit-learn
* Matplotlib
* Kaggle Notebooks

## Key Learning Outcomes

This project helped me practice and better understand:

* Missing value analysis
* Data type conversion
* Date parsing
* Text consistency checking
* Numerical data validation
* Distribution analysis
* Box-Cox normalization
* Min-Max scaling
* Final data quality validation

One of the main lessons from this project was that data cleaning is not simply about removing missing values. It is important to understand the meaning and context of the data before deciding how each issue should be handled.

## How to Run

1. Clone or download this repository.
2. Download the original dataset from Kaggle using the dataset link above.
3. Open `e-commerce-dataset-cleaning.ipynb`.
4. Update the dataset path if needed.
5. Run the notebook cells in order.

## Possible Next Steps

- Perform exploratory data analysis on the cleaned dataset
- Analyze sales trends over time
- Explore customer segmentation
- Build machine learning models using the prepared features
  
## Project Background

This project was created as a practical follow-up to the **Kaggle Data Cleaning course**, with the goal of applying the concepts learned in the course to a larger e-commerce dataset.
