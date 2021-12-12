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
- Add a regularisation term to misclassified examples, which aims to draw the perturbs examples close to their clean counterparts.
- Use BCE instead of commonly used CE. Point: adversarial learning requires a strong classifier.
- Use KL divergence to characterise the distinction between misclassified examples and their perturbed counterparts with soft decision.

