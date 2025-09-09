# Predicting Crime Rate in Cleveland Census Tracts Using Permit Data

## Overview
This project explores the relationship between infrastructure investment and crime rates in Cleveland, Ohio. Using **building and demolition permit data**, we developed a **long short-term memory (LSTM) neural network** to predict crime rates (per 1,000 residents) across Cleveland census tracts.  

The research goal is to help policymakers evaluate whether infrastructure investments lead to measurable decreases in crime rates — and, consequently, potential cost savings for the city.

---

## Problem Background
Cleveland is consistently ranked among the most dangerous cities in the U.S., with crime costing the city billions annually. Recent initiatives, like the “15-minute city” project, have emphasized infrastructure investment, but mainly focused on transportation.  

This project aims to **fill the gap** by predicting how general infrastructure improvements impact crime rates at the census tract level, allowing for more efficient allocation of resources.

---

## Data
Data was sourced from the **Cleveland Open Data Portal**, organized by the Office of Urban Analytics and Innovation.  

**Datasets used:**
- Crime Incidents (~700,000 rows)  
- Building Permits (~170,000 rows)  
- Demolition Permits (~10,000 rows)  
- Census Tract 2010–2020 Net Change  
- City of Cleveland Census  

Timeframe: **2016–2024**, grouped by census tract and month.  
Final dataset included 12 engineered features related to permit counts, values, and types, along with crime rate statistics.

---

## Methods
- **Feature Engineering:**  
  - Crime incidents bucketed into *violent, nonviolent, and vice*.  
  - Permit types categorized (e.g., housing, business, education, hazard, recreation).  
  - Population changes estimated at the monthly tract level.  
  - Final features normalized via log-transformation.

- **Model:**  
  - Bidirectional **LSTM** network built with TensorFlow.  
  - Two LSTM layers (64 and 32 units) + dropout (30%).  
  - Output layer: single prediction of crime rate per 1,000 residents.  
  - Sliding six-month input windows predicting one year ahead.  
  - Data split: 70% train, 20% validation, 10% test.

---

## Results
- Model outperformed the baseline (predicting next year’s rate using previous year’s average):  
  - **17% improvement overall**  
  - **48% improvement on 2024 predictions**  
- Average error: **~5.6 crimes per 1,000 residents**.  
- Accuracy varied significantly across census tracts.  
- Model performed worse during **pandemic years (2020–2023)** due to disruptions in crime patterns.  
- Certain permit types (education, housing, demolitions) showed stronger associations with reduced crime.

---

## Discussion
- Predictions must be applied **tract-by-tract**, not citywide.  
- Some census tracts showed strong predictive accuracy, while others did not.  
- Policymakers can use model outputs to evaluate whether investment in a given tract is economically justified.  
- Example: In East Shaker Heights (Tract 39035119600), $275K of investment in 2023 was associated with ~$285K predicted crime savings in 2024.

---

## Limitations
- Small census tracts with low permit counts showed high variance.  
- Pandemic disrupted temporal crime patterns.  
- Confounding variables (e.g., increased policing) may influence results.  
- Predictions are **not universal** — must be contextualized regionally.

---

## Future Work
- Incorporate **stratified sampling** to better represent high-crime tracts.  
- Explore additional confounders (e.g., police presence, socioeconomic variables).  
- Extend analysis beyond Cleveland to other U.S. cities.  
- Investigate **longer-term recurring effects** of investments.

---

## Tech Stack
- **Python** (Pandas, NumPy, TensorFlow, scikit-learn, Matplotlib)  
- **Jupyter Notebook** for exploratory analysis and modeling  
- **Cleveland Open Data Portal** for raw data  

