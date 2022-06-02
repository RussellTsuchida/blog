---
title: "Principal-Component-Analysis"
date: 2022-06-02
---

First introductions to Principal component analysis are usually delivered via so-called maximum variance or minimum reprojection error formulations, both of with lead to eigenvalue problems. Another useful view is that of probabilistic PCA, which is the subject of this post. The probabilistic view offers a number of benefits and generalisations. Two useful sources of information are chapter 12.2 of [Bishop's book](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf) and chapter 10.7 of [Mathematics for Machine Learning](https://mml-book.github.io/book/mml-book.pdf).

## A Graphical model
We are given access to a dataset $$X \in \mathbb{R}^{N \times d}$$, which represents $$N$$ vectors $$x_i \in \mathbb{R}^d, \quad 1 \leq i \leq N$$. Let $$ l < d$$. We assume that the observed data are samples from a conditionally multivariate Gaussian distribution given some latent variables $$Z \in \mathbb{R}^{N \times l}$$, representing $$N$$ vectors $$z_i \in \mathbb{R}^l, \quad 1 \leq i \leq N$$. The expected value of the Gaussian is $$ Z W^\top + 1_{N \times 1} \mu^\top $$ for some deterministic parameters $$W \in \mathbb{R}^{d \times l}$$ and $$\mu \in \mathbb{R}^{d}$$. The covariance matrix of the Gaussian is diagonal with deterministic entry $$\sigma^2$$. The distribution over $$Z$$ is an uncorrelated standard Gaussian. This leads to the graphical representation as shown.

## Parameter estimation and inference
Given our model, we may estimate the values of $$W$$ and $$\mu$$ by maximum likelihood estimation, and infer the distribution over $$Z$$ by examining the posterior. Since the Gaussian distribution is in some sense closed under marginalisation and conditioning, the marginal likelihood and posterior can be found in closed form. These are

$$ p(x_i \mid W, \mu, \sigma^2 ) = \mathcal{N} (\mu, W W^\top + \sigma^2 I ) $$

and

$$ p(z_i \mid x_i, W, \mu, \sigma^2) = \mathcal{N}(m, C), \quad m = W^\top(W W^\top + \sigma^2 I)^{-1}(x_i - \mu), \quad C = I = W^\top(W W^\top + \sigma^2 I)^{-1} W $$
