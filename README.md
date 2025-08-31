# 🏡 House Price Prediction Project  

## 📋 Project Overview  
This project focuses on building a machine learning model to predict house prices based on various property features. The implementation follows a structured approach to data preprocessing, feature engineering, and model selection to create an accurate predictive system.  

---

## 🗂️ Dataset Description  
The dataset contains approximately **15,000 property listings** with the following key features:  

**Core Features:**  
- number of bedrooms, number of bathrooms, number of floors  
- living area, lot area, area of the house (excluding basement), area of the basement  
- waterfront present (binary), number of views, condition of the house, grade of the house  
- Built Year, Renovation Year, Postal Code, Latitude, Longitude  
- Number of schools nearby, Distance from the airport  

**Target variable:**  
- Price  

---

## 🔧 Data Preprocessing & Feature Engineering  

### 1. Date Conversion and Feature Engineering  
- **Challenge:** The `Date` column was stored in Excel serial number format (e.g., 42491).  
- **Solution:** Converted to proper datetime format and extracted meaningful temporal features.  
- **Created:** `House_age = Sale Year – Built Year`.  
- **Rationale:** House age provides more predictive power than raw sale dates.  

### 2. Feature Selection and Removal  
**Removed Features:**  
- `id`: Unique identifier with no predictive value  
- `Date`: Redundant after extracting temporal features  
- `living_area_renov`, `lot_area_renov`: inconsistent values  
- `Renovation Year`: unreliable due to data quality issues  
- `Postal Code`: dropped in favor of continuous geographic coordinates  

**Retained Features:**  
- Original `living area`, `lot area` (higher correlation with price)  
- `Latitude` and `Longitude`: weak individual correlations but allowed model to capture geographic patterns  
- All quality/amenity features with logical connections to house prices  

### 3. Data Quality Assessment  
- Found inconsistencies in renovation-related features.  
- Prioritized reliable features with clear logical connections to price.  
- Addressed categorical vs. continuous feature treatment.  

### 4. Correlation Analysis  
**Strongest correlations with price:**  
- living area: **0.71**  
- grade of the house: **0.67**  
- area (excl. basement): **0.62**  
- number of bathrooms: **0.53**  

**Moderate correlations:**  
- Longitude: **0.30**  
- number of bedrooms: **0.31**  
- lot area: **0.26**  

---

## 🧠 Model Selection Rationale  

**Algorithm Choice:** Random Forest Regressor  

**Why Random Forest?**  
- **Non-linear relationships:** Captures patterns Linear Regression missed (e.g., 2-bed homes more expensive than larger ones).  
- **Feature handling:** Works well with mixed feature types.  
- **Robustness:** Tolerates outliers/noisy data.  
- **Interpretability:** Provides feature importance scores.  

**Comparative Approach:**  
- Linear Regression baseline established first.  
- Random Forest tested against it to quantify improvements.  

---

## 🚀 Model Implementation & Results  

### Data Preprocessing for Modeling  
- StandardScaler applied to normalize numeric features.  
- Train-test split (80-20) applied.  
- Scaling applied separately to train/test to avoid leakage.  

---

### Baseline Model: Linear Regression  

**Performance:**  
- RMSE: ~199,000  
- MAE: ~124,000  
- R²: 0.718  

**Interpretation:**  
- Captured 71.8% of variance but left ~28% unexplained.  
- Struggled with higher-priced homes → large errors.  
- Good benchmark for more complex models.  

---

### Primary Model: Random Forest Regressor  

**Configuration:**  
- `n_estimators=100`  
- `random_state=42`  
- Trained on unscaled data (scale-invariant).  

**Performance:**  
- RMSE: ~132,551 (**34% better than linear**)  
- MAE: ~69,035 (**44% better than linear**)  
- R²: 0.875 (**87.5% variance explained**)  

**Interpretation:**  
- Significantly better predictions across all metrics.  
- Successfully captured non-linear relationships.  
- Geographic splits from latitude/longitude improved predictions.  

---

## 📊 Results Analysis  

### Model Performance Comparison  

| Model             | RMSE     | MAE     | R²     | Improvement          |  
|-------------------|----------|---------|--------|----------------------|  
| Linear Regression | ~199,000 | ~124,000| 0.718  | Baseline             |  
| Random Forest     | ~132,551 | ~69,035 | 0.875  | 34–44% improvement   |  

---

### 🔍 Feature Importance vs Correlation  

- **Living area (0.34 importance):** Highest predictor, consistent with 0.71 correlation.  
- **Grade (0.25):** Second strongest, consistent with 0.67 correlation.  
- **Latitude (0.16):** Weak raw correlation (0.024), but highly predictive → Random Forest found geographic zones.  
- **Longitude (lower than expected):** Despite 0.3 correlation, less predictive than latitude.  
- **House_age:** Engineered feature added real predictive value, validating preprocessing effort.  

**Takeaway:** Random Forest revealed that correlation ≠ predictive power. Some weakly correlated features (latitude) turned out critical once the model could learn splits.  

---

## 📈 Visualizations  
 

### Predicted vs. Actual Prices Scatter Plot  
👉 <img width="1390" height="590" alt="image" src="https://github.com/user-attachments/assets/cb207dac-2856-4fdd-9a89-7b3d55d1b013" />

### Residual Plot  
👉 <img width="1389" height="590" alt="image" src="https://github.com/user-attachments/assets/8fac3369-0ac6-43d6-bf0a-437a75d29075" />


### Feature Importance Bar Chart  
👉 <img width="835" height="718" alt="image" src="https://github.com/user-attachments/assets/77591da6-f43c-4c36-927f-5b9e4709f35e" />


---

## 🎯 Conclusion  

This project demonstrates a full end-to-end ML workflow for house price prediction:  

- Data exploration and preprocessing  
- Thoughtful feature engineering and selection  
- Rigorous baseline vs advanced model comparison  
- Validation of preprocessing choices through feature importance  

✅ Random Forest achieved **87.5% variance explained** and reduced prediction errors by **34–44%** compared to Linear Regression.  

The results highlight:  
- The importance of **non-linear models for real-world data**  
- How **EDA + feature engineering directly influence performance**  
- The value of **interpreting model insights beyond raw accuracy**  
