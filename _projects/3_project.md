---
layout: page
title: Deep Learning-Based Volatility Forecasting
description: Forecasting realized volatility with deep learning models
img: assets/img/volatility_forecast.png
importance: 3
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/volatility_forecast.png" title="Forecasted vs. realized volatility on the test set" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Forecasted (orange) vs. realized (blue) daily volatility on the test split.
</div>

This project, carried out jointly with **Ruben Cardoso** at ENS Paris-Saclay, builds deep learning forecasters for next-day financial volatility on the **Oxford–Man Realized Volatility** dataset and compares them against classical econometric baselines. Inputs are lagged realized-volatility estimators (rv5, rv10, bipower variation, median RV, semivariance), daily and overnight log returns, and trade counts; the target is the next-day log realized volatility.

A central design choice is a **symbol-aware pipeline**: rolling windows are built per symbol with chronological train/validation/test splits, but a single deep model is trained jointly across all symbols so it can learn shared structure without leaking information across them. We compare HAR-RV and GARCH(1,1) baselines (fit per symbol) against naive deep models (windowed MLP, LSTM) and four TCN-based architectures inspired by *DeepVol*: a vanilla causal-convolution TCN, a Gated TCN, a TCN with temporal attention pooling, and a hybrid causal-Conv1d → GRU → attention model. Performance is measured with MSE, the QLIKE loss, and directional accuracy.

The results show a clear hierarchy. HAR-RV remains the strongest model overall on MSE and QLIKE - confirming the importance of multi-horizon persistence - but it is fit per symbol. Among the symbol-pooled deep models, the TCN-based architectures substantially outperform MLP and LSTM, and GatedTCNVol surpasses symbol-specific GARCH. Attention pooling adds only marginal gains over plain causal convolutions. The takeaway is that a single deep model trained jointly across instruments can rival symbol-specific parametric baselines, with architectural inductive bias (causal convolutions, gating) mattering more than raw capacity.

You can find the project on GitHub [here](https://github.com/shubhasanket/DL-Based-Volatility-Forecasting).
