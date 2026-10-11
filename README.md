# ⚡ Steel Plant Electricity Consumption Analytics & Prediction

An end-to-end Machine Learning and interactive Streamlit analytics platform to analyze, monitor, and predict electrical energy consumption in heavy steel manufacturing operations.

---

## 📌 Overview

Steel manufacturing is an energy-intensive industrial process where electricity costs represent a significant portion of operational expenditure. Fluctuating production volumes, environmental factors (ambient temperature and humidity), and shifting operational schedules directly influence electric power demand.

This project delivers:
1. **Predictive Modeling**: A machine learning regressor (`RandomForestRegressor`) trained to forecast power usage (`Electricity_Consumption_MWh`) based on industrial production output (`Production_Tons`).
2. **Interactive Streamlit Dashboard**: A feature-rich visual workspace enabling energy managers and plant supervisors to filter by shift/year, inspect consumption anomalies, evaluate regression metrics, and backtest forecast accuracy over configurable time horizons.

---

## ✨ Key Features

- **📊 Comprehensive Data Overview**: View and filter historical plant operations data with timezone/datetime-safe formatting.
- **📈 Multi-Variate Trend Exploration**:
  - Longitudinal electricity consumption tracking.
  - Production volume vs. electricity demand correlation.
  - Ambient temperature variations across operating shifts.
- **🎯 Rigorous Model Performance Evaluation**:
  - Evaluation on hold-out test sets.
  - Quantitative metrics: **Mean Absolute Error (MAE)**, **$R^2$ Score**, **Symmetric Mean Absolute Percentage Error (SMAPE)**, **MAE-based Accuracy (%)**, and **Tolerance Accuracy (predictions within $\pm 5\%$)**.
  - Actual vs. Predicted scatter plot with identity reference line.
- **⏱️ Interactive Backtesting & Validation**:
  - Adjustable validation window slider (10 to 60 days).
  - Time-series overlay of actual versus forecasted energy demand.
  - One-click export of predicted vs. actual metrics as CSV (`predicted_vs_actual_energy.csv`).
- **🔄 Shift & Temporal Filtering**: Filter metrics dynamically by shift (*Morning*, *Evening*, *Night*) and specific operating years.

---

## 📂 Project Structure

```text
├── dashboard.py                   # Streamlit web application
├── train.py                       # ML model training and serialization script
├── model.pkl                      # Serialized Random Forest model artifact
├── steel_plant.csv                # Primary historical operational dataset
├── steel_plant_2015_2024.csv      # Extended historical dataset (2015-2024)
├── steel.csv                      # Full operational dataset
├── requirements.txt               # Python package dependencies
├── .gitignore                     # Git exclusion rules
└── README.md                      # Project documentation
```

---

## 📊 Dataset Schema

The dataset records shift-level steel plant metrics with the following attributes:

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `Date` | Date (`YYYY-MM-DD`) | Date of logging |
| `Shift` | String | Operating shift (`Morning`, `Evening`, `Night`) |
| `Temperature_C` | Float | Ambient temperature (°C) |
| `Humidity_%` | Float | Relative humidity percentage |
| `Production_Tons` | Float | Finished steel production output (Metric Tons) |
| `Electricity_Consumption_MWh` | Float | **Target**: Total electric energy consumed (Megawatt-hours) |

---

## 🚀 Getting Started

### 1. Prerequisites

- Python 3.9+ (tested on Python 3.10)
- `pip` package manager

### 2. Clone the Repository

```bash
git clone https://github.com/paraspatil31/steel-plant-energy-consumption.git
cd steel-plant-energy-consumption
```

### 3. Create a Virtual Environment (Optional but Recommended)

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux / macOS
python3 -m venv venv
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 🖥️ Running the Application

### Launch the Streamlit Dashboard

Run the following command in the project root:

```bash
streamlit run dashboard.py
```

Or execute via Python module:

```bash
python -m streamlit run dashboard.py
```

Once running, open your web browser at `http://localhost:8501`. Use the sidebar file uploader to load `steel_plant.csv` and begin exploring.

---

## 🧠 Model Retraining

To retrain the Random Forest model on updated plant production data:

```bash
python train.py
```

The script will:
1. Load `steel_plant.csv`.
2. Clean missing records for production and power consumption.
3. Fit a `RandomForestRegressor(n_estimators=100, random_state=20, n_jobs=-1)`.
4. Serialize and save the refreshed model to `model.pkl`.

---

## 🛠️ Built With

- **[Python](https://www.python.org/)** - Core programming language
- **[Streamlit](https://streamlit.io/)** - Web dashboard framework
- **[Scikit-Learn](https://scikit-learn.org/)** - Machine learning modeling and metrics
- **[Pandas](https://pandas.pydata.org/)** - Data manipulation and time-series handling
- **[Matplotlib](https://matplotlib.org/)** - Scientific plotting and diagnostics

---

## 📄 License

This project is licensed under the MIT License - feel free to use and adapt for academic or commercial purposes.
