
Prognostics and Health Management of Turbofan Engines
RUL Prediction via Dual-Residual Attention
About the Project

This project is based on my final report titled “A Comparative Study of Dual-Residual Attention Architectures for Safety-Critical Remaining Useful Life Estimation.”
The work focuses on predicting the Remaining Useful Life (RUL) of turbofan engines using deep learning models trained on simulated sensor data from NASA’s CMAPSS FD001 dataset.

Rather than only comparing prediction accuracy, the project examines how different recurrent architectures behave over the entire operating life of an engine. In particular, it compares LSTM and GRU models when both are used within the same Dual-Residual Attention framework, and evaluates them using both standard error metrics and a trajectory-level safety score.

What the Project Does

The model processes multivariate time-series sensor data and estimates how much useful life remains before engine failure. A dual-attention mechanism is used so the model can assign importance to both specific sensors and specific time steps in the engine’s history.

Two versions of the same architecture were trained:

one using an LSTM as the temporal encoder

one using a GRU as the temporal encoder

Apart from this difference, the models are identical. This allows a direct comparison of how the two recurrent units affect prediction behavior, especially under long-term degradation.

Data and Preprocessing

The experiments use the NASA CMAPSS FD001 dataset, which simulates turbofan engine degradation under a single operating condition. Each engine run is converted into overlapping windows of 30 time steps.

As described in the report, the target RUL values are capped using a piecewise linear function with a maximum value of 125. During exploratory analysis, sensors s18 and s19 were removed because they showed zero variance across the dataset.

Model and Training

The architecture applies:

sensor-level (spatial) attention,

a residual gating mechanism,

a recurrent encoder (LSTM or GRU),

and time-level (temporal) attention.

All models were trained using the same setup: Adam optimizer, learning rate of 0.001, batch size of 64, and 50 epochs. No additional tuning or architectural changes were introduced beyond what is documented in the report.

Evaluation and Results

Two evaluation approaches were used. The first evaluates prediction error only at the final cycle of each test engine, which is common in CMAPSS literature. The second evaluates prediction error at every time window across the engine’s life, producing a cumulative NASA score that reflects trajectory-level risk.

The reported results show that RMSE values across models are similar, while larger differences appear in the cumulative NASA score when full trajectories are considered.

Interpretability

Attention weights learned by the model were visualized to understand which sensors and which time periods influenced predictions. These visualizations were used for qualitative analysis and do not claim causal validation.
