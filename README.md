# Household Energy Consumption Prediction

This project develops a machine learning model to **predict household energy consumption**. By analyzing historical usage, we uncover patterns, forecast demand, and generate actionable insights for both consumers and energy providers.

---

## 📌 Business Use Cases

- **Energy Management for Households:** Monitor usage, spot savings opportunities, and build energy-efficient habits to reduce bills.
- **Demand Forecasting for Energy Providers:** Improve load balancing, resource allocation, and dynamic pricing strategies.
- **Anomaly Detection:** Identify irregular patterns indicating faulty appliances, energy theft, or other issues.
- **Smart Grid Integration:** Enable real-time optimization with predictive analytics.
- **Environmental Impact:** Support conservation initiatives and reduce carbon footprints.

---

## 🗄️ Dataset

- **Name:** Individual Household Electric Power Consumption  
- **Source:** UCI Machine Learning Repository  
- **Description:** One household’s electric power measurements sampled **every minute** over **~4 years**.  
- **Features:** `Global_active_power`, `Global_reactive_power`, `Voltage`, `Global_intensity`, `Sub_metering_1`, `Sub_metering_2`, `Sub_metering_3`  
- **Target Variable:** `Global_active_power`

---

## 🧰 Technical Stack

- **Language:** Python  
- **Libraries:**  
  - **Pandas** – data manipulation  
  - **NumPy** – numerical computing  
  - **Scikit-learn** – preprocessing, modeling, evaluation  
  - **Matplotlib & Seaborn** – visualization

---

## 🔁 Project Workflow

### 1) Data Understanding & Exploration (EDA)
- Inspect structure, data types, and quality.
- Identify missing values marked as `?`.
- Resample from **minute** to **hourly** averages to reduce noise and improve compute efficiency.

### 2) Data Preprocessing
- **Datetime Conversion:** Merge `Date` + `Time` → `datetime` index (essential for time series).
- **Handle Missing Values:** Forward fill (`ffill`) to propagate last known observations.
- **Data Types:** Convert feature columns to numeric (`float`) for analysis/modeling.

### 3) Feature Engineering
Create time-based and rolling features to capture cyclical patterns:

- `hour`, `day_of_week`, `month`, `quarter`, `year`  
- `rolling_avg_24h` – 24-hour rolling mean of `Global_active_power`

### 4) Model Selection & Training
- **Temporal split:** 80% train / 20% test, **no shuffling** (preserve order).
- **Models Trained:**
  - Linear Regression (baseline)
  - Random Forest Regressor
  - Gradient Boosting Regressor
  - Neural Network (MLPRegressor)
- **Tuning:** `RandomizedSearchCV` on Random Forest to optimize performance.

---

## 📈 Model Evaluation

Models are evaluated using **RMSE**, **MAE**, and **R²**.  
*(Replace example scores with your actual results.)*

| Model             |   RMSE |   MAE  |   R²   |
|-------------------|-------:|-------:|:------:|
| Linear Regression | 0.3512 | 0.2489 | 0.8123 |
| Random Forest     | 0.1945 | 0.0912 | 0.9421 |
| Gradient Boosting | 0.2103 | 0.1156 | 0.9318 |
| **Tuned RF**      | **0.1899** | **0.0875** | **0.9478** |

---

## 🔍 Feature Importance Analysis

The **Tuned Random Forest** highlighted:
- **Most influential:** `rolling_avg_24h`, `hour`  
- (Add your complete ranking and interpretation.)

*Add plot:* `reports/figures/feature_importance.png`

---

## 📊 Visualization of Predictive Performance

Compare actual vs predicted energy consumption on the test set (tail segment for readability).

*Add plot:* `reports/figures/timeseries_actual_vs_pred.png`

---

## ▶️ How to Run

### 1) Clone the Repository
```bash
git clone https://github.com/your-username/Householdenergy.git
cd Householdenergy

# Create
python -m venv venv

# Activate (Windows)
.\venv\Scripts\activate

# Activate (macOS/Linux)
source venv/bin/activate

pip install -r requirements.txt

Open and run main.ipynb in JupyterLab or your preferred IDE.
(Or replace this with your script commands if you use Python modules/CLIs.)
