# COVID-19 Mortality Forecasting: A Time Series Analysis

**Project by:** Filip Sahatqija (https://www.linkedin.com/in/filip-sahatqija-474661207/)

**Domain:** Data Analysis & Epidemiology | Self-Initiated Research

## Overview

This project presents a comprehensive time series analysis and forecast of COVID-19 mortality in Norway. Using publicly available data from 1 January 2020 to 10 April 2021, the analysis compares mortality and incidence patterns between Slovakia and Norway. The primary goal is to develop a predictive model that forecasts weekly deaths based on past mortality data and case incidence.

The project employs a range of statistical models, including Exponential Smoothing, ARIMA, SARIMA, and ARIMAX, with a key finding that weekly case counts with a one-week lag are a significant predictor of mortality. The final model is rigorously evaluated using statistical diagnostics to ensure its validity and reliability.

---

## Problem Statement

Accurate prediction of COVID-19 mortality is critical for guiding public health responses, resource allocation, and hospital readiness. This project seeks to answer the question: **Can we accurately forecast weekly COVID-19 deaths in Norway using past case and mortality data?**

The central hypothesis is that the number of new COVID-19 cases is a significant predictor of the number of deaths in subsequent weeks.

---

## Data

The dataset used in this analysis is the "COVID-19 Data Repository by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University."

* The analysis focuses on data for **Norway** and **Slovakia**.
* The time period covered is from **January 22, 2020, to April 10, 2021**.

---

## Methods and Models

The analysis was conducted in Python using `pandas`, `statsmodels`, and `pmdarima`. The key methods include:

* **Data Cleaning and Preprocessing:** SQL queries via the `duckdb` library were used for efficient data filtering and manipulation.
* **Exploratory Data Analysis (EDA):** Visualization of daily and weekly trends, including rolling averages, to compare the pandemic's trajectory in Norway and Slovakia.
* **Time Series Modeling:**
    * Holt-Winters Exponential Smoothing
    * ARIMA (Autoregressive Integrated Moving Average)
    * SARIMA (Seasonal ARIMA)
    * **ARIMAX (ARIMA with Exogenous Variables):** This model was used to incorporate weekly case counts as a predictor for deaths. Models with 1, 2, and 3-week lags for case counts were tested.
* **Model Diagnostics:** All models were evaluated using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and Mean Absolute Percentage Error (MAPE). Residuals were thoroughly checked for autocorrelation (Ljung-Box test), normality (Jarque-Bera test), and heteroscedasticity.

---

## Key Findings

1.  **Different Pandemic Trajectories:** Slovakia experienced significantly higher peaks in both case incidence and mortality compared to Norway during the analyzed period.
![Weekly difference in deaths between Norway and Slovakia.](/images/weekly_difference_plot.png)
2.  **Cases Predict Deaths:** The ARIMAX model confirmed that COVID-19 case numbers are a statistically significant predictor of deaths.
3.  **Optimal Lag Period:** The most effective model was an **ARIMAX(2,0,1) model using a one-week lag** between reported cases and deaths. This model provided the best balance of predictive accuracy and statistical significance.
![One-week lag between cases and deaths](/images/lag1.png)
4.  **Model Diagnostics:** Despite one major outlier in the first week of prediction, the final model's residuals were found to be homoscedastic and free of autocorrelation, indicating a robust and reliable fit.
![QQ plot with outlier](/images/qq_plot_full.png)
The original QQ plot shows that the model’s residuals do not follow a normal distribution (the red line). I assumed that the residuals did not show normal distribution because of one single outlier—the first prediction, which had a large error (see the blue dot near the -2 value on the x-axis).

![QQ plot without outlier](/images/qq_plot.png)
After removing the outlier, the residuals are aligned around the red reference line, indicating a much smaller deviation from normality in the residual distribution.

5. **Model Evaulation:** The final model was very accurate, with a Mean Absolute Percentage Error (MAPE) of just 8.6%. **This means the model's weekly forecast was, on average, off by only 8.6% from the actual number of deaths.**

---
## Public Health Implications

These results demonstrate that **timely COVID-19 case surveillance can provide early warning for mortality surges.** In practice, this can help:

- Anticipate hospital capacity needs.
- Guide resource allocation.
- Support targeted public health interventions.

---

## How to Run This Project

To replicate this analysis, please follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone <https://github.com/Sahatfi/time-series-covid>
    cd time-series-covid
    ```
2.  **Create and activate a virtual environment (recommended):**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```
3.  **Install the required libraries:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Run the Jupyter Notebook:**
    Launch Jupyter and open the `time-series-covid.ipynb` notebook located in the `notebooks/` directory.
    
    ---
