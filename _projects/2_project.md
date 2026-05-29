---
layout: page
title: Auto-Encoder with Regression for Time Series Anomaly Detection
description: PyTorch implementation with extended thresholding strategies
img: assets/img/aer_anomaly.png
importance: 2
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/aer_anomaly.png" title="AER anomaly detection on UCR time series" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    AER anomaly detection on UCR data: raw vs. processed signal, AER reconstruction, and the final anomaly score with detected windows highlighted.
</div>

This project is a from-scratch PyTorch reimplementation of the **Auto-Encoder with Regression (AER)** framework for univariate time-series anomaly detection. AER combines reconstruction-based detection - an auto-encoder trained on sliding windows of "normal" signal - with a bi-directional regression head on the latent representations, which improves sensitivity to subtle anomalies that a pure reconstruction loss tends to smooth over.

The reference implementation in `orion-ml` is built on TensorFlow/Keras, locked to Python 3.8–3.11, and abstracts most design choices behind its API - so it doesn't run on current Colab and is hard to experiment with. I rewrote the full pipeline in PyTorch directly from the equations in the paper, structured as a transparent end-to-end module: preprocessing, sliding windows, AER training, forward/reverse prediction with reconstruction, per-timestep error computation, score combination, and thresholding. On top of reproducing the method, I extended the post-processing layer with **alternative anomaly score constructions** (multiplicative, convex sum, predictive-only, regression-only) and **alternative thresholding strategies**, giving more interpretable control over how anomaly decisions are made.

I validated the implementation on synthetic time series - a sinusoid with injected level shifts, including a trended variant - and on real-world UCR anomaly-detection data, where the model correctly localises the anomalous windows. I also added a *train-once, infer-many* extension so a fitted AER can be reused on similar new series, with a small detection-quality cost on out-of-distribution test signals that I haven't fully tracked down.

You can find the project on GitHub [here](https://github.com/shubhasanket/Auto-Encoder-with-Regression-for-Time-Series-Anomaly-Detection/).
