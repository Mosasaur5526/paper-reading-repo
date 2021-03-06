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
[Relating Adversarially Robust Generalization to Flat Minima (arXiv 2104, ICCV 2021)](https://arxiv.org/abs/2104.04448)
- Find that robust error rate is not proportional to robust loss. In fact, robust loss may overfit more severely than robust error. Only when robust loss is under a threshold will it transfer to robust error rate more efficiently.
- Use some cases to show that judging flatness visually is difficult using, and point out that the biggest eigenvalues of Hessian does not reflect flatness among models because of its scale-variance.
- Emphasize that measuring flatness in robust loss is non-trivial and flatness in clean loss cannot be expected to correlate with robustness, and propose average-case/worst-case flatness as new stable metrics of flatness.
- Study a large amount of models and find that robustness strongly correlates with (average-case) flatness of the robust loss landscape in weight space.
- Point out that flatness improves robust generalisation by reducing both the robust generalisation gap and the impact of robust overfitting.

[Consistency Regularization for Adversarial Robustness (arXiv 2103, ICML workshop AML 2021, AAAI 2022)](https://arxiv.org/abs/2103.04623v3)
- Argue that data augmentation, even the naive cropping and flipping, does alleviate robust overfitting.
- Propose to match the predicted probabilities of the two adversarial samples augmented by two independent transformations.
- Find that most misclassified adversarial examples predicts the most confusing class and explain that this consistency regularisation works well thanks to the consistency of attacked directions.

[Exploring Memorization in Adversarial Training (arXiv 2106, ICLR 2022)](https://arxiv.org/abs/2106.01606)
- Train models using completely random labels using PGD-AT and TRADES, find the former cannot converge while the later can, and attribute this phenomenon to large gradient norm and variance of the adversarial term. This demonstrate that the model capacity is large enough to memorise all adversarial examples.
- State that most previous indicators of model generalisation ability cannot transfer to robust generalisation. Among them the flatness of loss landscape is the most reliable one.
- Explain robust overfitting using memorisation of the one-hot labels of "hard" adversarial examples that naturally lie close to the decision boundary.
- Propose to use temporal ensemble of predictions to mitigate robust overfitting and achieve the best result against previous methods.

[Robust Overfitting May Be Mitigated by Properly Learned Smoothening (ICLR 2021)](https://openreview.net/forum?id=qZzy5urZw9)
- Propose to use self-knowledge distillation (label smoothing) and stochastic weight averaging to mitigate robust overfitting.
- Validate its efficiency on multiple attack methods, model architectures, datasets and transferability.

 [On detecting adversarial perturbations (arXiv 1702, ICLR 2017)](https://arxiv.org/abs/1702.04267)
- Propose to detect adversarial examples with a binary classifier.
- Train the detector adversarially with a trade-off parameter against successful attack rate, since the adversarial examples can be crafted to evade the detection.
- The experiment result is confusing to me when sigma is large; maybe those misclassified clean examples are not counted. Anyway, it has obvious flaws in generalisation over different attack methods as pointed out in MagNet.

 [Adversarial Machine Learning at Scale (arXiv 1611, ICLR 2017)](https://arxiv.org/abs/1611.01236)
- Suggest to use mixed batch of clean examples and adversarial ones to scale adversarial training to large datasets.
- Suggest to use random value of epsilon to avoid overfitting on a specific epsilon.
- View adversarial training as a regulariser, which explains why the test error decreses on small datasets (this is outdated after stronger attacks has been widely applied to adversarial training) and increases on large datasets (underfitting is exacerbated).
- Discover the effect of label leaking: when the adversarial examples are constructed using true label, the transformation maybe too simple to be learnt leveraged for cheating by the model. This happens only when single step methods that make use of true label are used.
- Claim that large model capacity is helpful in elevating robustness and adversarial examples crafted by weak attack methods are more likely to transfer to other models.

 [An Eye for an Eye: Defending against Gradient-based Attacks with Gradients (arXiv 2202, CVPR 2022 submission)](https://arxiv.org/abs/2202.01117)
- Build on the autoencoder denoising framework to defend against adversarial examples, which is called TRN.
- Approximate the gradient map, though the target label is unknown, by concatenating gradient maps calculated using all possible labels. Find that all gradient maps are quite similar except the one calculated on the target label.
- Input both the adversarial image and the gradient map into the network and mix their features up to learn a benign perturbation to restore the image.
- Surprisingly, only using the gradient branch or the image branch also significantly outperform the robustness evaluated on adversarial training. This can be attribute to overfitting on a certain type of attack method.
- Has good generalisation over several gradient-based methods and resistance to BPDA.

 [MagNet: a Two-Pronged Defense against Adversarial Examples (arXiv 1705, ACM SIGSAC CCS 2017)](https://arxiv.org/abs/1705.09064)
- Defense against adversarial attack with a detector and a reformer (autoencoder), which are perfect compensations for each other. The detector eliminates those examples that too far away from the manifold, while the reformer project regular adversarial examples onto the normal manifold.
- Train different autoencoders by punishing and randomly pick one of them during inference. This randomness further prevent the defender from gray-box attack.
- Propose to use Jensen-Shannon entrophy between the output of clean examples and their adversarial counterparts to measure the reconstruction error.

[Enhancing the Transferability of Adversarial Attacks through Variance Tuning (arXiv 2103, CVPR 2021)](https://arxiv.org/abs/2103.15571)
- Propose to boost the transferability of adversarial examples by considering gradient variance in the neighbourhood of last attack step.
- Do not make any comments on understanding why it works. It is true that this makes the gradient more stable; however, I don't think the algorithm makes sense.

[Witches' Brew: Industrial Scale Data Poisoning via Gradient Matching (arXiv 2009, ICLR 2021)](https://arxiv.org/abs/2009.02276)
- Propose to insert malicious gradient into the training process to misclassify a set of training data, without harming the accuracy on untargeted validation set.
- The poisoning perturbs only a small subset of training examples, aligns their gradients with an adversarial target direction, and optimises the cosine similarity to do this.
- Use random start, ensemble of models and data augmentation techniques during the poisoning to counteract the adverse effect brought by them during test time and to boost the transferability among different network architectures.
- Note that this is not a harmful poisoning that degrades general validation performance. Instead, it maintains validation accuracy.
- Only discuss a small portion of poisoned dataset (1% ~ 6%) and several target images (1 ~ 16) in the appendix. In fact, the method already have a very small success rate when scaled to more than 6 images, and a higher portion will not always help.

[Are Adversarial Examples Created Equal? A Learnable Weighted Minimax Risk for Robustness under Non-uniform Attacks (arXiv 2010, AAAI 2021)](https://arxiv.org/abs/2010.12989)
- Point out that different adversarial examples have different vulnerability and the equally weighted loss is a biased estimator of the test dataset distribution.
- Propose to use exponential reweighting in the loss, not only in training but also in generating the adversarial examples (equivalent to dynamically adjusting step size according to the weight).
- Simultaneously suggest the attacker to make use of the margin information by using the same strategy of reweighting when setting step size.

[Geometry-aware Instance-reweighted Adversarial Training (arXiv 2010, ICLR 2021)](https://arxiv.org/abs/2010.01736)
- Restate that adversarial training requires larger model capacity and more epochs to achieve low loss on the training set, and believe within limited model capacity they should carefully fine-tune the boundary.
- Pay attention to the easily attackable examples and claim equal weight to all examples will lead to an overfitting on guarded data, but I don't think so.
- Model the distance to the decision boundary using least PGD steps that successfully misclassifies the example, and heuristically assign large weights to the ones close to the boundary.

[Attacks Which Do Not Kill Training Make Adversarial Learning Stronger (arXiv 2002, ICML 2020)](https://arxiv.org/abs/2002.11242)
- Believe using strong adversarial attack at the beginning of AT "kills" the training because the adversarial examples are too strong and twist the decision boundary.
- Propose to use friendly adversarial examples, which has a small adversarial loss value but the misclassification on it is quite confident, for AT.
- Can be regarded as a kind of curriculum learning as the attack strength has been demonstrated to increase during the training process.
- Have sustainable natural accuracy and robustness against different attack norm bound compared with traditional AT.

Transcoders: A Better Alternative To Denoising Autoencoders (CVPR 2022 submission)
- Argue that auto-encoders fail to project adversarial images onto the latent manifold since it may have several closest candidates of projection and can be confused by the gradient.
- Propose transcoder for denoising. Instead of reconstructing the full image, it project an input to a representative image of each class and then send it into the classifier. It just works like a light module for adversarial detection.
- The experiments are quite simple that they only compare vanilla auto-encoder with the proposed method, without considering any other traditional defense.

[Learning Sample Reweighting for Adversarial Robustness (ICLR 2022 rejection)](https://openreview.net/forum?id=7zc05Ua_HOK)
- Notice that adversarial class, especially when perturbation radius is large, is not always consistent with the class that has the minimal margin according to logits.
- Propose multi-class margin according to the insight above, caring about margins from each class boundary regardless of logits order.
- Follow the framework of bilevel optimisation/meta-learning to train the auxiliary reweighting network, and the method is called BiLAW. Specifically, it characterises the quality of a example by the linear correlation between the gradients update of the model brought by the example and the validation set with pseudo update.
- Improve robustness against AA, but the improvement is only marginal.
- Find that the examples assigned with high weights are the ones even difficult for humans to recognise. However, I don't think think this trick really work because the assigned weights fluctuate in [0.4975, 0.5001], which is quite neglectable.

Revisiting Outer Optimization in Adversarial Training (CVPR 2022 submission)
- Point out that the convergence of momentum SGD optimiser heavily relies on the gradient norm and gradient variance of a batch. In AT, they are significantly larger than in standard training especially after a weight decay and deteriorate convergence.
- Propose ENGM optimiser to provably bound the gradient variance and norm, and achieve SOTA performance combined with SOTA AT techniques, e.g. AWP.
- Accelerate the optimisation by approximating the gradient norm (used for normalisation in the reweighting step) using the linear correlation between gradient norm at a specific examle and gradient norm of model parameters.
- Visualise the loss landscape at examples and find the ones optimised using ENGM is much smoother than vanilla optimisers.

[Double Descent in Adversarial Training: An Implicit Label Noise Perspective (arXiv 2110, ICLR 2022 rejection)](https://arxiv.org/abs/2110.03135)
- Observe double descent also in the setting of adversarial training after exponentially many epochs of training, and attribute the phenomenon to label noise.
- Propose the notion of implicit label noise, which depicts the bias between the assigned label distribution (pure one-hot label) and the perturbed true distribution of labels.
- Theoretically prove the existence of implicit label noise and that it can be mitigated by model probability with temperature scaling and interpolation. I fully cannot understand them, because the label distribution mismatch is a conjectural thing itself, and can never be bounded.
- The proposed method is just like a self-distillation, which consists of a teacher network and a student network.

[Data Quality Matters For Adversarial Training: An Empirical Study (arXiv 2101, ICLR 2022 rejection)](https://arxiv.org/abs/2102.07437)
- Define high/low-quality data by stability of misclassification during adversarial training, and find that the rank of the examples upon this is quite stable among different datasets and models.
- Attribute robust overfitting, robust overestimation and robustness-accuracy trade-off to low-quality data.
- Demonstrate that low-quality examples are closer to decision boundary so their epsilon-ball are easily to overlap. Therefore they may only twist the decision boundary to confuse gradient-based attack methods.

[Robust Unlearnable Examples: Protecting Data Privacy Against Adversarial Learning (ICLR 2022)](https://openreview.net/forum?id=baUQQPwQiAg)
- Emphasise that the conferred unlearnability works because they provide poor training error. However, when adversarial training is applied, the training error reappears to be non-trivial, making the poisoned examples learnable.
- Propose the same min-min-max training objective as AVDIN.
- Enhance the stability against data augmentation techniques using gradient approximation over transformation distribution as proposed years ago to boost the robustness of adversarial examples.
- Achieve good performance against adversarial training but only considers relatively small perturbations (i.e. no larger than 4/255) when AT is applied.

[ZeroGrad : Mitigating and Explaining Catastrophic Overfitting in FGSM Adversarial Training (arXiv 2103)](https://arxiv.org/abs/2103.15476)
- Observe a significant change in parameters when catastrophic overfitting happens.
- Provide a proof about the sudden dramatic change by prove the existence of a gigantic gradient value. However, I think this claim is largely unconvincing, as it hypothesises an exact zero gradient that even being close to the local minima will not make the proof hold.
- Also obverse that when catastrophic overfitting occurs, MSE of difference in batch perturbation will exhibit a pattern of sudden increase.
- Propose ZeroGrad and MultiGrad, which removes small (by setting a proportion) and sensitive (sign changing frequently, voted by multiple random samples, can run parallelly) gradient values respectively.
- Successfully avoid catastrophic overfitting and achieve good performance, but ironically, it still even falls behind PGD-2.

[Adversarial examples make strong poisons (arXiv 2106, NeurIPS 2021)](https://arxiv.org/abs/2106.10807)
- Stress that adversarial training is totally different from training directly on fixed (adversarial) examples, which is devastating since the model will only fit the poisoned data.
- Generate poisons simply use adversarial attack on a pre-trained models on clean data, and state their method's priority to Wang's double minimisation is that it does not require access to the entire training set which may be impractical.
- Find the class targeted attack is significantly effective than untargeted attack and attribute this phenomenon to the later's perturbing samples into a limited set of labels which is not discriminatively useful for a network and is thus ignored. On the contrary, targeted attack ensures that adversarial features is associated with incorrect labels.
- Reproduce Madry's famous experiment and verify that targeted attack indeed instill non-robust features of the target class into the example. 
- Argue that such property of explicit label mapping won't raise security problem if the crafting model is unknown to the attacker, but I think it doesn't hold much water, because such a pattern is fixed and can be trivially reassigned to correct ones.

[Fooling Adversarial Training with Inducing Noise (arXiv 2111, ICLR 2022 rejection)](https://arxiv.org/abs/2111.10130)
- Find previous methods making examples unlearnable is far from effective when adversarial training is applied that they only disables non-robust features rather than robust features that adversarial trainig relies on.
- Due to necessity of robust features, they select adversarially trainied models as a surrogate to craft adversarially unlearnable examples.
- Propose NextCycle and NearSwap strategies to force consistent lable bias in the inner minimisation, which is proved to be effective against random selection and most/least likely labels through experiments.
- Propose IAT training strategy, which iteratively generates poisoned examples and adversarially trains the model on the poisoned dataset. The point is they intend to close the gap between a model trained from scratch and a pre-trained model.
- Name the proposed method as ADVIN and it significantly decreases the robust accuracy though with advesarial training to nearly zero, and reduces natural accuracy by a large margin compared with previous methods.
- Analyse the effect of generating poisons only on small patches. The winner is unexpectedly the size of 16 ?? 16 patches.
- I notice that the confusion matrix is very intriguing. From the philosophy of cryptography, a concrete label bias mapping will fail to conceal itself against (statistical) analysis. The fixed pattern may be discovered and leveraged.

[Boosting adversarial attacks with momentum (arXiv 1710, CVPR 2018)](https://arxiv.org/abs/1710.06081)
- Propose to combine momentum with iterative FGSM and believe that single step FGSM is prone to underfitting while iterative FGSM suffers from overfitting and momentum can save the later from getting stuck in a local maximum.
- Study how to attack an ensemble of models efficiently still using momentum, and find empirically the ensemble in logits performs better than the ensemble in predictions and the ensemble in loss.
- Trivially expand momentum attack to L2 norm bound and targeted settings.

[Learning to Learn Transferable Attack (arXiv 2112, AAAI 2022)](https://arxiv.org/abs/2112.06658)
- Generate different tasks using data augmentation and model augmentation. Specifically, simply use random resize and crop for data augmentation, and implement model augmentation using an extension of SGM which uses MGS method to fine-tune decay factors of different layers.
- Integrate meta-learning process into the pipeline, in which meta-training generates a perturbation using support set and meta-testing fine-tunes it on query set.
- Improve the transferability by a large margin in scenarios of attacking both undefended models as well as adversarially trained models.
- Combine LLTA with momentum and achieve new SOTA.

[Adversarial Risk and the Dangers of Evaluating Against Weak Attacks (arXiv 1802, ICML 2018)](https://arxiv.org/abs/1802.05666)
- Define and further analyse models' obscurity to adversaries, which is similar to obfuscated gradients. In fact, this is a concurrent work to the BPDA paper, which also got published in ICML 2018.
- Propose SPSA adversarial attack which does not leverage gradient information to investigate whether models claimed to be robust really are so.
- Specifically analyse 3 kinds of breakable defenses including non-differentiability, leveraging generative models (purification) and stochasticity and ensembling, and adversarial training is the only defense found not to be obscure and really robust. 

[Adversarial Robustness through Local Linearization (arXiv 1907, NeurIPS 2019)](https://arxiv.org/abs/1907.02610)
- Define a local linearity measure using taylor expansion and empirically verify that the loss surface becomes increasingly linear as we increase the number of PGD steps of the inner maximisation during adversarial training.
- Propose to minimise the error of approximation error and the gradient magnitude term, in which the direction where the error is minimised needs to be find using optimisation, but experimentally requires much less steps compared with common PGD.
- Due to strong local linearity enhanced by the proposed method, adversarial robustness degrades gracefully compared with other standard adversarially trained models, and suffers less from obfuscated gradients.

[An Alternative Surrogate Loss for PGD-based Adversarial Testing (arXiv 1910)](https://arxiv.org/abs/1910.09338)
- Find hyper-parameters of PGD variants need to be tunes for each specific case.
- Propose MultiTargeted attack which uses different surrogate loss functions for each class except the true class.
- In order to limit runtime complexity, the algorithm reduces number of restarts and may restrict the number of target classes to top-T ones.
- Discuss some simple cases where PGD is strictly weaker than MultiTargeted, and derive theorems for its superiority.

[Data Augmentation Can Improve Robustness (arXiv 2111, NeurIPS 2021)](https://arxiv.org/abs/2111.05328)
- Emphasise the importance of using external data in alleviating overfitting, and the importance of model weight averaging in further improving robustness.
- Use an example of Pad & Crop and MixUp to verify the hypothesis that model weight averaging helps robustness to a greater extent when robust accuracy between model iterations can be maintained.
- Through experiments, CutMix with weight averaging has been proved to be the most successful strategy since CutMix suffers the least from data augmentation.
- Point out that augmentations designed for robustness need to preserve low-level features by comparing blending-based data augmentation versus spatial composition techniques.
- Explain that model ensembling benefits from data diversity boosted by data augmentation.
- Implicitly compare common ensembling to weight averaging and claim that the later is the consequence of the compromise of computational efficiency and it degenerates to the former due to local linearity.

[Overfitting in adversarially robust deep learning (arXiv 2002, ICML 2020)](https://arxiv.org/abs/2002.11569)
- Discover the phenomenon that adversarial training results in severe overfitting compared with standard training. The best test error occurs in the middle of the training rather than at last, and there's a huge gap between them.
- Try various learning rate adjustment schemes, among which smoother learning rate schedule yields strictly worse performance than discrete piecewise decay schedule does. Cyclic training strategy actually leads to best last performance.
- Find that larger model capacity indeed improves robustness but the huge gap of overfitting still exists though training longer is usual viewed as increasing model complexity.
- Investigate a number of modern methods to prevent overfitting but only to find that no other method outperforms simple early stopping, unless considered under semi-supervised setting, though it still won't close the gap.

[Unlearnable Examples: Making Personal Data Unexploitable (arXiv 2101, ICLR 2021)](https://arxiv.org/abs/2101.04898)
- Change the min-max game in adversarial training to min-min, using the opposite of PGD to minimise the empirical risk too.
- Generate class-wise error-minimising noise by accumulating perturbations on all examples in a class.
- Find that class-wise noise is more effective in generating unlearnable examples compared with sample-wise noise.
- Though a random or error-maximising class-wise noise also works, early stopping can alleviate the unlearnability, so the error-minimising method is superior to them.
- Demonstrate its stability using one single unlearnable class, as well as its good transferability among different datasets.
- Show good resistance to several data augmentation techniques but it still lacks resistance against adversarial training.

[Defense against Adversarial Attacks Using High-Level Representation Guided Denoiser (arXiv 1712, CVPR 2018)](https://arxiv.org/abs/1712.02976)
- View adversarial defense from the perspective of denoising.
- Propose variants of U-Net which all perform denoising but constrain the loss at different layers, which are named PGD (at pixel level) and HGD (at the intermediate layers).
- HGD includes FGD, LGD, CGD. They add loss on CNN features, logit values and class labels respectively.
- Among them, LGD and CGD perform best, but the robustness is far from recent methods.

[Evaluating and Understanding the Robustness of Adversarial Logit Pairing (arXiv 1807, NeurIPS SECML 2018)](https://arxiv.org/abs/1807.10272)
- Argue that the model trained using ALP is not really robust with more PGD iterations.
- Plot loss landscapes around test data points which provide evidence that ALP sometimes induces a ???bumpier,??? depresses loss landscape tightly around the input points.

[Feature Denoising for Improving Adversarial Robustness (arXiv 1812, CVPR 2019)](https://arxiv.org/abs/1812.03411)
- Find that adversarial perturbation actually invokes noise in the feature, so feature denoising is important.
- Propose a new feature denoising block which consists of a denoising operation, a residual connection to maintain original features and a 1??1 convolution layer to adaptively control the trade-off between denoising and feature maintenance.
- The denoising operation has multiple implementations including non-local ones (Gaussian, dot product) and local ones (mean, median), among which Gaussian with embedding (inspired from attention mechanism) outperforms the others in experiments.
- Push the envelope by using lots of denoising blocks combined with a 2??2 subsampling to achieve SOTA under black-box setting.
- This is the first successful attempt on training robust classifiers on ImageNet against extremely strong PGD-2000 attack.

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

[Self-ensemble Adversarial Training for Improved Robustness (ICLR 2022)](https://openreview.net/forum?id=oU3aTsmeRQV)
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
- Show that gradient directions are orthogonal among different models but decision boundaries are well-aligned.
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
- Trust that random transformation is helpful to alleviate over-fitting.

[Overfitting in adversarially robust deep learning (arXiv 2002, ICML 2020)](https://arxiv.org/abs/2002.11569)
- Systematically study the overfitting in adversarial training and find this phenomenon is universal among different model sizes and other settings.
- Propose to use validation-based early stopping to capture the best checkpoint during training, which is quite effective. Particularly, the performance of the best checkpoint achieved by common adversarial training is on par with that achieved by TRADES.
- Try regularisation and several data augumentation methods that work on standard training to mitigate the robust overfitting, however, none of them succeed.
- State that robust overfitting is a phenomenon separate from double descent.


