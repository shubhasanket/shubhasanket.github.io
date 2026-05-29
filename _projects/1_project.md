---
layout: page
title: Neural Network-Based PDE Solver Using the Feynman-Kac Formula
description: Mesh-free neural PDE solver
img: assets/img/feynman_kac.png
importance: 2
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/feynman_kac.png" title="Neural network vs exact Black-Scholes surface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The neural network learns the full space-time Black-Scholes price surface (left) and matches the exact solution (right).
</div>

Classical PDE solvers such as finite differences and finite elements are effective in low dimensions but become intractable in high dimensions due to the curse of dimensionality. This project develops a mesh-free alternative built on the **Feynman-Kac formula**, which reformulates certain linear parabolic PDEs as expectations over stochastic processes - turning a deterministic solve into a statistical estimation problem.

The key observation is that the Feynman-Kac representation expresses the PDE solution as a conditional expectation, which is exactly the minimizer of a mean-squared-error regression problem. I therefore train a neural network to approximate that conditional expectation: simulate trajectories of the underlying SDE, evaluate the terminal payoff to build training targets, and fit the network by minimizing the MSE between its prediction and the (noisy) labels. Despite the label noise, the network learns the conditional mean rather than interpolating the data.

I validated the method on the heat equation and on the **Black-Scholes** equation for pricing European call options, generating data both via the closed-form geometric Brownian motion solution and via Euler-Maruyama discretization. I then extended the fixed-time model to a single network that learns the entire space-time price surface, removing the need to retrain for each maturity. Across experiments the neural solver showed strong agreement with both Monte Carlo simulation and the Crank-Nicolson finite-difference scheme, while offering mesh-free, reusable inference across all time-price pairs.

You can find the project on GitHub [here](https://github.com/shubhasanket/Neural-Network-Based-PDE-Solver-Using-the-Feynman-Kac-Formula).
