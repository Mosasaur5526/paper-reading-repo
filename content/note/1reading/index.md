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
[Improving Adversarial Robustness via Promoting Ensemble Diversity (arXiv 1901, ICML 2019)](https://arxiv.org/abs/1901.08846)
- Define a new kind of diversity among components which focuses on non-maximal predictions.
- Propose ADP regularisation, which consists of a Shannon entropy term and a logarithm of ensemble diversity (LED).
- The ensemble entropy prevents the prediction results from trivially converge to one-hot vectors and just works like label-smoothing when the LED term is absent.
- The LED part controls to angles among non-maximal predictions by encouraging orthogonal non-maximal predictions among different individuals, and it can be elegantly interpreted as the volume spanned by the prediction vectors.
- Using the computationally efficient proposed ensemble method, they achieve SOTA in both natural accuracy and adversarial robustness and mitigate the transferability among different components since they yields distinctive non-maximal prediction patterns.

[Robustness via curvature regularization, and vice versa (arXiv 1811, CVPR 2019)](https://arxiv.org/abs/1811.09716)
- Examine the loss landscape with respect to the examples, and find adversarial training encourages it to be less flat with smaller curvature.
- Point out a somewhat paradoxical fact that adversarially trained models is more robust as well as easier to attack (FGSM works as effectively as PGD since the loss landscape is flat).
- Establish a theoretical connection between the shortest perturbation misclassifies an example and the largest eigenvalue of Hessian by using the second-order approximation of the loss function.
- Notice that the gradient at a specific point is often collinear to the largest eigenvector in practice. Therefore the bound is approximately tight.
- Propose CURE method to punish largest eigenvalues of Hessian, which is theoretically equivalent to punish the expectation of gradient changes towards some specific directions. Particularly, the directions are chosen to be the gradient direction as it has been observed that it is often collinear to the largest eigenvector.
- Achieve comparable robustness to adversarial training, which partially prove that the curvature vanishing from the loss landscape is not simply a by-product of adversarial training.

[Adversarial Weight Perturbation Helps Robust Generalization (arXiv 2004, NeurIPS 2020)](https://arxiv.org/abs/2004.05884)
- Identify the fact that robust generalisation gap is closely related to flatness of loss landscapes with respect to weight.
- Certify SOTA adversarial training methods always yield flat weight loss landscapes which help close the generalisation gap.
- Propose AWP method to adversarially perturb the weight calculated on a batch of adversarial examples generated on the fly and minimise the double-perturb result.
- Combine AWP with various AT methods and achieve consistent improvement on robustness.

[The Space of Transferable Adversarial Examples (arXiv 1704)](https://arxiv.org/abs/1704.03453)
- Propose a methods which directly estimates the dimensionality of adversarial subspace where adversarial perturbations lie.
- The space is named as GAAS and its construction is implied by the proof of lemma 1. I think the definition and construction method is quite unclear, and the authors conduct no further analysis on the subspace in the rest of the paper.
- Explore decision boundary similarity and find different models have similar decision boundaries, which enables adversarial transferability.
- Claim that adversarial training fails to displace the decision boundaries by a large margin but enhances gradient masking instead. This is consistent with the conclusion that sometimes black-box attack even outperforms white-box attack.
- Analyse the transferability with model-agnostic perturbation between means of different classes and pseudo-linearity of feature extractors. I think this analysis is valueless.
- Use an extreme case of XOR artifacts to demonstrate that transferability among models is not an intrinsic property. This argument is intriguing but impractical in real.

[Self-ensemble Adversarial Training for Improved Robustness (ICLR 2022 submission)](https://openreview.net/forum?id=oU3aTsmeRQV)
- Propose a new method named SEAT, which ensembles different parameter snapshots during the training period.
- The method looks like momentum strategy but it just update the ensemble on the fly.
- Prove the discrepancy in averaged prediction method and weight-averaged models by deriving a condition on second order smallness.
- State that ordinary averaged parameter ensemble method is likely to suffer from the same of homogenisation problem of averaged prediction method, which deteriorates the diversity of individuals.
- Demonstrate model trained using SEAT indeed alleviate the homogenisation problem through experiments.
- Discuss different learning strategies on learning rate, visualise loss landscapes and find common staircase learning rate settings is not suitable in this case, while the cyclic one is.
- Intuitively, learning rate becoming very small encourages homogenisation. Proposition 2 of the paper intends to prove this effect but maybe there're some little problems among the proof lines.
- SEAT + MART + CutMix yields best performance among all mixed training strategies.

[Do Wider Neural Networks Really Help Adversarial Robustness? (arXiv 2010, NeurIPS 2021)](https://arxiv.org/abs/2010.01279)
- Decompose the adversarial training loss into natural empirical risk and a robust regularisation term, just like TRADES etc.
- Argue that the intrinsic trade-off is between natural accuracy and perturbation stability, and robustness accuracy is just a by-product.
- Claim that wider neural networks require fine-tuning of the trade-off parameter, and propose WAR method to efficiently find the best choice.
- Connect Lipschitz constant with perturbation stability and prove that it has the same order of the square of network width.

[Universal adversarial perturbations (arXiv 1610, CVPR 2017)](https://arxiv.org/abs/1610.08401)
- Accumulate valid perturbation for a small subset of data and achieve a universal perturbation.
- The universal perturbation not only has a remarkable generalisation power over unseen data points, but also generalises across different models.
- Find that the perturbation lets most images stray into several dominant labels, presenting a very peculiar topology of the directed graph.
- Report that fine-tuning on dataset with universal perturbation won't provide the network with immunity to it.
- Analyse the geometric distribution of decision boundaries, and successfully construct a subspace spanned from singular values of perturbation directions of different examples, in which random perturbation yields high successful rate.

[Delving into Transferable Adversarial Examples and Black-box Attacks (arXiv 1611, ICLR 2017)](https://arxiv.org/abs/1611.02770)
- Propose to boost transferability of targeted adversarial examples that was hardly transferable at that time using ensemble-optimisation-based approaches.
- Show that gradient direction are orthogonal among different models but decision boundaries are well-aligned.
- Analyse empirical transferability from the RMSD of perturbation.
- Use the geometric properties to explain why ensemble-fast gradient-based approaches won't work.

[Enhancing Adversarial Example Transferability with an Intermediate Level Attack (arXiv 1907, ICCV 2019)](https://arxiv.org/abs/1907.10823)
- Propose a framework called ILA to minimise the difference between feature distinctions of the pre-computed adversarial example's and the fine-tuned one's at a specific layer.
- Use ILAP (Projection) loss to encourage the new feature distinction direction to be parallel to the referential one.
- Use ILAF (flexible) loss to maximise perturbation norm within this layer and show that after fine-tuning the ILAF is superior to ILAP. Besides, ILAF is more model-specific, while ILAP suits for all cases without a need to tune hyper-parameters.
- Establish a connection between the disturbance value of an ILAP attack and the optimal layer.
- Demonstrate that I-FGSM in earlier layers is a worse approximation of Best Transfer Direction, while better in later layers, which explains why earlier layers are not good choices.
- Conclude that extreme linearity of the last several layers gives poor approximation of the true decision boundary and degrades the attack performance.

[Backpropagating Linearly Improves Transferability of Adversarial Examples (arXiv 2012, NeurIPS 2020)](https://arxiv.org/abs/2012.03528)
- Remove some nonlinear layers and fine-tune it, which yields higher adversarial transferability.
- Propose linear back propagation (LinBP) inspired by the previous work of removing skip connections, and further boost transferability.
- For the case of skip connection, add a coefficient according to the sparsity of the ReLU diagonal matrix to cater for its removal.

[MMA Training: Direct Input Space Margin Maximization through Adversarial Training (arXiv 1812, ICLR 2020)](https://arxiv.org/abs/1812.02637)
- Propose max-margin adversarial training (MMA), which maximises the margin to a threshold and simultaneously minimises classification loss.
- Prove that performing gradient descent on logit margin loss on shortest successful perturbation is equivalent to maximising the margin.
- Use soft logit margin loss as a surrogate to stabilise the training, and prove that it is a lower bound of the margin.
- Leverage PGD to find a perturbation direction and do bisection search to find a zero-crossing to approximate the shortest successful perturbation.
- Add an additional clean loss during training to make the loss landscape less flat.
- Discuss standard AT from a perspective of margin, and conclude that when epsilon is large it will maximise the upper bound of the margin and is not necessarily helpful.

[Clustering Effect of Adversarial Robust Models (NeurIPS 2021)](https://papers.nips.cc/paper/2021/hash/f770b62bc8f42a0b66751fe636fc6eb0-Abstract.html)
- Define semantic superclasses and find adversarially trained models give consistent semantic clustering effects.
- Extract a linear sub-network using backward propagation, and think it has a connection with the non-linear model in class-wise direction.
- Claim that the non-linear components are example-wise, while linear components are generally applied to all examples.
- Apply the clustering effect to domain adaptation, with which I'm not quite familiar.
- Propose a regularisation term to enhance the clustering effect, which improves robustness against both white/black-box attack and even the standard accuracy.
- Adversarial examples achieved by attacking adversarially trained models show similar clustering effect in attack successful rate.

[Adversarial Logit Pairing (arXiv 1803)](https://arxiv.org/abs/1803.06373)
- Add a logit pairing term to both adversarial examples and their counterparts and two random clean examples.
- Achieve SOTA black/white-box robustness after adversarial logit pairing.
- Find clean logit pairing yields comparable adversarial robustness with significant training efficiency.
- Argue that the logit pairing term works by encouraging small logit values (not that confident), just like but stronger than label-smoothing.

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
[Adversarial Training for Free! (arXiv 1904, NeurIPS 2019)](https://arxiv.org/abs/1904.12843)


