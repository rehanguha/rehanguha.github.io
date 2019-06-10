---
layout: post
title: "Domain Adaptation / Sample Selection Bias"
excerpt: "Is the trained model with 90% accuracy is not performing as expected in Production Environment?"
categories: [Mathematics, Machine Learning, Statistics, Sampling]
tags: [Deep Learning, Error, Sampling, Distribution, Transfer Learning]
share: true
comments: true
mathjax: true
---

This post is about the common issue in bias is a mismatch between the training and the test distribution.
The issue of train/test mismatch has been widely studied under many different names:

1.  Covariate Shift
2.  Sample Selection Bias
3.  Domain Adaptation

### What's the Problem ?

**Let's start with a scenario:**

A learning algorithm $A$ with a probabilistic classifier $h$ is trained for voice recognition and translation for cars. The dataset was collected and was trained and tested and it is found that the accuracy of the model is very high, say 90%. But when the same model was thrown into the real-life situation the model accuracy came out to be approximately 60%.

  

**Why do you think this happened?**

Lets consider two distributions $D_{source}$  and $D_{test}$ and we have labelled training/testing data from $D_{source}$ say $x_1, x_2, x_3, ... , x_n$ totalling N samples. we also have K unlabeled Data i.e. the Realtime data $D_{test}$: $y_1, y_2, y_3, ... , y_n$

$D_{source}$  and $D_{test}$ are the distribution of source and test data. Mathematically we can write as probability distibution of source data as $\Pr_{source} or \Pr_{s}$ and Test data as $\Pr_{test} or \Pr_{t}$

Domain adaptation is a field associated with machine learning and transfer learning. This scenario arises when we aim at learning from a source data distribution a well performing model on a different target data distribution.

### How can you solve it ?

**Classic Test Error**

$$\epsilon_{test} \leqslant \hat{\epsilon}_{train} \ +\ \sqrt{\frac{Complexity}{n}}$$


Now we are going to reweigh the source distribution based on how similar they are to the test distribution. This is justified using the importance sampling for switching expectations.


$$Test Error => \epsilon _{t}(h) \ =\mathbb{E}_{\Pr_{t}[x]} \ \mathbb{E}_{\Pr[y|x]} \ [ h(x) \neq y]\\
\Longrightarrow \sum _{x}\Pr_{t}[x] \ \mathbb{E}_{\Pr[y|x]}[ h(x) \neq y]\\
\Longrightarrow \sum _{x}\frac{\Pr_{s}[x]}{\Pr_{s}[x]} \ \Pr_{t}[x] \ \mathbb{E}_{\Pr[y|x]} \ [ h(x) \neq y]\\
\Longrightarrow \sum _{x}\frac{\Pr_{t}[x]}{\Pr_{s}[x]} \ \Pr_{s}[x] \ \mathbb{E}_{\Pr[y|x]} \ [ h(x) \neq y]\\
\Longrightarrow \mathbb{E}_{\Pr_{s}[x]} \ \frac{\Pr_{t}[x]}{\Pr_{s}[x]} \ \mathbb{E}_{\Pr[y|x]} \ [ h(x) \neq y]$$


What we have achieved rewriting the test loss, which is an expectation over $\Pr_{t} $, as an expectation over $\Pr_{s}$ instead. This transformation was useful because we know $\Pr_{s}$ is a labeled data and not $\Pr_{t}$.

A learning algorithm $A$ with a probabilistic classifier $h$ should have a training set $x$ is weighted according to the ratio $\Pr_{t} : \Pr_{s}$. This makes sense: the classifier is told to pay more attention to the training examples that have a high probability under the new distribution, and less attention to training that has low probability under the new distribution.

Now the problem is that with this approach, we do not have access to $\Pr_{t}$ or $\Pr_{s}$ so we cannot compute this ratio. So we need to explicitly estimate the distribution i.e. know as Density Estimation. This is an incredibly difficult problem; far harder than the original adaptation problem.



