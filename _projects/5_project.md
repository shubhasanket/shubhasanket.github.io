---
layout: page
title: Bridging the Inference Gap - Consistent Training for Low-Resource Cross-Lingual Intervention
description: Inference-time cross-lingual intervention for large language models
img: assets/img/incline.png
importance: 3
category: work
giscus_comments: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/incline.png" title="INCLINE project poster" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Project poster: consistent training for inference-time cross-lingual intervention. Joint work with Kshitij Ambilduke at ENS Paris-Saclay.
</div>

This project, carried out at ENS Paris-Saclay jointly with **Kshitij Ambilduke**, studies how to reduce the cross-lingual performance gap of large language models *without* retraining them. Language models perform well overall but remain heavily English-centric, with large gaps on low-resource languages; full fine-tuning or retraining to close those gaps is expensive.

We build on **INCLINE** (Inference-Time Cross-Lingual Intervention), which aligns internal representations across languages and transfers knowledge from high- to low-performing languages, applied purely at inference time with no parameter updates. Concretely, we learn an alignment matrix that maps source-language hidden states into the target-language representation space, and at inference we project the test input into the target space and blend it with the original representation using a strength hyperparameter.

**Our contribution - consistency.** We observed that INCLINE trains for a direct projection but then uses that projection for *mixing* during inference, creating an objective mismatch. We modify the training objective to directly optimize the post-intervention vector, so the alignment learns the specific shift needed given the mixing factor. We also add L2 regularization, since the system is heavily over-parameterized.

We evaluated on a low-resource translation task using Llama-3-8B-Instruct (quantized for tractable compute), extracting sentence representations from the last token of source and target sentences, and measuring translation quality with BLEU, ChrF++ and AfriCOMET (for African languages) on FLORES devtest data. We found that INCLINE helps even in severe low-resource settings and across scripts (somewhat better for Latin scripts), that LoRA outperforms it but at much higher cost, and that our regularized, consistency-trained objective is more stable - notably succeeding on Sanskrit where the non-regularized variant failed - and improves performance on African languages while matching it elsewhere.

You can find the project on GitHub [here](https://github.com/shubhasanket/Inference-Time-Alignment).
