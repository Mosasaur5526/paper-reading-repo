---
title: "Reading Notes for Adversarial Learning"
subtitle: Including notes for adversarial example/attack/defense/training.

# Summary for listings and search engines
summary: This is a note for adversarial learning, which involves adversarial example/attack/defense/training.

# Link this post with a project
projects: []

# Date published
date: "2021-12-12T00:00:00Z"

# Date updated
lastmod: "2021-12-12T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  # caption: 'Image credit: [**Pi**](https://zhuanlan.zhihu.com/p/113729693)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Academic

---

[Improving Adversarial Robustness Requires Revisiting Misclassified Examples (ICLR 2020)](https://openreview.net/forum?id=rklOg6EFwS)
- Defense method named as MART.
- Add a regularisation term to misclassified examples, which aims to draw the perturbs examples close to their clean counterparts.
- Use BCE instead of commonly used CE. Point: adversarial learning requires a strong classifier. Still use CE to find adversarial examples.
- Use KL divergence to characterise the distinction between misclassified examples and their perturbed counterparts with soft decision.
- Conclude that technique used for inner maximisation has a negligible influence on the final robustness, while the outer minimization counts a lot.
- Consider MART under unsupervised settings.

[Evading Defenses to Transferable Adversarial Examples by Translation-invariant Attacks (arXiv 1904, CVPR 2019)](https://arxiv.org/abs/1904.02884)
- Argue that common adversarial examples not having much transferability could be attribute to adversarially trained models have distinctive discriminative regions.
- Propose TI attack which calculates weighted gradients of different pixel translation at each step of gradient-based attack methods.
- Assume CNN is locally translation-invariant on gradients and propose a computationally efficient method which is to convolve the gradient with a kernel matrix.

[Improving Transferability of Adversarial Examples with Input Diversity (arXiv 1803, CVPR 2019)](https://arxiv.org/abs/1803.06978)
- Propose DI attack which randomly adds a transformation to the image before calculating gradient at each step of gradient-based attack methods.
- Is inspired from some defenses which use image transformation to disable the malicious attack.
- Trust the random transformation is helpful to alleviate over-fitting.

[Skip Connections Matter: On the Transferability of Adversarial Examples Generated with ResNets (arXiv 2002, ICLR 2020)](https://arxiv.org/abs/2002.05990)
[Ensemble Adversarial Training: Attacks and Defenses (arXiv 1705, ICLR 2018)](https://arxiv.org/abs/1705.07204)
[Mind the box: l1-APGD for sparse adversarial attacks on image classifiers (arXiv 2103, ICML 2021)](https://arxiv.org/abs/2103.01208)
[Adversarial Examples Are Not Bugs, They Are Features (arXiv 1905, NeurIPS 2019)](https://arxiv.org/abs/1905.02175)
[Adversarial examples in the physical world (arXiv 1607, ICLR 2017 workshop)](https://arxiv.org/abs/1607.02533)
[Fast is better than free: Revisiting adversarial training (arXiv 2001, ICLR 2020)](https://arxiv.org/abs/2001.03994)
[Deep Image Prior (arXiv 1711, CVPR 2018)](https://arxiv.org/abs/1711.10925)
[Adversarial Training for Free! (arXiv 1904, NeurIPS 2019)](https://arxiv.org/abs/1904.12843)


