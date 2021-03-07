---
layout: post
title: The Rise of Software 2.0
date: 2021-01-04 13:32:20 +0200
last_modified_at:  2021-01-04 13:32:20 +0200
excerpt: How Deep Learning Is Reshaping Software Production Industry
categories: Non-Technical 
image:
  feature: rise-ai.jpg
  topPosition: 0px
tags: Deep Learning, Startup, Neural Networks, Software
bgContrast: dark
bgGradientOpacity: darker
syntaxHighlighter: no
---

At some point in my research, I was studying the interaction between Software Engineering (SE) and Artificial Intelligence (AI) in the literature. I passed by [Erik Meijer](https://www.linkedin.com/in/erikmeijer1/) keynote at the FSE'18 conference. The keynote was titled "[Behind every great deep learning framework is an even greater programming languages concept](https://dl.acm.org/doi/abs/10.1145/3236024.3280855)". The talk illustrated the deep programming language principles behind Differentiable Programming, hoping to inspire the working Software 1.0 engineers to pay serious attention to the threats and opportunities of Software 2.0.
{: .text-justify}

[Andrej Karpathy](https://medium.com/@karpathy) defines software 2.0 as following "[Software 2.0](https://medium.com/@karpathy/software-2-0-a64152b37c35) can be written in much more abstract, human *unfriendly* language, such as the weights of a neural network. No human is involved in writing this code because there are a lot of weights (typical networks might have millions), and coding directly in weights is kind of hard".
{: .text-justify}

I personally see Software 2.0 as Deep Learning complementing traditional software engineering stack, so that we can build complex software we couldn't build before. I believe that software production has evolved from being pure software 1.0 to software 2.0 through an intermediate state called *Data Products*. This state came into existence when top software companies understood the business potential of Big Data and started building data products using machine learning. The below figure illustrates more my idea.
{: .text-justify}

![Software Products Evolution](../assets/img/s1tos2.png)
{: .text-center}
The 3 states of software production evolution. (Image by author)
{: .text-center}

In the below sections I will support my idea more by mentioning the characteristics of such products and give some real-life examples to them. Note that I won't discuss the software 1.0 products as they are well established.
{: .text-justify}

## Data Products

In the flow of explaining the reasons Data Science rose recently, Schutt and  O’Neil in [Doing Data Science Book](https://www.oreilly.com/library/view/doing-data-science/9781449363871/) argue that one major factor behind the interestingness of data is that data itself becomes building blocks of data products.
{: .text-justify}

In real life, those products can be Amazon recommendation systems that predict what would interest you as a client. Facebook recommendation systems that propose friendship possibilities. Netflix movie recommendation. What else? Google search query completion algorithm. Waze routing algorithm. The ranking algorithm behind Airbnb experiences. And the list goes on.
{: .text-justify}

I characterize such products by the following:

1. **They are secondary**. Not in the sense that they are not important but that they add value to the primary software product. Consider Airbnb experience ranking and recommendation algorithm. Airbnb's main software product is a platform where people can host residences or rent one. While running the platform for multiple years a huge amount of data is generated. Like all businesses, they decided to put this potential into action and increase the number of people buying experiences by recommending to them what most interests them.
{: .text-justify}

2. **They evolve**. While traditional software products evolve throughout time. Data Products evolve much faster. I won't be exaggerating if I said that every datafied user interaction with a data product will directly contribute to the product evolvement. When you rate a movie on Netflix, your action will slightly affect their recommender system. Such effects are aggregated across users. Schutt and O’Neil articulate it as following "We’re witnessing the beginning of a massive, culturally saturated feedback loop where our behavior changes the product and the product changes our behavior."
{: .text-justify}

3. **Based on Traditional ML**. Such products are mostly built using traditional Machine Learning algorithms that used to work well and are still working. Decision Trees, Support Vector Machines, Regression, etc.
{: .text-justify}

4. **Interpretability Matter**. A banker would be glad to have a decision tree model to predict the approval of personal loans for a person. This is because the model generates knowledge that can be formulated as a set of human-friendly rules. Such as "If the person is young, married, have a six-figure income then there is - according to training data - a 78% probability that he/she will default on loans." On the other hand, good luck convincing this banker to use the X state-of-the-art Neural-Networks-based Deep Learning model.
{: .text-justify}

5. **Medium R&D score.** If we consider traditional software to be Development more than Research (from a technical perspective), i.e. it resides on the D end of the R&D spectrum. Then Data products lays at the center of the R&D spectrum. The data product building cycle is not deterministic, you can't simply set milestones with delivery deadlines. It is a trial-and-error process. We choose N algorithms and try M hyperparameters and hope some of them achieve bushiness requirements. Although the Data Product Process is at the center of the R&D spectrum, it leans toward the D as it is always suitable to use off-the-shelf algorithms. And algorithmic innovation doesn't matter in most cases.
{: .text-justify}

I believe that those really describe Data Products or the intermediate state between software 1.0 and software 2.0. If there are any other characteristics in your mind please share them in the comments section. I would be glad to check them.
{: .text-justify}

## Software 2.0

Software 2.0 is Neural Networks. It is Deep Learning. It is Connectionist Machine Learning. It is machines learning complex concepts by aggregating simple computational units. Andrej Karpathy describes it will [here](https://medium.com/@karpathy/software-2-0-a64152b37c35). He also describes its characteristics and how it is compared to traditional software. To avoid redundancy I will focus more on giving real-world examples of such software than on characteristics.
{: .text-justify}

I will first mention some characteristics that contrast software 2.0 with Data Products.

1. **Based on Deep Learning**. Obviously. Unlike Data products software 2.0 products are based on contemporary deep learning models.
{: .text-justify}

2. **It is primary**. Unlike data products, Software 2.0 is not secondary. It is the core component of the software product and the actual business value.
{: .text-justify}

3. **Interpretability Doesn't Matter**. Yes, that is true. Interpretability doesn't matter. How come it doesn't matter and there is a research domain working on making deep learning models more interpretable? Well, it does matter for some safety-sensitive domains such as autonomous vehicles and medical applications. But for many other applications, it doesn't. As long the model output what is expected then kudos. This will be more evident with the product examples I will mention below.
{: .text-justify}

4. **High R&D score**. Software 2.0 leans more toward the R in the R&D spectrum. For every application, there are some tips and tricks that you need to innovate to achieve the best results compared to off-the-shelf models. There is always some algorithmic innovation happening in there. If you build a software 2.0 product in a given domain, then you will automatically become a domain expert developing niche expertise.
{: .text-justify}

## Software 2.0 examples

Here I will mention some real software 2.0 examples so that one can understand them first-hand.

### 1. [Prisma](https://prisma-ai.com/)

I think that many people have heard or used Prisma by now. Prisma is a photo-editing mobile application that uses neural networks and artificial intelligence to apply artistic effects to transform images. The app was created by Alexey Moiseenkov, Oleg Poyaganov, Ilya Frolov, Andrey Usoltsev, Aram Hardy. It was launched in June 2016 as a [free mobile app](https://en.wikipedia.org/wiki/Prisma_(app)). Prisma utilizes the recent [neural style transfer](https://en.wikipedia.org/wiki/Neural_Style_Transfer) technology to redraw an image using another image style. See how Prisma is a deep-learning-based product, how the underlying model interpretability doesn't matter, and how it certainly had a High R&D score. Won't this technology be cool for videos? [check out this](https://www.youtube.com/watch?v=Uxax5EKg0zA). Cool ha!
{: .text-justify}

!["Mona Lisa in the style of "Woman with a Hat""](../assets/img/mona_style.jpg)
{: .text-center}
Mona Lisa in the style of "Woman with a Hat" using neural style transfer. (Image Source Wikipedia)
{: .text-center}

### 2. [Rosebud.ai](https://www.rosebud.ai/)

Rosebud actually provides multiple software 2.0 products under the umbrella of AI-generated media. It uses the latest technological advances in Generative Adversarial Networks [GANs](https://en.wikipedia.org/wiki/Generative_adversarial_network) and [Deepfakes](https://en.wikipedia.org/wiki/Deepfake). Products such as [Tokkingheads](https://tokkingheads.com/) where you make an avatar or the face of a real person articulate your voice or a certain text. [Generative Photos](https://app.generative.photos/) where you can change human models' faces, race, and edit hair. [Faceloop](https://www.rosebud.ai/faceloop) where you can apply new filters to your faces such as changing the hair color, cartoonify, and age. You can try some!
{: .text-justify}

!["An example of deepfake technology"](./asets/img/../../../assets/img/amy_cage_deepfake.gif)
{: .text-center}
An example of deepfake technology: in a scene from Man of Steel, actress Amy Adams in the original (left)
is modified to have the face of actor Nicolas Cage (right) (Image Source Wikipedia)
{: .text-center}

### 3. [Lobe.ai](https://lobe.ai/)

Lobe.ai is not actually a software 2.0 product but a platform to build such products. It says the following "Lobe is a free, private desktop application that has everything you need to take your machine learning ideas from prototype to production." Using lobe, training deep learning models is like drinking a [sip of water](https://youtu.be/Mdcw3Sb98DA). Note that lobe is a Microsoft product.
{: .text-justify}

### 4. [Otter.ai](https://otter.ai)

Otter is a transcription AI-based service that can be used along with mainstream video conferencing software such as Zoom. I tried it to transcribe Hinton's (dubbed God Father of AI) "[Introduction to Deep Learning](https://www.youtube.com/watch?v=GJdWESd543Y)" Lecture. You can find the results [here](https://otter.ai/u/NWloZiFOHD1YdjOvsvvqzZzKZJY).
{: .text-justify}

### 5. [Grammarly](https://app.grammarly.com/)

I bet that the majority of readers already know Grammarly. Grammarly is an AI-based digital writing assistance application. This manuscript has been proofread by it.
{: .text-justify}

I listed here 5 software 2.0 products. As you can see the mentioned characteristics applies. A lot is happening out in the wild and many great startups are building great stuff using AI ([Check](https://www.businesswire.com/news/home/20190213005463/en/Xnor.ai-Unveils-First-Battery-free-Solar-AI-Technology-Enabling-a-New-Wave-of-Edge-AI-Computing) what xnor.ai have done!). However, I choose those 5 examples for simplicity and because they target end-users so that the reader can check them out. If you know of any cool software 2.0 app please share it in the comments below. I would like to hear about it. And if you found this article interesting don’t forget to support with a clap!
{: .text-justify}

I hope that I made the software 2.0 characteristics crystal clear. Now that you are inspired, why not build your own software 2.0 apps? What do you think would be possible to do using deep Learning that wasn't been possible before!
{: .text-justify}
