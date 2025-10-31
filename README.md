# Microsoft Stock Closing Price Prediction (MSFT)

## 📘 COVER PAGE

**Title:** Microsoft Stock Closing Price Prediction (MSFT)  
**Authors:** Esteban Javier Berumen Nieto, Priscila Cervantes Ramírez, Mariana Salome García González  
**Institution:** Instituto Tecnológico y de Estudios Superiores de Occidente (ITESO)

---

## 💡 MOTIVATION

### Why was Microsoft chosen?

Microsoft (MSFT) was selected because it is one of the largest and most representative technology companies globally.  
Its stock trades on NASDAQ, is highly liquid, and exhibits relatively stable price movements compared to other tech equities.

### Company Overview

**Microsoft Corporation** is an American multinational company founded in **1975** by **Bill Gates** and **Paul Allen**, dedicated to developing **software, hardware, cloud services, and consumer/business products**.

**Main products:**
- **Windows** – Operating systems  
- **Office Suite** – Word, Excel, PowerPoint  
- **Azure** – Cloud computing services  
- **Xbox** – Video game consoles  
- **LinkedIn** – Professional social network  

### Key Milestones
- **1975:** Founded by Bill Gates and Paul Allen  
- **1981:** Release of MS-DOS, becoming an industry standard  
- **1985:** Launch of Windows 1.0 with a graphical user interface  
- **1986:** Microsoft goes public (IPO) and is listed on NASDAQ as MSFT  
- **1990s:** Dominates OS and office software markets with Windows and Office  
- **2000s:** Launches Windows XP, Vista, and Windows 7  
- **2014:** Satya Nadella becomes CEO, focusing on cloud and digital transformation  
- **2016:** Acquires LinkedIn for $26.2 billion USD  
- **2018:** Major expansion of Azure as a cloud leader  
- **2021–2025:** Strategic investments in AI, acquisitions like Nuance Communications, and growth of enterprise and consumer products  

---

## 🧠 METHODOLOGY

### SARIMAX Model

**Order Selection:**
Based on **ACF** and **PACF** analysis, the selected parameters were:  
*(p=1, d=1, q=1) × (P=0, D=1, Q=1, s=5)*, accounting for the weekly pattern of 5 trading days.

**Seasonality:**
A seasonal component with a 5-day period was used to capture weekday effects.

**Exogenous Variables:**
In addition to the closing price, exogenous variables such as **open**, **high**, **low**, and **daily percentage change** were included.  
These enhance the model’s predictive power by capturing daily price behavior — a decision supported by **CCF (cross-correlation function)** analysis.

**Model Selection (AIC/BIC):**
After comparing multiple variations, the model with the **lowest AIC and BIC** values was chosen, as these indicate better model fit with minimal complexity.

#### Selected SARIMAX Model

| #  | Trend | Seasonal (P,D,Q,s) | AIC        | BIC    | MAE        | MSE        |
| -- | :---- | :----------------- | :--------- | :----- | :--------- | :--------- |
| 9  | c     | (0,1,1,5)          | -34.86     | -14.49 | **0.0177** | **0.0005** |

---

### FFNN (Feedforward Neural Network)

**Hyperparameter Selection:**
- **Input lags:** Last **7 days** used as input features to capture short-term dependencies.  
- **Architecture:** Three dense hidden layers with **64**, **32**, and **8** neurons respectively.  
- **Activation functions:**  
  - Hidden layers: **ReLU**  
  - Output layer: **Linear** (for continuous value prediction)  
- **Optimizer:** **Adam**  
- **Regularization:** **EarlyStopping (patience=15)** to avoid overfitting.

**Walk-Forward Validation Scheme:**
A key step for time-series evaluation — the model is **retrained sequentially** as new data becomes available.  
The dataset was divided into **training**, **validation**, and **test** sets.  
The trained model generated **5-day forecasts** for the week **October 20–24, 2025**.

**FNN Performance:**
> **Test MSE:** 0.006761 | **Test MAE:** 0.057989

---

## 📊 PREDICTIONS

| date       | pred_close_sarimax | pred_close_FNN |
|-------------|--------------------|----------------|
| 2025-10-20  | 513.641784         | 512.347839     |
| 2025-10-21  | 513.710796         | 511.750122     |
| 2025-10-22  | 513.666771         | 511.873840     |
| 2025-10-23  | 513.656211         | 511.680969     |
| 2025-10-24  | 513.609880         | 511.871185     |

**Forecast Summary:**
Both models show stable predictions across the 5-day horizon.  
The **SARIMAX model** captures smoother mean-reverting behavior, while the **FFNN model** slightly adjusts for recent short-term movements.

---

## 🧾 CONCLUSION

The combination of **SARIMAX** (for interpretable statistical modeling) and **FFNN** (for nonlinear pattern learning) provides a robust comparative framework for stock forecasting.  
While both deliver similar results, **FFNN** shows better adaptability to small trend changes, whereas **SARIMAX** maintains strong baseline consistency.

---

