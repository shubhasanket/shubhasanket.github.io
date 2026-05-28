---
layout: page
title: Fitting Stochastic Differential Equations to the Lorenz Trajectory
description: SDE surrogate models for chaotic Lorenz dynamics
img: assets/img/lorenz_sde.png
importance: 3
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/lorenz_sde.png" title="Autoregressive SDE fit to the Lorenz x-component" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An autoregressive SDE fit (blue) compared with the original Lorenz x(t) trajectory (orange).
</div>

This project, carried out during my research internship in the AIRSEA team at Laboratoire Jean Kuntzmann (CNRS), develops a systematic methodology for inferring a stochastic differential equation (SDE) that approximates the dynamics of the deterministic, chaotic **Lorenz system** - focusing on its x-component as the observed signal.

The approach combines numerical simulation via the Euler-Maruyama scheme, parametric forms for the drift and diffusion coefficients, and maximum-likelihood estimation through a joint negative-log-likelihood loss tailored to the discrete-time approximation. I compared three models of increasing complexity: a linear drift with polynomial diffusion; an autoregressive linear drift with exponential diffusion; and an autoregressive linear-quadratic drift with exponential diffusion. To assess fit quality I introduced a simple sign-invariant L2 trajectory distance, complemented by visual comparison of trajectories.

The results highlight a clear trade-off between model complexity and stability. The simplest model is stable but produces noisy trajectories that do not resemble the Lorenz dynamics; the autoregressive model resembles the Lorenz x(t) more closely as the lag order grows, but becomes increasingly unstable and prone to explosive amplitudes; and the most flexible model, while it converges during optimization, diverges at simulation time. Overall the study illustrates both the promise and the difficulty of using SDEs as reduced surrogate models for chaotic deterministic systems.

You can find the project on GitHub [here](https://github.com/shubhasanket/Fitting-a-Stochastic-Differential-Equation-to-a-Deterministic-Lorenz-Trajectory).
