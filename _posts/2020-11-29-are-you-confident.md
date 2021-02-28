---
layout: post
title: Are you confident about that, Neural Network?
date: 2020-11-29 13:32:20 +0200
excerpt: A simple introduction to uncertainty in deep learning 
img: uncertain_wally.jpg # Add image post (optional)
fig-caption: <span>Photo by <a href="https://unsplash.com/@ninjason?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Jason Leung</a> on <a href="https://unsplash.com/s/photos/thinking-robot?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
tags: [Deep Learning, Uncertainty, Neural Networks]
last_modified_at:  2014-12-15 01:00:00
categories: history
image:
  feature: walt-disney.jpg
  topPosition: 0px
bgContrast: dark
bgGradientOpacity: darker
syntaxHighlighter: no
---

On [14 Feb 2016](https://www.bbc.com/news/technology-35692845) Google self-driving car hit a bus. On [23 March 2018](https://www.wired.com/story/tesla-autopilot-self-driving-crash-california/) Tesla's Autopilot was involved in another deadly car crash. A big part of intelligence is not acting when one is uncertain and this has to be integrated into our artificial intelligence (AI) algorithms to avoid accidents. Regarding Neural Networks - which are the building blocks of the current Deep Learning AI wave and are being used in safety-critical applications - the problem is that they don't have an inherent uncertainty quantification. This semi-technical article discusses the matter and reports different approaches proposed to resolve the problem.
{: .text-justify}

> *A big part of intelligence is not acting when one is uncertain.*

### Discriminative vs Generative

Conventional Neural Networks have no inherent uncertainty quantification. This means it doesn't tell us how much it knows about the input and how confident it is about its output. Consider a network that is trained to classify dog and cat images. What will happen if you feed it a zebra image? It will respond with a dog/cat prediction. At the end of the day that what the network was trained for and it has only two outputs anyway. But that doesn't have to be the case. The network should be augmented with the concept of raising its hand and saying: this is something I am not trained for.
{: .text-justify}

It is good to know that there exist 2 different types of machine learning models. (1) **Discriminative** models which map inputs to their classes by finding decision boundaries. (2) **Generative** models which model the data distribution and find classes central tendency and how they are spread around centers.
{: .text-justify}

<div class="img img--fullContainer img--14xLeading" style="background-image: url({{ site.baseurl_posts_img }}nn_decision_boundary.PNG);" width="50%" alt="A Neural Network decision boundary over a dataset"></div>
{: .text-center}

A Neural Network decision boundary over a dataset as a discriminative machine learning model
{: .text-center}

Consider the figure above which showcase a dataset of two classes (orange and blue points) along with the decision boundary learned by a [neural network](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=gauss&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.43335&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false) over it. As you can see the data is distributed between [-6, 6] on both axes. Now consider a data point that is above the decision boundary (blue region) but very far from the training dataset say the point (50, 4). The network will classify it as blue despite it being very far from the original training set and with a high class score! This is an example of a **discriminative** machine learning model - Neural Network - failing to deal with out-of-domain images.
{: .text-justify}

On the other hand, **generative** models learn classes probability distribution as in the [Naive Bayes](https://jakevdp.github.io/PythonDataScienceHandbook/06.00-figure-code.html#Gaussian-Naive-Bayes) classifier. The figure below gives the intuition of such model predictions in action. In this case, if we feed the model a far data point it will output a very low class score for both classes as it is very far from both centers and beyond the data standard deviation. In this case, we can say that the model is uncertain about the decision and this point is probably out of the training data domain.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/naive_bayes_fitting.png" alt="A Neural Network decision boundary over a dataset" width="50%"> -->
{: .text-center}

A Naive Bayes output over a dataset as a generative machine learning model
{: .text-center}

All in all neural networks (convolutional ones as a result) as discriminative models don't have inherent uncertainty quantifications. Also, this nature makes them more susceptible to adversarial inputs (inputs intensionally and systemically perturbed to deceive neural networks) than other models like Radial Basis Function (RBF) networks. However, this is another topic I leave for the curious to check [1]. In the following section, we will see what did researchers have proposed to add uncertainty quantification to neural networks.
{: .text-justify}

### Problem Resolution

The below resolutions are retrieved from 2 research papers [2][3] and considered to be state-of-the-art methodologies. Although the resolutions are based on a sound theory I will explain them intuitively.
{: .text-justify}

#### Monte Carlo Dropout Sampling

The simplest of all resolutions is Monte Carlo Dropout (MC-Dropout) which feeds the input N times through the same network while tweaking the network slightly every time. The tweak is done by shutting down some (different each time) of the network nodes or neurons. This is called Dropout. Dropout is first introduced as a regularization trick to prevent the model from over-fitting during *training* [4]. However, in our case, we are using it during *inference* to sample different parameters distribution. The uncertainty in this case is the output variance. In other words, if the models output different classes or the same class with different class scores the model is considered uncertain about the input.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/guess_food_blindfold.jpg" alt="Guess the food blindfolded" width="50%"> -->
{: .text-center}

[Guess The Food Blindfolded Challenge](https://www.realplaycoalition.com/activities-for-kids/senses-game/) 
{: .text-center}

We can this as analogous to shutting down a person's different sensory organs while asking him to recognize objects (say blindfold his eyes one time, and cover his skin in another, and so on). If the person constantly keeps predicting the same object despite losing different sensory organs, this means the object is very familiar to him such that he can figure it using limited sensory organs. On the other hand, if he predicts different objects each time this means that the object is challenging for him. The below figure is a bonus illustration.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/nn_mc_dropout.jpg" alt="MCDropout Uncertanity Quantification" width="50%"> -->
{: .text-center}

If you are still curious about adversarial inputs, notice that a similar method has been used to detect them [5].
{: .text-justify}

#### Ensembles

Ensembles are simply training multiple neural networks with different random initialization and different shuffling of the training dataset. The uncertainty will be the variance of the models' predictions. The authors in [2] found it to be more accurate than MC-dropout in approximating the ground truth uncertainty; however, it is computationally expensive.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/young-old-ladies.png" alt="Different Perspective" width="50%"> -->
{: .text-center}

A group of people didn't agree on the content of image C. This means it is ambiguous.
{: .text-center}

This reminds me of Stephen Covey "The seven habits of highly effective people" in the paradigm shift section where he tells the story when he gave one group of his students the image (A - young lady) in the above figure and the image (B - old lady) for the other group. He then gave the image (C) to both and asked them to tell what is in it. Certainly, the first group said it was a young lady and the other said it was an old one. This because - like neural networks - each group has a different perspective (different position in the parameters manifold in case of neural networks). And the fact that the same image had different interpretations means it is of ambiguous and uncertain nature. The below figure is a bonus illustration.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/ensembles.PNG" alt="Ensembles" width="50%"> -->
{: .text-center}

#### Before we continue

Now that uncertainty is more familiar it is good to know two different types of uncertainties. (1) **Aleatoric** uncertainty captures the uncertainty in the data generating process, e.g., inherent randomness of a coin-flipping or measurement noise. This type of uncertainty cannot be reduced even if we collect more training data. (2) **Epistemic** uncertainty models the ignorance of the predictive model where it can be explained away given enough training data. The below [figure](https://towardsdatascience.com/my-deep-learning-model-says-sorry-i-dont-know-the-answer-that-s-absolutely-ok-50ffa562cb0b) explains the concept better. The orange braces corresponds to aleatoric uncertainty while the golden ones correspond to epistemic uncertainty resulting from lack of training data.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/uncertainty_types.png" alt="Uncertainty Types" width="50%"> -->
{: .text-center}

Type of uncertainties
{: .text-center}

So far the proposed methodologies target epistemic uncertainty as aleatoric one is already available as the class scores (this is different for regression though, check the references for further details).
{: .text-justify}

#### Sampling Free Uncertainty Quantification

The uncertainty quantifications presented earlier both depend on sampling a set of different model parameters (different networks). The authors in [3] proposed a sampling free one for regression using mixture neural networks (MDNs).
{: .text-justify}

##### Why MDNs

An MDN is a variant of a neural network proposed in 1994 by Christopher Bishop [6]. The author proposed the variant after proofing that conventional neural networks assume a normal distribution of the target data. In other words, if the target data was multi-modal in some region the network will fail to approximate it and learns the average. This a very important insight and should be considered by practitioners. Consider a self-driving cars dataset annotated by recording humans driving. For some similar scenarios, the humans might have behaved differently, some go left others go right. If we train the network to predict the steering angle in such scenario , it will learn to go straight (as each training sample will push the gradients toward them and the network will minimize the error by settling on the average). The below figure presents two toy datasets one with a normally distributed target and the other with a bimodal distributed one.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/normaility%20good%20bad.png" alt="Normal vs. Binormal fitting" width="50%"> -->
{: .text-center}

##### How is an MDN different

Rather than predicting the target directly, MDNs predicts a linear combination of **k** distributions. Rather than having one output neuron, it has 3*K ones. For each distribution, the network predicts a mean, a standard deviation, and the distribution weight. Increasing K gives the model more flexibility to model multi-model targets. The below figure illustrates an MDN.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/normal_mdn.png" alt="Normal Network vs. MDN" width="50%"> -->
{: .text-center}

Normal NN vs MDN
{: .text-center}

Since this article is about uncertainty quantification and not about MDNs the reader is asked to follow up about MDNs through the references.
{: .text-justify}

##### Back to the sampling free thing

Using MDNs the network is no more predicting one target but several distributions. The authors proposed to use the distributions mean of variances as an aleatoric uncertainty quantifier and the distributions variance of means as an epistemic uncertainty quantifier. How confusing.
{: .text-justify}

<!-- <img src="{{site.baseurl}}/assets/img/total%20variance%20-%20total%20expectation.png" alt="Total Variance and Total Expectation" width="50%"> -->
{: .text-center}

Illustration of Mean of variance and Variance of Means
{: .text-center}

The figure above illustrates both values. Consider an MDN with k=3 i.e. the network is predicting three distributions. The **Variance of Means** is how much the means of the three distributions away from each other if they are near to each other this means we have a low epistemic uncertainty and we are good to go. Otherwise, the network function should be inspected or delegated in the scenario of means being far from each other as it is encountering a high uncertainty situation. The **Mean of variance** on the other hand, is the average spreads of the three distributions. If all the distributions are widely spread then aleatoric uncertainty is high. If all are narrowly spread then aleatoric uncertainty is low. Check [this site](http://brenocon.com/totvar/) for an interactive demo.
{: .text-justify}

The authors proved that those two quantities respond to different ground truth uncertainty as stated. Note that unlike the previous quantifications this has not been tested on large scale problems.
{: .text-justify}

This might have been a wee bit heavy for some readers. Check out the below video to refresh your mind and see how humans can beat machines through out-of-domain inputs.
{: .text-justify}

{% include ytb.html id="KriBQVhsgZk" %}
{: .text-center}

### Conclusion

This was a simple introduction to uncertainty quantification in deep learning. Neural networks don't have inherent uncertainty quantification thus this called for the augmentation of such concept. We discussed three proposals to resolve this: MC-dropout, ensembles, and MDNs. The reader is referred to the references section for further details. Please don't hesitate to mention any feedback in the comments section below (you can comment as a guest), as this will help me optimize my writings.
{: .text-justify}

### References

[1] [Explaining And Harnessing Adversarial Examples, Goodfellow et. al.](https://arxiv.org/pdf/1412.6572.pdf)

[2] [Evaluating Scalable Bayesian Deep Learning Methods for Robust Computer Vision, Gustafsson et. al.](https://arxiv.org/abs/1906.01620)

[3] [Uncertainty-Aware Learning from Demonstration using Mixture Density Networks with Sampling-Free Variance Modeling, Choi et. al.](https://arxiv.org/abs/1709.02249)

[4] [Dropout: A Simple Way to Prevent Neural Networks from Overfitting, Srivastava et. al.](https://jmlr.org/papers/v15/srivastava14a.html)

[5] [DeepMutation: Mutation Testing of Deep Learning Systems, Lei et. al.](https://arxiv.org/abs/1805.05206)

[6] [Mixture density networks, Bishop](https://research.aston.ac.uk/en/publications/mixture-density-networks)
