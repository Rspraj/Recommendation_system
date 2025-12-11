📦 Customer Segmentation & Product Recommendation System

A machine-learning pipeline that segments customers and generates personalized product recommendations using transaction data.

📌 Project Overview

This project performs customer segmentation using transactional purchase behavior and then generates personalized product recommendations for each customer based on cluster-level purchasing patterns.

The workflow consists of:

Data Cleaning & Preparation

Outlier Detection (Isolation Forest)

Feature Standardization

Dimensionality Reduction (PCA)

Customer Segmentation via KMeans

Cluster Profiling & Visualization

Product Recommendation Engine — identifying top items purchased in each cluster

Final Output:
A dataset with CustomerID + Cluster Assignment + Top-3 Recommended Products

🗂 Dataset Description

The dataset includes standard retail transaction variables:

Variable	Description
InvoiceNo	Unique transaction code (prefix “C” indicates a cancellation)
StockCode	Unique product identifier
Description	Product name
Quantity	Number of units purchased
InvoiceDate	Timestamp of transaction
UnitPrice	Price per unit (GBP)
CustomerID	Unique customer identifier
Country	Customer location
🧠 Methodology
1. Data Cleaning

Removed nulls, duplicates

Normalized data types

Handled missing CustomerID

Cleaned product descriptions

2. Outlier Detection

Used Isolation Forest to identify abnormal customers (e.g., extremely high purchase counts).

iso = IsolationForest(...)
iso.fit(customer_data)
outliers = iso.predict(customer_data)


Outlier customers were removed before segmentation to avoid skewing clusters.

3. Data Scaling

All numeric features were standardized using:

scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_customer_features)

4. Dimensionality Reduction (PCA)

Reduced features to 3 principal components for:

Visualization

Enhanced clustering performance

Noise reduction

5. Customer Segmentation (KMeans)

Used KMeans with evaluation metrics:

Elbow Method

Silhouette Score

Calinski–Harabasz Score

Clusters were then visually examined in 2D and 3D (Plotly & Matplotlib).

6. Cluster Profiling

For each cluster:

Purchase behavior analyzed

Distribution of transaction features plotted

Most frequently purchased items identified

This provides insight into each segment’s buying patterns.

7. Product Recommendation System

For each customer:

Identify their assigned cluster

Retrieve top 3 most popular products in that cluster

Assign them as personalized recommendations

Example output columns:

Rec1_StockCode, Rec1_Description

Rec2_StockCode, Rec2_Description

Rec3_StockCode, Rec3_Description

📊 Visualizations Included

PCA scatter plots (2D & 3D)

Cluster distribution plots

Feature histograms segmented by cluster

Outlier distribution

Top product frequency charts

📁 Project Structure
├── Recommendation.ipynb     # Main notebook
├── README.md                # Documentation (this file)
└── data/
      └── transactions.csv   # Input dataset 

📦 Installation & Requirements
Install requirements
pip install numpy pandas seaborn matplotlib plotly scikit-learn yellowbrick


Or using Conda:

conda install numpy pandas seaborn matplotlib scikit-learn

▶️ How to Run

Open the notebook:

jupyter notebook Recommendation.ipynb


Run all cells sequentially

Final output will be a dataframe:

CustomerID | cluster | Rec1 | Rec2 | Rec3

📌 Key Features Summary
Feature	Description
Cluster-based recommendations	Products recommended from top-purchased items in the customer's cluster
Robust outlier removal	Ensures cleaner segmentation
Explainable segmentation	PCA and visual charts allow business interpretability
Production-ready pipeline	Can be easily converted to scheduled batch processing
🚀 
