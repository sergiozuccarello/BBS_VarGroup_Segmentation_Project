# 🛒 Retail Customer Segmentation: An Interpretability-First Approach

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data_Manipulation-150458.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit_Learn-Machine_Learning-F7931E.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

## 🎓 Academic & Corporate Context
This project was developed as part of the **Machine Learning** course at **Bologna Business School (BBS)**, under the guidance and conception of **Prof. Claudio Sartori**. 

The business challenge and dataset were provided in collaboration with **Var Group**, focusing on a real-world CRM challenge for a leading international food retailer active in the Italian territory.

## 📌 Summary
The primary goal was to evolve the retailer's marketing strategy from "mass communication" to **hyper-personalized targeting** by identifying distinct behavioral customer segments.

To ensure the resulting clusters were 100% transparent and actionable for the Marketing department, our team explicitly bypassed Dimensionality Reduction (PCA). This **Interpretability-First** approach guaranteed that every segment is defined by tangible, real-world metrics rather than abstract mathematical components.

## 🎯 Business Objectives
* Segment a customer base of ~25,000 users based on a 2-year transactional history (>2 million rows).
* Engineer behavioral features that capture psychological purchasing drivers.
* Deliver distinct, easily interpretable personas ready for CRM campaign deployment.

## 🧬 Feature Engineering (The "Customer DNA")
To move beyond standard RFM (Recency, Frequency, Monetary) metrics, we engineered 12 custom behavioral pillars, including:
1. **Discount Sensitivity:** The ratio of promotional spend vs. total spend (`1 - Net/Gross`), successfully isolating "Cherry Pickers" and promo-driven users.
2. **The Digital Divide (Card Usage Rate):** Tracking the fraction of digital/card payments to identify tech-savvy shoppers suitable for app-based marketing.
3. **Loyalty Dynamics:** Analyzing the relationship between `AVG_PTS_EARNED` and `REDEMPTION_FREQ` to separate passive point-collectors from active brand fans.
4. **Customer Tenure:** Calculating days since registration to distinguish between new standard shoppers and historical brand traditionalists.
5. **Category Diversity:** A proxy for "Wallet Share," tracking the breadth of departments a customer shops in.

## ⚙️ Data Preprocessing Pipeline
To calculate robust Euclidean distances in a 12-dimensional space without PCA, strict preprocessing was required to prevent spatial distortion and data leakage:
* **Multicollinearity Handling:** `MONETARY` was dropped from the training features (due to high correlation with Frequency and Avg Basket) to prevent double-counting wealth.
* **Extreme Outlier Isolation:** The top 0.1% of customers (B2B profiles/system anomalies) were isolated based on `AVG_BASKET_GROSS` and `RETURN_RATE` prior to scaling.
* **Long-Tail Compression:** Applied 99th-percentile soft-capping and `log1p` transformations to highly skewed volumetric features.
* **Feature Scaling:** `MinMaxScaler` applied to normalize all dimensions equally between 0 and 1.

## 🤖 Model Evaluation & Selection
Multiple algorithms were tested to find the optimal mathematical and business fit:
* **DBSCAN:** Failed due to continuous density in retail behavior, collapsing 97.7% of users into a single cluster.
* **Gaussian Mixture Model (GMM):** Suffered from the curse of dimensionality in the unreduced 12D space (Silhouette: 0.09).
* **K-Means (Winner):** Maintained strong cluster cohesion (Silhouette: ~0.29) and actionable boundaries. The Elbow Method and business logic dictated **k=4**.

## 📊 Results: The 4 Strategic Personas
The model successfully grouped the customer base into four highly actionable profiles:
1. 📱 **Digital VIPs (26.0%):** The high-spending, tech-savvy engine. Shop across all categories, 90%+ card usage.
2. 🏛️ **Historical Traditionalists (29.0%):** The bedrock of the brand. 15+ years tenure, high frequency, highly reliant on cash.
3. 🛒 **Recent Regulars (27.0%):** The standard shopper with strong growth and up-selling potential.
4. 🏷️ **At-Risk / Promo-Driven (18.0%):** High discount sensitivity. Customers who drift away without heavy promotional triggers.

## 🚀 Next Steps for the Business
* Deploy targeted digital coupons exclusively to the **Promo-Driven** segment to optimize ROI.
* Push App-download campaigns strictly to the **Digital VIPs** and tech-savvy segments.
* Design "basket-building" gamification strategies for the **Recent Regulars**.

## 📁 Repository Structure
* `notebooks/`: Contains the main Jupyter Notebook with the full EDA, Preprocessing, and Clustering pipeline.
* `data/`: (Data omitted for privacy/NDA reasons).
* `presentation/`: Contains the PDF slide deck summarizing the project for Var Group stakeholders.

---
### 👨‍💻 Project Team
* [Sergio Zuccarello]
* [Ali Oshakbayev]
* [Ani Llanaj]
* [Aziz Rouached]
* [Tin Asavasapphavat]