We can try to estimate the ratio directly rather than separately estimating the two probability distributions.
All examples are drawn according to some fixed base distribution $\Pr[y|x]$. Some of these are selected for the new distribution, and some of them are selected for the old distribution. We will use a selection variable "$\sigma$" to address the above situation. We will define as below,

**Redefining Source Distribution (Adaptation)**

1) Draw from the test $\Pr_{t}[x]$

2) Select into the source with $\Pr[ \sigma=1\|x]$


$\Pr_{s}[x]\=\\frac{\Pr_{t}[x]\ \Pr[\sigma=1\|x]}{\Pr[\sigma =1]}$

$\Pr[ \sigma =1]$ is a regular normalizer. 


If we can estimate $\Pr[\sigma=1\|x]$, then the ratio that we sought, then we can compute the **Importance Ratio** as:
 
$\Pr_{s}[ x] \ =\ \frac{\Pr_{t}[ x] \ \Pr[ \sigma =1\ |\ x]}{\Pr[ \sigma =1]}\\
\\
\Longrightarrow \frac{\Pr_{t}[ x]}{\Pr_{s}[ x]} =\frac{\Pr[ \sigma =1]}{\Pr[ \sigma =1\ |\ x]}$

Therefore we can say,

$$\epsilon_{s}(h)\varpropto \mathbb{E}_{\Pr_{s}[x]}\frac{1}{\Pr[\sigma=1|x]} \mathbb{E}_{\Pr[y|x]}[h(x)\neq y]$$

**What is the Adaptation Error?**

$$\epsilon _{t}(h) \leqslant ??$$


**A bound on the Adaptation Error**

Let $h$ be a binary hypothesis. If $\Pr_{s}[y\|x] \ =\ \Pr_{t}[y\|x]$, then

$$\epsilon_{t}(h) \ < \epsilon _{s}(h) \ +\ \int _{x}|\Pr_{t}( x) \ -\ \Pr_{s}(x)| dx$$

where, $\Pr_{s}[y\|x] =\Pr_{t}[y\|x]$ is the covariate shift assumption i.e. the conditional distribution is the same.



 
$$\epsilon _{s}( h) \ =\ \mathbb{E}_{\Pr_{s}[x]} \ \mathbb{E}_{\Pr[y|x]} \ [ h(x) \neq y]\\
\therefore \\
\\
\epsilon _{t}( h) =\mathbb{E}_{\Pr_{t}[x]} \ \mathbb{E}_{\Pr[y|x]} \ [ h( x) \neq y]\\
\Longrightarrow \int _{x}\int _{y}\Pr_{t}[x] \ \Pr[y|x] \ [ h(x) \neq y] \ dy\ dx\\
\Longrightarrow \int _{x}\Pr_{t}[x]+\Pr_{s}[x]-\Pr_{s}[x] \ \times \int _{y}\Pr[y|x] \ [h(x) \neq y] \ dy\ dx\\
\Longrightarrow \epsilon _{s}(h) +\int _{x}(\Pr_{t}[x] -\Pr_{s}[x]) \times \int _{y}\Pr[y|x] \ [h(x) \neq y] \ dy\ dx\ \leqslant \epsilon _{s}(h) +\int _{x} |\ \Pr_{t}[x] -\Pr_{s}[x] \ |\ (1) \ dx\\
\Longrightarrow \epsilon _{s}(h) \ +\ \int _{x}| \ \Pr_{t}[x] \ -\ \Pr_{s}[x] \ | \ dx\\
\Longrightarrow \epsilon _{s}(h) \ +\ 2|\ \Pr_{t}[x] \ -\ \Pr_{s}[x] \ |_{var}\\
\\
where,\ |\ P-Q\ |_{var} =\sup _{e} \ |\ P(e) -Q(e) \ |=\frac{1}{2}\int _{x} |\ P( x) -Q( x) \ |\ dx$$
 
