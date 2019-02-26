---
layout: post
title: Norm2
excerpt: "Sampling is a fundamental aspect of statistics, but unlike the other methods of data collection, sampling involves choosing a method of sampling which further influences the data that you will result with. There are two major categories in sampling: probability and non-probability sampling."
categories: [Statistics, Sampling]
tags: [Statistics]
share: true
comments: true
mathjax: true
---

## What is Norm ?

A norm is a function that assigns a strictly positive length or size to each vector in a vector space—except for the zero vector, which is assigned a length of zero.

## What is Norm2 or Euclidean Norm?

On an n-dimensional Euclidean space $\displaystyle R_{n}$, the intuitive notion of length of the vector $\displaystyle x\ =\ ( x_{1} ,x_{2} ,\ ...,\ x_{n})$ is captured by the formula
 
$\displaystyle \|\|x\|\|_2 := \sqrt{x^2_1 + x^2_2  +...+ x^2_n} \ $

The Euclidean norm is also called the Euclidean length, $\displaystyle L^{2}$ distance, $\displaystyle L^{2}$ norm.


## What is Overflow and Underflow condition ?

Now, there is a largest (in magnitude) number that can be stored and a smallest (in magnitude) number not equal to zero, that can be stored. Storing number larger than the magnitude will cause the memory to Overflow and often it is stored as "Not-A-Number" or "NAN". Now if we try to store a number lower than magnitude but great than zero that situation will result Underflow and it is often set to Zero.

## How is Overflow and Underflow related to Euclidean Norm ?

Let us focus on Overflow. The problem for computing the length (2-norm) of a vector is that equals the square root of the sum of the component. 
While the answer may not cause an overflow, but intermediate results when squaring components could.

## How can we solve the problem  during numerical computation ?

$\displaystyle \|\|x\|\|\_{2} := \sqrt{x^{2}\_{1} + x^{2}\_{2} +...+ x^{2}\_{n}} \ $

we can also write as,

$\displaystyle \|\|x\|\|\_2 \ :=\sqrt{\sum^{n-1}\_{i=0} \chi ^{2}_{i}}$

The solution is to exploit the above equation:


$\displaystyle \|\|x\|\|\_{2} := \sqrt{\sum ^{n-1}\_{i=0} \chi ^{2}_{i}} $

$\displaystyle \Longrightarrow \sqrt{\sum ^{n-1}_{i=0} \ \left[ \alpha ^{2} \ \left(\frac{\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \sqrt{\alpha ^{2} \ \sum ^{n-1}_{i=0} \ \left[\left(\frac{\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \alpha \sqrt{\sum ^{n-1}_{i=0} \ \left[\left(\frac{\\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \alpha \sqrt{\left(\frac{x}{\alpha }\right)^{T}\left(\frac{x}{\alpha }\right)} \ $


where,

$\displaystyle \alpha =\max^{n-1}\_{i=0} \ \|\chi _{i} \|\ ;\ \alpha  >0\ $

> Note that there is no overflow for intermidiate results (when squaring) will happen because all the elements are of magnitude less than or equal to one.



### References

1. https://www3.ntu.edu.sg/home/ehchua/programming/java/datarepresentation.html
2. https://en.wikipedia.org/wiki/Euclidean_distance