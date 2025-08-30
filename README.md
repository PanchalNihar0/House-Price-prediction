# 🏠 House Price Prediction Project

## 📋 Project Overview
This project focuses on building a machine learning model to predict house prices based on various property features. The implementation follows a structured approach to data preprocessing, feature engineering, and model selection to create an accurate predictive system.

---

## 🗂️ Dataset Description
The dataset contains approximately **15,000 property listings** with the following key features:

### Core Features:
- number of bedrooms, number of bathrooms, number of floors  
- living area, lot area, Area of the house (excluding basement), Area of the basement  
- waterfront present (binary), number of views, condition of the house, grade of the house  
- Built Year, Renovation Year, Postal Code, Latitude, Longitude  
- Number of schools nearby, Distance from the airport  

**Target variable:** `Price`

---

## 🔧 Data Preprocessing & Feature Engineering

### 1. Date Conversion and Feature Engineering
- **Challenge:** The Date column was stored in Excel serial number format (e.g., 42491).  
- **Solution:** Converted to proper datetime format and extracted meaningful temporal features.  
- **Created:** `House_age` feature calculated as `Sale Year - Built Year`.  
- **Rationale:** House age provides more predictive power than raw sale dates for price modeling.  

---

### 2. Feature Selection and Removal
**Removed Features:**
- `id`: Unique identifier with no predictive value  
- `Date`: Redundant after extracting temporal features  
- `living_area_renov`, `lot_area_renov`: Removed due to data inconsistency issues where these values differed from original measurements even for non-renovated properties  
- `Renovation Year`: Dropped as the renovation status was already questionable based on area measurement inconsistencies  
- `Postal Code`: Initially considered but ultimately removed in favor of continuous geographic coordinates  

**Retained Features:**
- Maintained original area measurements (`living area`, `lot area`) due to their stronger correlation with price (0.71 and 0.26 respectively)  
- Kept Latitude and Longitude as continuous features despite individual weak correlations, allowing the model to discover geographic patterns through threshold splits  
- Preserved all quality and amenity features with logical connections to house prices  

---

### 3. Data Quality Assessment
- Discovered significant data inconsistencies where renovation-related columns showed different values from original measurements even for properties marked as non-renovated  
- Made intentional decisions to prioritize features with clearer data integrity and stronger logical connections to house prices  
- Addressed the categorical nature of certain features while maintaining their predictive integrity  

---

### 4. Correlation Analysis
**Strongest Correlations with Price:**
- `living area`: **0.71**  
- `grade of the house`: **0.67**  
- `Area of the house (excluding basement)`: **0.62**  
- `number of bathrooms`: **0.53**  

**Moderate Correlations:**
- `Longitude`: **0.3**  
- `number of bedrooms`: **0.31**  
- `lot area`: **0.26**  

---

## 🧠 Model Selection Rationale

### Algorithm Choice: **Random Forest Regressor**
**Reasons for Selection:**
- **Non-linear relationships:** Initial EDA revealed non-linear patterns (e.g., 2-bedroom houses sometimes priced higher than larger properties)  
- **Feature handling:** Effectively manages mixed feature types (numeric, categorical) without requiring extensive preprocessing  
- **Robustness:** Handles outliers and noisy data well compared to more sensitive algorithms  
- **Interpretability:** Provides feature importance scores for model explanation  

**Comparative Approach:**
- Establish a **Linear Regression baseline** to quantify the improvement from Random Forest's non-linear modeling capabilities  
- Linear Regression results will provide a performance benchmark despite its limitations with complex relationships  

---

## 📊 Next Steps

**Immediate Implementation:**
- Train-Test Split: **80-20 split** with consistent random state for reproducibility  
- Baseline Model: Linear Regression with proper feature scaling  
- Primary Model: Random Forest Regressor with default parameters initially  
- Performance Metrics: **RMSE, MAE, and R²** for comprehensive evaluation  

**Future Considerations:**
- Hyperparameter tuning for Random Forest optimization  
- Potential feature engineering experiments  
- Model interpretation using SHAP values or feature importance analysis  
- Deployment considerations for practical application  

---

## 🎯 Project Goals
- Build a robust house price prediction model demonstrating practical ML skills  
- Showcase thoughtful feature engineering and data preprocessing decisions  
- Create a portfolio piece that highlights both technical implementation and strategic decision-making  
- Establish a foundation for potential model deployment and further refinement  

---

This project demonstrates a **methodical approach** to solving real-world machine learning problems, emphasizing:
- Data quality assessment  
- Appropriate algorithm selection  
- Practical implementation strategies  
