# Tech Assessment: Weather Trend Forecasting
---

## 🚀 Project Overview
This repository contains the code and methodology for analyzing the "Global Weather Repository.csv" dataset and forecasting future weather trends. The project demonstrates a complete Data Science lifecycle, covering data cleaning, exploratory data analysis (EDA), and time series forecasting using Linear Regression.

### 🔗 Important Links
* **Google Colab Notebook:** [Google Colab](https://colab.research.google.com/drive/1KAsKtup5fGbGUnv-W3Bse1NOEDyRFF27?usp=sharing)
* **Demo Video:** [Google Drive](https://drive.google.com/file/d/1k4qSg6QFJ9q4y-yiVDg6Bj2AWZVOYE83/view?usp=sharing)
* **Report:** [Google Docs](https://docs.google.com/document/d/1-GFgGvjZZ6vGhCuRzTidr6lPp0tR-Lnj10azr3r4zcs/edit?usp=sharing)

---

## 🧠 What was Done

### 1. Data Cleaning & Preprocessing
* **Outlier Handling:** Instead of blind statistical cuts, physics-based rules were applied to remove catastrophic sensor failures (e.g., temperatures of 79°C, wind speeds over 2900 km/h). Extreme but physically possible events (like heavy rainfall) were preserved.
* **Air Quality:** Negative values were removed, and a 99th-percentile cutoff was applied to handle anomalous pollution spikes.
* **Dimensionality Reduction:** Imperial system columns were dropped to prevent multicollinearity.
* **Normalization:** All continuous numerical variables were scaled using `StandardScaler`.

### 2. Exploratory Data Analysis (EDA)
* Plotted global temporal trends for temperature and precipitation.
* Generated a Pearson correlation heatmap to uncover interactions between variables (e.g., UV Index, Humidity, and Temperature).

### 3. Feature Engineering & Time Series Modeling
* **Temporal Ordering:** The `last_updated` feature was converted to `datetime` to ensure strict chronological ordering and appropriate train/test splitting (80/20) to prevent data leakage.
* **Feature Shift:** Since future data is unavailable during forecasting, the prediction relied on the previous day's data by applying a `shift(1)` operation to all selected variables.

---

## 📊 Results Analysis
To assess feature importance, an ablation study was conducted comparing three model configurations:

1. **Model 1 (Multivariate):** Used `shift(1)` for Temperature, Humidity, UV, and Pressure.
2. **Model 2 (Univariate):** Used only `shift(1)` for Temperature.
3. **Model 3 (Without Temperature):** Attempted to predict temperature using only exogenous variables (Humidity, UV, Pressure).

**Conclusion:** Even when utilizing the exogenous variables with the highest correlation, the model struggled to learn the true underlying weather patterns. The most significant determining factor for accuracy proved to be the previous day's temperature (Model 2 performed almost identically to Model 1, while Model 3 failed completely). 

However, relying heavily on this variable causes the model to fall into a naïve forecasting state, where it simply attempts to output a value close to the previous day's temperature. Future improvements should include a larger, multi-year dataset for historical date comparisons, and the addition of time-based features (day of the year) and location parameters to account for regional climate patterns.

---

## 💻 How to Run This Project

### Google Colab
1. Click the Google Colab link provided in the "Important Links" section above.
2. Upload the `GlobalWeatherRepository.csv` dataset to the Colab session storage.
3. Click `Runtime` > `Run all`.
