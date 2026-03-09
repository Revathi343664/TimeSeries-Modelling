Time Series Forecasting Using ARIMA, LSTM, and GRU Models


Project Overview

This project compares **three time series forecasting models — ARIMA, LSTM, and GRU —** on two financial datasets to evaluate their forecasting performance.

The goal is to understand how **traditional statistical models** and **deep learning models** perform on different types of time series data. The models were evaluated using multiple performance metrics to determine which approach is most suitable for each dataset.

---

Datasets Used

1. Johnson & Johnson Sales (jj.csv)

* Quarterly earnings data from **1960 to 1980**
* Displays **long-term upward trend and seasonality**

2. Amazon Stock Prices (amzn.csv)

* Daily closing stock prices from **2018 to 2023**
* Shows **high volatility and market fluctuations**

---

Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib & Seaborn
* Statsmodels
* TensorFlow / Keras
* Scikit-learn
* pmdarima (Auto ARIMA)
* SciPy

---

Methodology

1. Exploratory Data Analysis (EDA)

EDA was performed to understand the characteristics of both datasets.

Johnson & Johnson Dataset

* Clear **upward trend with seasonality**
* No missing values or major outliers

Amazon Dataset

* Rapid price growth between **2020–2021**
* High volatility afterward
* No missing values detected

---

Data Stationarity Testing

Time series models require stationary data.

Johnson & Johnson Dataset

Initial ADF Test:

ADF Statistic: **2.742**
p-value: **1.0**

This confirmed **non-stationarity**.

To correct this:

* **Box-Cox Transformation** (λ = 0.0507)
* **First-order differencing**

After transformation:

ADF Statistic: **-4.3814**
p-value: **0.00032**

The data became **stationary**.

---

Amazon Dataset

Initial ADF Test:

ADF Statistic: **-1.6578**
p-value: **0.453**

Steps applied:

* **First-order differencing**
* **Box-Cox Transformation (λ = -0.369)**

Final ADF Test:

ADF Statistic: **-13.8296**
p-value: **7.63e-26**

The dataset achieved **stationarity**.

---

ARIMA Model Selection

Johnson & Johnson Dataset

| Method             | Best Parameters |
| ------------------ | --------------- |
| Manual Grid Search | ARIMA(4,1,3)    |
| Auto ARIMA         | ARIMA(1,1,3)    |

Final Model:

**ARIMA(4,1,3)**

Model Statistics:

* AIC: -137.53
* BIC: -118.18

Residual diagnostics confirmed:

* Random residuals
* Normal distribution
* No autocorrelation

---

Amazon Dataset

| Method             | Best Parameters |
| ------------------ | --------------- |
| Manual Grid Search | ARIMA(0,1,0)    |
| Auto ARIMA         | ARIMA(2,1,2)    |

Final Model:

ARIMA(0,1,0)** (Random Walk)

Model Statistics:

* AIC: -10318.53
* BIC: -10313.39

---

Deep Learning Models

Two recurrent neural network models were implemented.

LSTM Model

Architecture:

```
LSTM (64 units)
Dense (1 output)
```

Training configuration:

* Sequence length: **12 months**
* Epochs: **50**
* Data scaling: **MinMaxScaler**

---

GRU Model

Architecture:

```
GRU (64 units)
Dense (1 output)
```

Training configuration:

* Sequence length: **12 months**
* Epochs: **50**

---

Spectral Analysis

Frequency-domain analysis was performed using:

* FFT
* DFT
* Periodogram
* Spectrogram

Key Findings

Johnson & Johnson Dataset

* Strong **low-frequency components**
* Indicates **long-term trends and seasonal patterns**

Amazon Dataset

* Dominant **low-frequency power**
* Indicates **trend-driven stock price behavior**

---

Model Evaluation

Models were evaluated using:

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)
* MAPE (Mean Absolute Percentage Error)

---

# Results

## Johnson & Johnson Dataset

| Model | RMSE     | MAE      | MAPE       |
| ----- | -------- | -------- | ---------- |
| ARIMA | 5.64     | 3.83     | 60.58%     |
| LSTM  | **2.10** | **1.70** | **14.66%** |
| GRU   | 9.19     | 8.90     | 71.69%     |

**Best Model:** LSTM

Reason: Ability to capture **non-linear patterns and seasonality**.

---

## Amazon Dataset

| Model | RMSE     | MAE      | MAPE      |
| ----- | -------- | -------- | --------- |
| ARIMA | **3.44** | **1.97** | **1.69%** |
| LSTM  | 4.46     | 3.52     | 3.01%     |
| GRU   | 3.83     | 2.94     | 2.50%     |

**Best Model:** ARIMA

Reason: Stock prices behave more like **random walk processes**, which ARIMA handles well.

---

Key Insights

* **LSTM performs better for nonlinear time series data.**
* **ARIMA performs well for linear trend-driven financial data.**
* GRU showed moderate performance but struggled with smaller datasets.

---

Future Improvements

Potential enhancements include:

* Hyperparameter tuning for LSTM and GRU
* Feature engineering (lag features, moving averages)
* Hybrid models such as:

  * **ARIMA + LSTM**
  * **Stacked LSTM**
* Ensemble forecasting
* Longer sequence inputs (24–36 months)
* Cross-validation for time series
* Deployment for **real-time forecasting systems**

---

Conclusion

This study compared **ARIMA, LSTM, and GRU models** for time series forecasting on two datasets.

Key findings:

* **LSTM performed best for Johnson & Johnson sales data**, capturing nonlinear patterns effectively.
* **ARIMA performed best for Amazon stock prices**, which follow trend-driven dynamics.
* The effectiveness of a forecasting model strongly depends on **data characteristics**.

