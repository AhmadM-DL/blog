---
layout: post
title: On Unsupervised Deep Learning
date: 2020-06-24 13:32:20 +0200
description: A simple survey to unsupervised deep learning 
img: unsupervised.jpg 
fig-caption: <span>Photo by <a href="https://www.pexels.com/@fotios-photos?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels">Lisa Fotios</a> on <a href="https://www.pexels.com/photo/child-playing-with-lego-blocks-5435599/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels">Pexels</a></span>
tags: [Deep Learning, Unsupervised]
---

Deep Learning has shown significant improvements over traditional machine learning approaches in the domain of Visual Data. However, its breakthrough has been demonstrated mostly from the Supervised Learning perspective. Supervised Learning demands expansive annotation of data and ignores the tremendously massive amount of easily available unlabeled data. Recently Unsupervised Learning has gained researchers’ attention to make use of the available unlabeled data. In this short article I will try to shed light on the Unsupervised Deep Learning movement and researchers ways of attacking the problem.
{: .text-justify}

>"This is what is going to allow our AI systems to go to the next level" Yann Lecun referring to **Self-Supervised Learning** at [AAAI 2020 ACM Turning Award Live event](https://www.zdnet.com/article/deep-learning-godfathers-bengio-hinton-and-lecun-say-the-field-can-fix-its-flaws/)

### Unsupervised First

Although the publicity of supervised Deep Learning has shadowed the unsupervised deep learning movement, unsupervised deep learning has always existed alongside supervised learning. While Yann Lecun [1] was working on applied supervised deep learning using a convolutional neural network, Geoffrey Hinton [2, 3] was working on learning representations without supervision using generative models. When his student Krizhevsky was working on AlexNet for ImageNet, Hinton was [ resistant to the idea ](https://qz.com/1307091/the-inside-story-of-how-ai-got-good-enough-to-dominate-silicon-valley/) as he thought that machines should learn labels by itself.
{: .text-justify}

Since 2015 the domain of unsupervised deep learning has gained researchers attention and the number of research papers quickly increased. The approaches tackling the domain started to form sub-domains each tackling it from a different perspective. We can divide the domain into 4 categories of research:
{: .text-justify}

- Clustering-Based
- Sample-Specificity-Based
- Self-Supervised
- Generative Models.

 With Clustering-Based and Self-Supervised being the most attracting and having the largest number of publications. The movement started initially with Restricted Boltzmann Machines (RBMs) [4] and Deep Belief Networks (DBNs) [2] as generative models to extract hierarchical representation of data. Then by 2015 the Clustering-Based approaches followed along with Self-Supervised movement in parallel. Recently, a handful of Sample-Specificity-Based approaches have been published.
{: .text-justify}

![Unsupervised Deep Learning]({{site.baseurl}}/assets/img//unsupervised%20deep%20learning.png)
{: .text-center}
Unsupervised Deep Learning Coarse Taxonomy
{: .text-center}

### Unsupervised Deep Learning Approaches

#### Clustering Based

Clustering-Based Unsupervised Deep Learning simply extends traditional clustering methods by adopting neural networks to learn clustering-friendly representations. We can see them as a neural network that incorporates two losses rather than one, a Network Loss and a Clustering Loss. A hyper-parameter is usually introduced to tradeoff between the losses:
{: .text-justify}

![Network Losses]({{site.baseurl}}/assets/img//network_loss.PNG)
{: .text-center}

The choice of the network loss and the clustering loss leads to a variety of approaches. From the clustering loss perspective researchers used used k-means, clustering assignment hardening,  agglomerative clustering, locality-preserving loss, group sparsity loss along with k-means, etc.
{: .text-justify}

From the Network loss perspective the majority used Autoencoders reconstruction loss. Others used Variational Autoencoders (VAE) and Generative Adversarial Networks (GANs) losses. On the other hand, some neglected the network loss and used cluster assignments to fine-tune the network.
{: .text-justify}

A comprehensive survey for clustering-based approaches can be found in [5, 6].
{: .text-justify}

![Clustering-Based Unsupervised Deep Learning]({{site.baseurl}}/assets/img//clustering_unsuervised_deep_learning.png)
Clustering-Based Unsupervised Deep Learning. Image from [6].
{: .text-center}

#### Self-Supervised

In a community parallel to Clustering-Based approaches, Self-Supervised Deep Learning approaches have been also gaining attention and momentum. Rather than introducing new losses to deep models, self-supervised approaches generate pseudo labels for the models to be trained on. The idea is to propose a pretext task – a task that doesn’t require human annotation (i.e. coloring) and it's training data can be automatically generated - for the network to solve. By training the network on the proposed task objective functions it learns features that are relevant for an actual downstream task.
{: .text-justify}

![The general workflow of self-supervised deep learning]({{site.baseurl}}/assets/img//self-supervised-pipeline.png)
{: .text-center}
The general workflow of self-supervised deep learning. Image from [7].
{: .text-center}

To the date of writing this article, several pretext tasks have been proposed. Recently, the authors in [7] have compiled a comprehensive survey on self-supervised learning. The range of proposed tasks varies considerably starting by tasks that solely depend on 3-channel Images and not ending in ones that depend on videos, artificially generated data (using game-engines), artificially generated labels (using hardcoded programs), and more-than-3-channels images (i.e. images with depth).
{: .text-justify}

Examples of tasks that acts on 3-channels images are:

- Predict the relative position between image patches.
- Coloring grayscale images
- In-painting occluded image patches
- Invariance against augmentation
- Cross channel prediction (predict color channel from grayscale and vice-versa)
- Solving a jigsaw puzzle
- Counting objects
- Predicting image rotation
- ...

![Self Supervised Tasks]({{site.baseurl}}/assets/img//self_supervised_tasks.png)
{: .text-center}
Examples of proposed self supervised pretext tasks. Clockwise from top left: Predict Relative Position, In-painting,  Predict cross channel, Solving Jigsaw Puzzle.  Images from [7].
{: .text-center}

#### Generative Models

Generative models were the first to be proposed in the domain of unsupervised deep learning. Rather than learning by discrimination the models are trained to reproduce images and are penalized by the quality of generated images.
{: .text-justify}

Earlier methods included Deep Belief Networks (DBNs) and Restricted Boltzmann Machines RBMs [2-4]. DBNs have fallen of favor and rarely used [8] compared to other Generative Models such as Autoencoders [9,10], Variational Autoencoders [11], and Generative Adversarial Networks (GANs) [12].
{: .text-justify}

Although the motivation behind these approaches is to model the data and be able to generate it, the representation learned during training generative models can be exploited for downstream tasks. Note that Generative models are frequently used for network loss in clustering-based unsupervised deep learning.
{: .text-justify}

![Generative Adversarial Network]({{site.baseurl}}/assets/img//GAN.png)
{: .text-center}
The infamous GAN network. Image from [7].
{: .text-center}

#### Sample Specificity Based Approaches

Sample-Specificity-Based approaches have gone with clustering to the extreme where they consider each instance as a class that the network should learn to discriminate it. The number of publications concerning this approach is small.
{: .text-justify}

Initially [13] proposed Exemplar-CNN in which they extract patches from images and then create a surrogate class for each patch by augmenting it. The model is trained to discriminate between those surrogate classes. [14] proposed to map image instances to a fixed distribution of random vectors. [15] directly transferred the supervised learning approach by giving a label for each instance however they used a non-parametric softmax alternative and approximated it using noise-contrastive estimation (NCE).
{: .text-justify}

### Recap

This was a coarse introduction to unsupervised deep learning. If you are interested in more details, I recommend to check out the references. I would like to hear any constructive feedback.
{: .text-justify}

### References

[1] Y. Lecun, L. Bottou, Y. Bengio, and P. Haffner, “Gradient-based learning applied to document recognition,” Proc. IEEE.

[2] G. E. Hinton, S. Osindero, and Y.-W. Teh, “A Fast Learning Algorithm for Deep Belief Nets,” Neural Comput.

[3] R. Memisevic and G. Hinton, “Unsupervised Learning of Image Transformations,” in 2007 IEEE Conference on Computer Vision and Pattern Recognition.

[4] G. E. Hinton, “A Practical Guide to Training Restricted Boltzmann Machines,” in Neural Networks: Tricks of the Trade: Second Edition.

[5] E. Aljalbout, V. Golkov, Y. Siddiqui, M. Strobel, and D. Cremers, “Clustering with Deep Learning: Taxonomy and New Methods,” ArXiv.

[6] E. Min, X. Guo, Q. Liu, G. Zhang, J. Cui, and J. Long, “A Survey of Clustering With Deep Learning: From the Perspective of Network Architecture,” IEEE.

[7] L. Jing and Y. Tian, “Self-supervised Visual Feature Learning with Deep Neural Networks: A Survey,” ArXiv.

[8] I. Goodfellow, Y. Bengio, and A. Courville, Deep Learning. MIT Press, 2016.

[9] P. Vincent, H. Larochelle, I. Lajoie, Y. Bengio, and P.-A. Manzagol, “Stacked Denoising Autoencoders: Learning Useful Representations in a Deep Network with a Local Denoising Criterion,”.

[10] P. Vincent, H. Larochelle, Y. Bengio, and P.-A. Manzagol, “Extracting and composing robust features with denoising autoencoders,” in Proceedings of the 25th international conference on Machine learning - ICML ’08.

[11] D. P. Kingma and M. Welling, “Auto-Encoding Variational Bayes,” ArXiv.

[12] I. J. Goodfellow et al., “Generative Adversarial Networks,” ArXiv.

[13] A. Dosovitskiy, P. Fischer, J. T. Springenberg, M. Riedmiller, and T. Brox, “Discriminative Unsupervised Feature Learning with Exemplar Convolutional Neural Networks,” ArXiv.

[14] P. Bojanowski and A. Joulin, “Unsupervised Learning by Predicting Noise,” ArXiv.

[15] Z. Wu, Y. Xiong, S. Yu, and D. Lin, “Unsupervised Feature Learning via Non-Parametric Instance-level Discrimination,” ArXiv.
