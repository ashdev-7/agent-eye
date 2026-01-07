Prognostics and Health Management of Turbofan Engines
RUL Prediction via Dual-Residual Attention
About the Project

This project is based on my final report titled “A Comparative Study of Dual-Residual Attention Architectures for Safety-Critical Remaining Useful Life Estimation.” The work focuses on predicting the Remaining Useful Life (RUL) of turbofan engines using deep learning models trained on simulated sensor data from NASA’s CMAPSS FD001 dataset.

Rather than limiting evaluation to prediction accuracy at a single point, the project examines how different recurrent architectures behave over the entire operating life of an engine. Specifically, it compares LSTM and GRU models when both are used within the same Dual-Residual Attention framework, and evaluates them using standard error metrics as well as a trajectory-level safety score.

Project Scope

The model processes multivariate time-series sensor data and estimates the remaining operational life before engine failure. A dual-attention mechanism is used so the model can assign importance to both individual sensors and specific time steps within an engine’s history.

Two versions of the same architecture were trained: one using an LSTM as the temporal encoder and one using a GRU. Apart from this difference, the architectures are identical. This setup allows for a direct comparison of how the two recurrent units influence prediction behavior, particularly during long-term degradation.

Data and Preprocessing

The experiments use the NASA CMAPSS FD001 dataset, which simulates turbofan engine degradation under a single operating condition. Each engine trajectory is converted into overlapping windows of 30 time steps.

As described in the report, target RUL values are capped using a piecewise linear function with a maximum value of 125. During exploratory analysis, sensors s18 and s19 were removed because they exhibited zero variance across the dataset.

Model and Training

The architecture consists of sensor-level (spatial) attention, a residual gating mechanism, a recurrent encoder (either LSTM or GRU), and time-level (temporal) attention. All models were trained using the same configuration: Adam optimizer, learning rate of 0.001, batch size of 64, and 50 epochs. No additional tuning or architectural modifications were introduced beyond what is documented in the report.

Evaluation and Results

Two evaluation approaches were used. The first evaluates prediction error only at the final cycle of each test engine, which is common in CMAPSS-based studies. The second evaluates prediction error at every time window across the engine’s operating life, producing a cumulative NASA score that reflects trajectory-level risk.

The reported results indicate that RMSE values across models are similar, while larger differences appear in the cumulative NASA score when full trajectories are considered.

Interpretability

Attention weights learned by the model were visualized to examine which sensors and time periods influenced predictions. These visualizations were used for qualitative analysis only and do not claim causal validation.
