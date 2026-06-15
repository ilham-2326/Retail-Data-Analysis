# Retail-Data-Analysis
# E-commerce Sales Data — Cleaning & Analysis

##  Project Overview
This project focuses on building an end-to-end data cleaning and exploratory data analysis (EDA) pipeline for a messy, real-world e-commerce sales dataset. Starting with an initial set of 103 orders containing formatting errors, missing fields, typos, and negative entries, a rigorous 10-step data cleaning workflow was applied to establish a single source of truth. Following data validation, the clean dataset was analyzed to extract key business metrics, visualize trends, and provide actionable operational recommendations.

##  Dataset Profile
* **Raw Data Size:** 103 orders (with columns for Order ID, Product, Category, Quantity, Price, Payment Method, Order Date, and Status)
* **Cleaned Data Output:** Saved as `cleaned_ecommerce_data.csv`

---

##  Data Cleaning Pipeline (10 Steps)

To guarantee the integrity of the downstream analysis, the dataset was subjected to the following programmatic cleaning steps:

1. **Drop Rows with Missing Targets:** Removed rows where `Total` revenue was missing, reducing the initial dataset to 89 high-integrity records.
2. **Column Name Sanitization:** Trimmed leading and trailing whitespaces from column headers to prevent `KeyError` bugs.
3. **Missing Category Imputation:** Filled missing `Category` values with a standardized `"UNKNOWN"` placeholder to preserve valid transaction details.
4. **Text Formats Standardization:** Applied uppercase casting and whitespace stripping (`.str.upper().str.strip()`) to string columns (`Category`, `Product`, `Payment_Method`, `Status`) to consolidate duplicate categorical entries.
5. **Data Type Correction:** Cast numerical elements (`Price`, `Quantity`, `Total`) from raw text `object` representations to numerical `float` types.
6. **Mathematical Consistency Verification:** Programmatically recalculated the revenue field to guarantee that:
   $$\text{Total} = \text{Quantity} \times \text{Price}$$
7. **Temporal Parsing:** Converted the mixed-format `Order_Date` column into a standardized `datetime64` format.
8. **Deduplication:** Identified and eliminated duplicate entries based on unique `Order_ID` keys.
9. **Anomalous Values Correction:** Detected negative entries in the `Quantity` column resulting from data entry errors and converted them using absolute values ($|\text{Quantity}|$).
10. **Categorical & Product Alignment:** Corrected structural category typos (e.g., aligning `ELECTRONIC` to `ELECTRONICS`) and reassigned misclassified items (e.g., placing `HEADPHONES` and `BLENDER` into their accurate categories) via an explicit product-to-category mapping dictionary.

---

## 🔍 Exploratory Data Analysis & Visualizations

The Jupyter Notebook produces 8 detailed visualizations built with a clean, unified, minimal aesthetic theme:

1. **Category Distribution:** Bar chart showing order frequencies across categories. *Electronics* and *Books* share the lead for the highest number of transactions.
2. **Revenue by Category:** Analysis of revenue distribution. *Electronics* generates the highest overall revenue, signaling a higher Average Order Value (AOV).
3. **Monthly Sales Trend:** Line plot mapping temporal revenue shifts. Sales peak dramatically in **February** and hit a seasonal trough in **April**.
4. **Payment Method Usage:** Pie chart indicating customer transaction choices. *Cash on Delivery (COD)* emerges as the dominant choice.
5. **Order Status Breakdown:** Frequency plot assessing fullfills, cancellations, and returns.
6. **Top Selling Products:** Horizontal bar chart measuring unit volume. *Science Fiction Books* and *Blenders* are the highest-volume products.
7. **Revenue vs. Revenue Lost to Returns:** Bar graph highlighting a significant portion of potential revenue (~$\$38,000$) lost to returned orders.
8. **Distribution of Order Values:** Histogram plotting transaction frequencies across price ranges to capture skewness and locate outliers, complete with mean and median indicators.

---

##  Key Insights & Business Recommendations

| # | Actionable Insight | Strategic Recommendation |
|---|---|---|
| **1** | **Electronics** leads total revenue despite having an identical order count to Books. | **Prioritize High-Margin Stock:** Allocate greater marketing spend and inventory space to Electronics due to its superior revenue per order. |
| **2** | **Cash on Delivery (COD)** stands as the most heavily utilized payment method. | **Mitigate Delivery Risks:** Optimize COD fulfillment logistics and introduce incentives (e.g., small discounts or loyalty points) to transition users toward prepaid options. |
| **3** | **Return Rates** are remarkably high, resulting in a loss of ~$\$38,000$ in gross revenue. | **Quality Control & Clearer Descriptions:** Conduct product audits on heavily returned items and improve sizing guides/product descriptions to align customer expectations. |
| **4** | Revenue shows significant seasonality, peaking in **February** and dropping in **April**. | **Seasonal Campaigns:** Plan aggressive marketing campaigns and inventory clearance sales in April, while ensuring stock depth ahead of February. |
| **5** | **Science Fiction Books** and **Blenders** move the largest physical volume of units. | **Cross-Selling & Bundling:** Design promotional bundles linking high-volume items with slower-moving or higher-margin accessories. |
| **6** | **Clothing** underperforms across both total transaction volume and revenue metrics. | **Assortment Review:** Audit the clothing department's pricing models, style variations, and target marketing strategies to address underperformance. |

---

##  Getting Started

### Prerequisites
Ensure you have Python installed along with the required core data science libraries:
```bash
pip install pandas numpy matplotlib
