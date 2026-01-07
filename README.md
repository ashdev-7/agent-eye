# Prognostics and Health Management of Turbofan Engines
## RUL Prediction via Dual-Residual Attention

## About the Project

This repository is based on my final report titled  
**“A Comparative Study of Dual-Residual Attention Architectures for Safety-Critical Remaining Useful Life Estimation.”**

The project focuses on predicting the Remaining Useful Life (RUL) of turbofan engines using deep learning models trained on simulated sensor data from NASA’s CMAPSS FD001 dataset.

Rather than limiting the analysis to final-cycle prediction accuracy, the work studies how different recurrent architectures behave across the entire operational life of an engine. Specifically, it compares LSTM and GRU models embedded within the same Dual-Residual Attention framework, evaluated using both standard error metrics and a trajectory-level safety score.

## What the Project Does

The model processes multivariate time-series sensor data to estimate how much useful life remains before engine failure. A dual-attention mechanism allows the model to assign importance to both specific sensors and specific time steps in the engine’s history.

Two versions of the same architecture were trained:

- one using an LSTM as the temporal encoder  
- one using a GRU as the temporal encoder  

Apart from the recurrent unit, the architectures are identical. This enables a direct comparison of how LSTM and GRU units influence prediction behavior under long-term degradation.

## Data and Preprocessing

The experiments use the NASA CMAPSS FD001 dataset, which simulates turbofan engine degradation under a single operating condition. Each engine run is converted into overlapping windows of 30 time steps.

As described in the report, target RUL values are capped using a piecewise linear function with a maximum value of 125. During exploratory analysis, sensors s18 and s19 were removed because they showed zero variance across the dataset.

## Model and Training

The architecture consists of:

- sensor-level (spatial) attention  
- a residual gating mechanism  
- a recurrent encoder (LSTM or GRU)  
- time-level (temporal) attention  

All models were trained using the same configuration: Adam optimizer, learning rate 0.001, batch size 64, and 50 epochs. No additional tuning or architectural changes were introduced beyond what is documented in the report.

## Evaluation and Results

Two evaluation strategies were used.

The first measures prediction error only at the final cycle of each test engine, which is common in CMAPSS-related literature.

The second evaluates prediction error at every time window across the engine’s life, producing a cumulative NASA score that reflects trajectory-level risk.

The reported results show that RMSE values are similar across models, while larger differences appear in the cumulative NASA score when full life-cycle trajectories are considered.

## Interpretability

Attention weights learned by the models were visualized to examine which sensors and which time periods influenced predictions. These visualizations were used for qualitative analysis only and do not claim causal validation.
