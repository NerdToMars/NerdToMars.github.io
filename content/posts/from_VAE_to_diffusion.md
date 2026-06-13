---
title: "From VAE to Diffusion"
date: 2025-08-17
draft: true
tags: ["machine learning", "generative models", "diffusion", "VAE"]
---

## Introduction

In this post, I will explore the journey from Variational Autoencoders (VAEs) to Diffusion Models and code a simple diffusion model from scratch using Rust Burn library.

Problem statement:

Given a MNIST handwritten digit $\mathbf{X}$, and the probability of $p(y)$, $y$ could be a digit from 0 to 9, or a non-digit. 

There are 2 tasks:
1. Maximum a Posteriori (MAP) inference: What s the most likely image $\mathbf{X}$ given the digit $y$?

2. Marginal inference: What is the probability of $p(y)$ given the image $\mathbf{X}$? 

## VAE
Let's refine the problem statement:

Define $\mathbf{X}$ is a 28x28 grayscale image, and $\mathbf{z}$ is a 2-dimensional latent vector. In other words, we want to encode the image $\mathbf{X}$ into a 2-dimensional latent vector $\mathbf{z}$. 

Define a probability distribution $p(\mathbf{X}, \mathbf{z})$ as a joint distribution of the image $\mathbf{X}$ and the latent vector $\mathbf{z}$. 


Why we called it variational? why why why? 


### What are the tasks we want to solve?

1. The parameter $\theta$ of the distribution $p(\mathbf{X}, \mathbf{z}; \theta)$
2. approximate the posterior inference over z: given a observation $\mathbf{X}$, find the latent code $\mathbf{z}$ that maximizes the probability $p(\mathbf{z} | \mathbf{X})$.
3. marginal inference over x: given a latent code $\mathbf{z}$, find the image $\mathbf{X}$ that maximizes the probability $p(\mathbf{X} | \mathbf{z})$.  (or give a image with missing pixels, how to fill in the missing pixels?)


### Variational Inference

VI is a method to approximate the posterior distribution $p(\mathbf{z} | \mathbf{X}; \theta)$ by a simpler distribution $q(\mathbf{z} | \mathbf{X}; \phi)$. 

So what's the difference between $p(\mathbf{X}, \mathbf{z}; \theta)$ and $q(\mathbf{z} | \mathbf{X}; \phi)$?  That's what EBLO is doing. 


#### EBLO

$$
\log p(\mathbf{X}) = \log \int p(\mathbf{X}, \mathbf{z}) d\mathbf{z} 

\newline

= \log p(\mathbf{X}) * \int q(\mathbf{z} | \mathbf{X}; \phi) d\mathbf{z}

\newline

= \int q(\mathbf{z} | \mathbf{X}; \phi) * \log p(\mathbf{X}) d\mathbf{z}

\newline

= \mathbb{E}_{q(\mathbf{z} | \mathbf{X}; \phi)} \left[\log p(\mathbf{X})\right]

\newline

= \mathbb{E}_{q(\mathbf{z} | \mathbf{X}; \phi)} \left[\log \frac{ p(\mathbf{X}, \mathbf{z})}{p(\mathbf{z} | \mathbf{X})}\right]

\newline

= \mathbb{E}_{q(\mathbf{z} | \mathbf{X}; \phi)} \left[ \log \frac{p(\mathbf{X}, \mathbf{z}) q()}{p(\mathbf{z} | \mathbf{X})q()} \right]

\newline 

\ge \mathbb{E}_{q(\mathbf{z} | \mathbf{X}; \phi)} \left[ \log \frac{p(\mathbf{})}{}  \right]

\newline

= \log \int \frac{p(\mathbf{X}, \mathbf{z})}{q(\mathbf{z} | \mathbf{X})} q(\mathbf{z} | \mathbf{X}) d\mathbf{z}

\newline

=  \log \mathbb{E}_{q(\mathbf{z} | \mathbf{X}; \phi)} \left[\frac{p(\mathbf{X}, \mathbf{z})}{q(\mathbf{z} | \mathbf{X}; \phi)}\right]
$$





## Diffusion







