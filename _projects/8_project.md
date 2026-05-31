---
layout: page
title: LLM Reasoning for Machine Translation
description: Investigating the CoT penalty for machine translation at small scale
img: assets/img/llm_mt.png
importance: 6
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/llm_mt.png" title="LLM Reasoning for Machine Translation - project report" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Teacher-student fine-tuning framework for machine translation, using intermediate reasoning and refinement strategies to improve translation quality.
</div>

This was a group project at ENS Paris-Saclay with **Richard Cheam**, **Alexandre Duplessis**, and **Tudy Herriou**, investigating an empirical puzzle: chain-of-thought (CoT) reasoning has transformed LLM performance on math and code, yet recent work shows that enabling thinking tokens in large reasoning models does not improve machine translation, and that CoT fine-tuning *underperforms* standard input-output fine-tuning. The natural question is *why* - why does explicit reasoning help one domain and not the other?

The project takes a four-phase approach. **Phase 1** establishes the phenomenon across few-shot prompting, fine-tuning, and CoT prompting on small models (gemma-3-270m, gemma-3-1b-pt and -it, Qwen3-1.7B/4B), confirming that CoT degrades MT quality at this scale. **Phase 2** analyses the reasoning traces themselves and tests their faithfulness via perturbation and truncation, finding that thinking-model traces are essentially ignored by the model, while instruct-model traces are used but actively harmful. **Phase 3** tests four hypotheses for *why* reasoning fails - non-decomposability, no training signal, System-1 disruption, and language interference - and identifies a Catch-22: where the model can reason well (high-resource, easy sentences) translation already works via pattern matching, and where reasoning is genuinely needed (low-resource, hard sentences) the model hallucinates instead. **Phase 4** uses these findings to design informed prompting strategies, showing that *target-language thinking* and *targeted post-hoc verification* are the most effective interventions at small scale.

**My contribution** was Phase 1, Section 2.1 - *Few-shot Machine Translation with Base LLMs*. I designed and ran the few-shot prompting study with the two base Gemma models, sweeping over number of demonstrations, translation direction, resource setting, and language typology to establish a baseline picture before any explicit reasoning was introduced. The results in that section show that model scale dominates, that few-shot gains saturate by around four shots and concentrate on mid-resource pairs, that translation direction is strongly asymmetric (X→English noticeably easier than English→X), and that direct prompting is consistently stronger than CoT, a finding which then anchors the project's broader investigation of why reasoning hurts MT.

Taken together, the project argues that at the 2-4B parameter scale CoT traces for MT are either ignored or harmful, that this reflects a *routing* problem rather than a capability gap, and that the right design principle is to preserve direct translation for cases the model already handles well, applying minimal targeted reasoning only when verifiable post-checks make it worthwhile.

You can find the project on GitHub [here](https://github.com/shubhasanket/LLM-Reasoning-for-Machine-Translation).
