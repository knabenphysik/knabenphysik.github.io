---
layout: post
title:  "Latent Space"
excerpt: "before touch neural net code, understand your data first is a good idea"
tags: ["generative ai"]
comments: true
---

The term _generative AI_ refers to computational techniques that are capable of generating seemingly new, meaningful content such as text, images, or audio from analyzing patterns (training) in existing data. To date, we can already see the impact of generative AI on work productivity. The question one must ask is "how" this generation of new information works.

Consider the famous autoencoder (AE) which consists of two parts: the encoder and the decoder. The encoder creates a concise and compact representation of the image, often referred to as the latent space representation. The decoder reconstructs the image back from these latent space representations. 

Adversarial generative learning on the other hand involves two networks. One of the networks is a generator that is a typical decoder. The generator samples from a random latent distribution and generates an image. The second network is a discriminator that tries to predict if an input image was generated by the generator network or was sampled from a dataset.

One key component or concept in both AE and adversarial generative learning is what we call _latent space_. Generative AI usually sample data from a distribution on a _latent space_. The rationale behind GANs is to learn the mapping from a latent distribution to the real data through adversarial training. Where as, autoencoders generate samples that tend to be close to the mean of the samples that are represented by the latent representations.

## Latent variables

The variables that are not directly observed but are rather inferred (through a mathematical model) from other variables that are observed (directly measured).[^1] Latent variables is also called hidden variables or unobserved variables.[^2]

The primary role of the latent variables is to allow a complicated distribution over the observed variables to be _represented_ in terms of a model constructed from simpler (typically exponential family) conditional distributions. For instance, consider an object recognition task in which each observed data point _corresponds_ to an image (comprising a vector of pixel intensities) of one of the objects. In this case, the latent variables might have an interpretation as the position and orientation of the object. This _representation_ must then represent the **features** of the original data distribution.


## Latent Space

Latent variables, despite serving distinct purposes, these representations are all vector spaces of reduced dimensionality (relative to the input), intended to produce more general features that helpfully **characterize** the input. These representations are often referred to as _**latent spaces**_.

Mathematically, the latent space should not then be seen as a linear euclidean space, but rather as a curved space (abstract multidimensional).[^3]

Now, you can say that latent space is like an abstract multidimensional space that encodes a meaningful internal representation of externally observed variables. Samples that are similar in the external world are positioned close to each other in the latent space.

So, the external world (or our raw data) is transform to a suitable internal representation or feature vector in latent space. 

## Outlook

You can say that latent spaces are important mainly in two view:

- they can provide insights into the data, revealing important relationships we are unaware of
- can serve as feature spaces for downstream machine learning applications

Thus, the usage of latent space in generative modeling aims to infer some actual data distribution is sound.

## Reference

[^1]: Wei Qi Yan, [Computational Methods for Deep Learning: Theoretic, Practice and Applications](https://link.springer.com/book/10.1007/978-3-030-61081-4),2021
[^2]: Christopher M. Bishop, [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf),2006
[^3]: G. Arvanitidis, L. K. Hansen & S. Hauberg, [Latent Space Oddity: on the Curvature of Deep Generative Models](https://arxiv.org/abs/1710.11379), 2017
