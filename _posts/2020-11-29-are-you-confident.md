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

<!-- <div class="img img--fullContainer img--14xLeading" style="background-image: url({{ site.baseurl_posts_img }}nn_decision_boundary.PNG);" width="50%" alt="A Neural Network decision boundary over a dataset"></div> -->
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

