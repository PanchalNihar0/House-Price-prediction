# House Price Prediction Project

📋 **Project Overview**  
This project focuses on building a machine learning model to predict house prices based on various property features. The implementation follows a structured approach to data preprocessing, feature engineering, and model selection to create an accurate predictive system.

---

## 🗂️ Dataset Description
The dataset contains approximately 15,000 property listings with the following key features:

**Core Features:**
- number of bedrooms, number of bathrooms, number of floors
- living area, lot area, Area of the house (excluding basement), Area of the basement
- waterfront present (binary), number of views, condition of the house, grade of the house
- Built Year, Renovation Year, Postal Code, Latitude, Longitude
- Number of schools nearby, Distance from the airport

**Target variable:** Price

---

## 🔧 Data Preprocessing & Feature Engineering

### 1. Date Conversion and Feature Engineering
**Challenge:** The Date column was stored in Excel serial number format (e.g., 42491)  
**Solution:** Converted to proper datetime format and extracted meaningful temporal features  
**Created:** `House_age` feature calculated as Sale Year minus Built Year  
**Rationale:** House age provides more predictive power than raw sale dates for price modeling

### 2. Feature Selection and Removal
**Removed Features:**
- `id`: Unique identifier with no predictive value
- `Date`: Redundant after extracting temporal features
- `living_area_renov`, `lot_area_renov`: Removed due to data inconsistency issues where these values differed from original measurements even for non-renovated properties
- `Renovation Year`: Dropped as the renovation status was already questionable based on area measurement inconsistencies
- `Postal Code`: Initially considered but ultimately removed in favor of continuous geographic coordinates

**Retained Features:**
- Maintained original area measurements (living area, lot area) due to their stronger correlation with price (0.71 and 0.26 respectively)
- Kept Latitude and Longitude as continuous features despite individual weak correlations, allowing the model to discover geographic patterns through threshold splits
- Preserved all quality and amenity features with logical connections to house prices

### 3. Data Quality Assessment
- Discovered significant data inconsistencies where renovation-related columns showed different values from original measurements even for properties marked as non-renovated
- Made intentional decisions to prioritize features with clearer data integrity and stronger logical connections to house prices
- Addressed the categorical nature of certain features while maintaining their predictive integrity

### 4. Correlation Analysis
**Strongest Correlations with Price:**
- living area: 0.71
- grade of the house: 0.67
- Area of the house (excluding basement): 0.62
- number of bathrooms: 0.53

**Moderate Correlations:**
- Longitude: 0.3
- number of bedrooms: 0.31
- lot area: 0.26

---

## 🧠 Model Selection Rationale
**Algorithm Choice:** Random Forest Regressor  

**Reasons for Selection:**
- Non-linear relationships: Initial EDA revealed non-linear patterns (e.g., 2-bedroom houses sometimes priced higher than larger properties)
- Feature handling: Effectively manages mixed feature types (numeric, categorical) without requiring extensive preprocessing
- Robustness: Handles outliers and noisy data well compared to more sensitive algorithms
- Interpretability: Provides feature importance scores for model explanation

**Comparative Approach:**
- Will establish a Linear Regression baseline to quantify the improvement from Random Forest's non-linear modeling capabilities
- Linear Regression results will provide a performance benchmark despite its limitations with complex relationships

---

## 🚀 Model Implementation & Results

### Data Preprocessing for Modeling
- Applied `StandardScaler` to normalize all numeric features
- Implemented proper train-test split (80-20) to prevent data leakage
- Scaled training and test data separately to maintain data integrity

### Baseline Model: Linear Regression
**Performance Metrics:**
- RMSE: ~199,000 (average prediction error magnitude)  
- MAE: ~124,000 (typical error magnitude)  
- R²: 0.718 (71.8% of variance explained)  

**Interpretation:**
- The linear model captured a decent portion of the signal but left ~28% of variance unexplained
- The discrepancy between RMSE and MAE indicated presence of larger prediction errors
- Established a solid baseline for comparison with more sophisticated models

### Primary Model: Random Forest Regressor
**Configuration:**
- n_estimators: 100
- random_state: 42 for reproducibility
- Trained on unscaled data (tree-based models are scale-invariant)

**Performance Metrics:**
- RMSE: ~132,551 (34% improvement over linear regression)  
- MAE: ~69,035 (44% improvement over linear regression)  
- R²: 0.875 (87.5% of variance explained)

**Interpretation:**
- Significant improvement across all metrics demonstrates Random Forest's ability to capture non-linear relationships
- The model explains 87.5% of price variance, indicating strong predictive power
- Geographic patterns from latitude/longitude coordinates were effectively captured through the algorithm's threshold splitting capability

---

## 📊 Results Analysis

**Model Performance Comparison**

| Model             | RMSE       | MAE       | R²    | Improvement             |
|------------------|-----------|-----------|-------|-------------------------|
| Linear Regression | ~199,000  | ~124,000  | 0.718 | Baseline               |
| Random Forest     | ~132,551  | ~69,035   | 0.875 | 34-44% improvement     |

**Key Insights:**
- Non-linear Pattern Capture: Random Forest successfully modeled complex relationships that Linear Regression could not capture
- Geographic Intelligence: The algorithm discovered meaningful spatial patterns from coordinate data despite weak individual correlations
- Error Reduction: Substantial decrease in both average and typical prediction errors
- Variance Explanation: 87.5% of price variability accounted for by the model

---

## 🔮 Next Steps & Future Enhancements

**Immediate Next Steps:**
- Hyperparameter tuning for Random Forest optimization
- Feature importance analysis to identify most predictive variables
- Model interpretation using SHAP values for explainable AI

**Potential Improvements:**
- Experiment with Gradient Boosting algorithms (XGBoost, LightGBM)
- Additional feature engineering based on domain knowledge
- Geographic clustering to enhance location-based pricing patterns
- Outlier detection and handling refinement

**Deployment Considerations:**
- Model serialization for production use
- API development for real-time price predictions
- Integration with property listing platforms
- Continuous model monitoring and retraining pipeline

---

## 🎯 Conclusion
This project successfully demonstrates a comprehensive approach to house price prediction, from data exploration and preprocessing to model selection and evaluation. The Random Forest algorithm significantly outperformed the linear baseline, achieving 87.5% variance explanation with substantially reduced prediction errors.

The implementation highlights the importance of:
- Thorough data quality assessment
- Thoughtful feature selection and engineering
- Appropriate algorithm selection based on data characteristics
- Rigorous model evaluation and comparison

<img width="1390" height="590" alt="image" src="https://github.com/user-attachments/assets/963e1b19-5f16-4551-8b57-851eb27b8641" />
