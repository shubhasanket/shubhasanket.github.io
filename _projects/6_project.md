---
layout: page
title: Learning the Rules, Missing the Game - Agent-Based Models and Neural Networks
description: Neural network surrogates for an agent-based voter model
img: assets/img/abm_voter.png
importance: 4
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/abm_voter.png" title="State trajectory heatmaps: ABM vs. learned surrogates" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    State trajectory heatmaps for a representative rollout of the synchronous voter model: the ground-truth ABM (left) against learned Logistic Regression, MLP, and GNN surrogates.
</div>

This project, carried out at ENS Paris-Saclay jointly with **Vibhu Dalal**, asks a simple but subtle question: if a neural network can predict the next step of an interacting system accurately, has it really learned the dynamics? Many agent-based models (ABMs) generate rich macroscopic behaviour - clustering, consensus, phase transitions - from simple local rules, and a natural machine learning question is whether learned models can serve as faithful surrogates for those rules.

We study this in a controlled setting using the **synchronous voter model** on an Erdős-Rényi graph. At each time step every agent copies a randomly chosen neighbour's binary opinion; the system is stochastic and eventually reaches an absorbing consensus state. We train three surrogate models - Logistic Regression, an MLP, and a graph neural network (GNN) - to predict next-step probabilities from the current configuration, and then probe them at progressively harder levels.

**Three experiments.** *One-step prediction* tests whether the local transition rule can be learned from data across dataset sizes from 10² to 10⁵. *Rollout stability* applies the learned models recursively, sampling next states from their Bernoulli outputs, and measures how Hamming and mean-opinion errors grow over horizons up to 100. *Emergent behaviour* compares macroscopic statistics across six initial-condition regimes - balanced, biased, near-consensus, and clustered - focusing on whether the surrogates reach and remain at consensus the way the true ABM does.

**What we found.** All three models learn the one-step rule well: with enough data the MLP and Logistic Regression are essentially indistinguishable, and the GNN's inductive bias is most useful in the small-data regime. But local accuracy does not translate into faithful simulation. Under recursive rollout, microscopic errors saturate near the decorrelation level within a handful of steps, regardless of dataset size. At the macroscopic level the gap is sharper still: the true ABM reaches stable consensus across all regimes, while Logistic Regression almost never does, the MLP often hits consensus only transiently, and the GNN comes closest but still allows the absorbing state to be broken. We trace this to a structural mismatch - supervised one-step training does not enforce the absorbing property of consensus, and Bernoulli sampling at every step gives any nonzero flip probability a chance to escape it.

The broader message is that learning local rules is not the same as learning the game those rules are playing. Capturing the right long-term dynamics of an interacting system requires structural inductive biases, multi-step or distribution-level training objectives, or explicit enforcement of properties like absorbing states - none of which are supplied for free by standard supervised learning.

You can find the project on GitHub [here](https://github.com/shubhasanket/Learning-the-Rules-Missing-the-Game-Agent-Based-Models-and-Neural-Networks).
