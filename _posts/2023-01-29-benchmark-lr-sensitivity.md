---
layout: post
title: "[Paper] Benchmarking Gradient Based Optimizers’ Sensitivity to Learning Rate"
excerpt: "This post perfroms a comparative study between multiple optimizers and how sensitive it behaves w.r.t. learning rate."
tags: [Optimization, Code, Deep Learning, Neural Network]
categories: [Optimization, Mathematics, Machine Learning]
share: true
link: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4318767
comments: true
mathjax: false
---

Initial choice of Learning Rate is a key part of gradient based methods and has a great effect on the performance of the Deep Learning Model.This paper studies the behavior of multiple gradient based optimization algorithm which are commonly used in Deep Learning and compare their performance on various learning rate. As observed popular choice of optimization algorithms are highly sensitive to various choice of learning rates. Our goal is to find which optimizer has an edge over others for a specific setting. We look at two datasets namely MNIST and CIFAR10 for benchmarking. The results are quite surprising, and it will help us to choose a learning rate more efficiently.

## Paper Link

### [Preprints.org (link)](https://www.preprints.org/manuscript/202301.0118/v1)

<iframe width="100%" height="400" src="https://www.preprints.org/manuscript/202301.0118/v1" allowfullscreen="allowfullscreen"></iframe>

### [SSRN (link)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4318767)
<iframe width="100%" height="400" src="https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4318767" allowfullscreen="allowfullscreen"></iframe>

## GitHub code link

Link: [https://github.com/rehanguha/Learning-Rate-Sensitivity](https://github.com/rehanguha/Learning-Rate-Sensitivity)
