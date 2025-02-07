[![FINOS - Incubating](https://cdn.jsdelivr.net/gh/finos/contrib-toolbox@master/images/badge-incubating.svg)](https://finosfoundation.atlassian.net/wiki/display/FINOS/Incubating)

# Global Financial Market Data Harmonization Project

## Problem Statement
Despite post-2008 financial crisis reforms in derivatives trading and reporting, financial regulators face significant challenges in obtaining a comprehensive view of market activity due to:
- Inconsistent data formats across different jurisdictions
- Varying reporting standards between exchanges
- Multiple currency denominations
- Lack of standardized data elements
- Difficulties in cross-border data sharing and analysis

## Objective
Develop a machine learning solution to:
1. Harmonize financial market data across different exchanges
2. Create standardized reporting formats
3. Enable real-time risk assessment across global markets
4. Facilitate regulatory oversight through unified data analysis

## Important Terms:
1. **RSI** → Momentum and Reversal Points  
2. **MACD** → Trend Changes and Strength  
3. **Volume** → Confirmation of Price Moves  
4. **Volatility** → Risk Levels  
5. **Bollinger Bands** → Price Channels and Extremes  

## Prediction Table : 
<img width="1183" alt="image" src="https://github.com/user-attachments/assets/d3a15ce2-b06a-4dc4-bfb6-3dc35364e5b6" />

# Market Analysis Model Documentation

## Overview
This project aims to predict market trends using two different types of models:
1. **LSTM (Long Short-Term Memory)** model.
2. **Traditional ML Models** (Random Forest, XGBoost, Gradient Boosting, Support Vector Regressor).

Both models are trained using the same dataset, but the LSTM model is used for sequence-based forecasting, while the traditional models use individual data points for prediction.

## Features and Target Prediction

### Primary Column Predicted:
- **Column:** `Returns`  
- **Description:** The returns represent the percentage change in the stock's closing price from the previous day.  
  **Formula:**
  \[
  \text{Returns} = \frac{P_t - P_{t-1}}{P_{t-1}}
  \]
  Where:
  - \(P_t\) is the price at time \(t\),
  - \(P_{t-1}\) is the price at time \(t-1\).

### Derived Column Predicted:
- **Column:** `Log_Returns`  
- **Description:** Logarithmic returns are used to model continuous compounding, often preferred in financial modeling.  
  **Formula:**
  \[
  \text{Log Returns} = \ln\left(\frac{P_t}{P_{t-1}}\right)
  \]
  Where:
  - \(P_t\) is the price at time \(t\),
  - \(P_{t-1}\) is the price at time \(t-1\),
  - \(\ln\) denotes the natural logarithm.

### Feature Columns Used for Training:
The following feature columns are used in training both LSTM and traditional models:

1. **`Returns`** – Percentage change in closing price.
2. **`Log_Returns`** – Logarithmic returns derived from the `Returns`.
3. **`MA5`** – 5-day moving average of the closing price.
4. **`MA20`** – 20-day moving average of the closing price.
5. **`MA50`** – 50-day moving average of the closing price.
6. **`Volatility`** – Standard deviation of returns, calculated over a 20-day rolling window.
7. **`RSI`** – Relative Strength Index (RSI), used to identify overbought/oversold conditions in the market.
8. **`MACD`** – Moving Average Convergence Divergence, used to identify potential buy or sell signals.
9. **`Volume_Rate`** – Volume divided by its 20-day moving average, used to identify spikes in trading volume.

## Model Training Process

### 1. LSTM Model
- The LSTM model is used for sequence-based prediction where the historical data is used to predict future values.
- The model is built with two LSTM layers and dropout for regularization. It predicts `Returns` as the primary output.

### 2. Traditional Models
- The traditional models, such as **Random Forest**, **XGBoost**, **Gradient Boosting**, and **Support Vector Regressor**, are trained on individual features like `Returns`, `Log_Returns`, `MA5`, `RSI`, etc.
- These models do not consider the sequence nature of the data but rather individual points of market features.

## Code Implementation

```python
# Loading and Preprocessing Data

def load_data(self):
    """Load and prepare CSV data"""
    # Read and process the data
    # Date column conversion and sorting
    # Feature engineering for returns, moving averages, RSI, etc.

def create_features(self):
    """Create technical indicators for analysis"""
    # Create returns, log returns, moving averages, volatility, RSI, etc.

def prepare_sequences(self, sequence_length=5000):
    """Prepare sequences for LSTM"""
    # Scale data and prepare sequences for the LSTM model.

def build_lstm_model(self, input_shape):
    """Build the LSTM model architecture"""
    # LSTM with two layers and dropout

def train_models(self, X_lstm, y):
    """Train both LSTM and traditional models"""
    # Train LSTM model
    # Train RandomForest, XGBoost, GradientBoosting, SVR using traditional features

# Anomaly detection using IsolationForest
def detect_anomalies(self):
    """Detect market anomalies"""
    # Use IsolationForest for anomaly detection based on features

def plot_results(self, y_test, anomalies, history):
    """Visualize the results of model predictions"""
    # Plot actual vs predicted values, performance metrics, and anomaly detection
```
## Models Comparitive Performance 

<img width="641" alt="image" src="https://github.com/user-attachments/assets/a9af32c4-710c-41d3-bd8f-17a49981ad23" />

## Anomaly Detection in Trade Price Data

<img width="666" alt="image" src="https://github.com/user-attachments/assets/6cb85e60-e566-4ee6-bdfe-d9528b86fa83" />

## Feature Correlation

<img width="615" alt="image" src="https://github.com/user-attachments/assets/781b8f44-6703-4dac-b76f-f385569d2b9d" />




