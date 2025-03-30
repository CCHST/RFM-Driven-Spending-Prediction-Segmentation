# Customer Segmentation & Spending Prediction using RFM and Machine Learning

## Project Overview

This project leverages **RFM (Recency, Frequency, Monetary)** analysis and machine learning models to:

1. **Segment customers** based on past behavior  
2. **Predict future RFM segments**  
3. **Estimate Q4 2025 spending** per customer group  
4. **Visualize segment transitions** and generate actionable insights for credit line adjustments

---

## Data Period

- **Training & Observation**: July 2024 – March 2025  
- **Training Target**: 2024 Q4  
- **Prediction Input**: 2025 Q1  
- **Prediction Target**: 2025 Q4 (estimated)

---

## Key Steps & Workflow

1. **Data Processing & Wrangling**  
   - Handle missing values and drop duplicates  
   - Filter transaction codes related to actual spending/purchases  

2. **Data Integration**  
   - Merge transaction records with customer and account datasets

3. **Historical Spending Pattern Analysis**  
   - Explore trends in customer transaction behavior over time  

4. **RFM Feature Engineering**  
   - Convert transaction dates to datetime format  
   - Filter observation period (e.g., July–September 2024)  
   - Calculate RFM metrics per customer:
     - `Recency`: Days since last transaction  
     - `Frequency`: Number of transactions  
     - `Monetary`: Total spending amount  

5. **Model Setup & Forecasting**  
   - Use RFM scores from **2024 Q3** as input features (X)  
   - Use **2024 Q4** RFM scores as prediction target (y)  
   - Train a classifier (Random Forest) to learn customer segment transitions  
   - Predict RFM segments for **Q4 2025** using Q1 2025 data  

6. **Model Evaluation & Insights**  
   - Evaluate model performance with accuracy and classification metrics  
   - Generate a **transition matrix** to visualize customer movement across segments  
   - Estimate potential **Q4 2025 spending** by predicted segment  