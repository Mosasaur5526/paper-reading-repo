---
title: Why Does Path Length Regularisation Work
subtitle: Path length regularisation is a new trick for training GAN (i.e. Generative Adversarial Networks) proposed by NVIDIA in their StyleGAN2 paper. In appendix C of the paper, authors of which provide its readers with somewhat obscure explanations of the effects of the trick, leaving novices like me greatly baffled. In this article, I will decompose the whole theory into more detailed proofs of several lemmas respectively, targeting at a deeper comprehension of this prominent piece of art.

# Summary for listings and search engines
summary: Please see [original post](https://zhuanlan.zhihu.com/p/348308433) for full version. Path length regularisation is a new trick for training GAN (i.e. Generative Adversarial Networks) proposed by NVIDIA in their StyleGAN2 paper. In appendix C of the paper, authors of which provide its readers with somewhat obscure explanations of the effects of the trick, leaving novices like me greatly baffled. In this article, I will decompose the whole theory into more detailed proofs of several lemmas respectively, targeting at a deeper comprehension of this prominent piece of art.

# Link this post with a project
projects: []

# Date published
date: "2021-01-31T00:00:00Z"

# Date updated
lastmod: "2021-06-11T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**StyleGAN**](https://openaccess.thecvf.com/content_CVPR_2019/html/Karras_A_Style-Based_Generator_Architecture_for_Generative_Adversarial_Networks_CVPR_2019_paper.html)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Academic

---

Original Post: https://zhuanlan.zhihu.com/p/348308433
