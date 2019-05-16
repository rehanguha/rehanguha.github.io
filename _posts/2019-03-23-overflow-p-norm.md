---
layout: post
title: Handling Overflow condition in calculating p-Norm
excerpt: "An error that occurs when the computer attempts to handle a number that is too large for it. If during execution of Euclidean Distance it arrives at a number outside this range, How will you handle it ?"
categories: [Mathematics, Metric geometry, Code]
tags: [Norm, Distance, Code]
share: true
comments: true
mathjax: true
---
## What is Norm ?

A norm is a function that assigns a strictly positive length or size to each vector in a vector space—except for the zero vector, which is assigned a length of zero.

## *p*-Norm or $L^p$ Norm

Let p ≥ 1 be a real number. The  *p*-norm (also called $\displaystyle L_{p}$-Norm) $\displaystyle x\ =\ ( x_{1} ,x_{2} ,\ ...,\ x_{n})$ is,
 
$$||X||_{p} \ :=\ \left(\sum ^{n}_{i=1} |x_{i} |^{p}\right)^{\frac{1}{p}} \ $$

When *p*=1, it is called Taxi-cab norm, $\displaystyle L^{1}$ norm.

## What is Norm2 or Euclidean Norm?

On an n-dimensional Euclidean space $\displaystyle R_{n}$, the intuitive notion of length of the vector $\displaystyle x\ =\ ( x_{1} ,x_{2} ,\ ...,\ x_{n})$ is captured by the formula
 
$\displaystyle \|\|x\|\|_2 := \sqrt{x^2_1 + x^2_2  +...+ x^2_n} \ $

The Euclidean norm is also called the Euclidean length, $\displaystyle L^{2}$ distance, $\displaystyle L^{2}$ norm.


## What is Overflow and Underflow condition ?

Now, there is a largest (in magnitude) number that can be stored and a smallest (in magnitude) number not equal to zero, that can be stored. Storing number larger than the magnitude will cause the memory to Overflow and often it is stored as "Not-A-Number" or "NAN". Now if we try to store a number lower than magnitude but great than zero that situation will result Underflow and it is often set to Zero.

## How is Overflow and Underflow related to p-Norm ?

Let us focus on Overflow. The problem for computing the length (2-norm) of a vector is that equals the square root of the sum of the squared component. 
While the answer may not cause an overflow, but intermediate results when squaring components could. The same thing holds true for *p*-Norm

## How can we solve the problem  during numerical computation ?

$\displaystyle \|\|x\|\|\_{p} \ \ :=\ \ \sqrt[p]{x^{p}\_{1} \ +\ x^{p}\_{2} \ +...+\ x^{p}\_{n}} \ $


we can also write as,



$$\displaystyle ||x||_{p} \ :=\sqrt[p]{\sum ^{n-1}_{i=0} \chi ^{p}_{i}}  \$$



The solution is to exploit the above equation:



$\displaystyle \|\|x\|\|\_{p} \\ :=\\sqrt[p]{\sum ^{n-1}\_{i=0} \chi ^{p}\_{i}}$



$\displaystyle \Longrightarrow \sqrt[p]{\sum ^{n-1}_{i=0} \ \left[ \alpha ^{p} \ \left(\frac{\chi _{i}}{\alpha }\right)^{p}\right]}$



$\displaystyle \Longrightarrow \sqrt[p]{\alpha ^{p} \ \sum ^{n-1}_{i=0} \ \left[\left(\frac{\chi _{i}}{\alpha }\right)^{p}\right]}$



$\displaystyle \Longrightarrow \alpha \ \sqrt[p]{\sum ^{n-1}_{i=0} \ \left[\left(\frac{\chi _{i}}{\alpha }\right)^{p}\right]}$



where,

$\displaystyle \alpha =\max^{n-1}\_{i=0} \ \|\chi _{i} \|\ ;\ \alpha  >0\ $

### Taking the example of 2-Norm / Euclidean Norm,

$\displaystyle \|\|x\|\|\_{2} := \sqrt{x^{2}\_{1} + x^{2}\_{2} +...+ x^{2}\_{n}} \ $

we can also write as,

$$\displaystyle \|x\|_2 \ :=\sqrt{\sum^{n-1}_{i=0} \chi ^{2}_{i}}$$

Similarly as above:


$\displaystyle \|\|x\|\|\_{2} := \sqrt{\sum ^{n-1}\_{i=0} \chi ^{2}_{i}} $

$\displaystyle \Longrightarrow \sqrt{\sum ^{n-1}_{i=0} \ \left[ \alpha ^{2} \ \left(\frac{\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \sqrt{\alpha ^{2} \ \sum ^{n-1}_{i=0} \ \left[\left(\frac{\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \alpha \sqrt{\sum ^{n-1}_{i=0} \ \left[\left(\frac{\\chi _{i}}{\alpha }\right)^{2}\right]}$

$\displaystyle \Longrightarrow \alpha \sqrt{\left(\frac{x}{\alpha }\right)^{T}\left(\frac{x}{\alpha }\right)} \ $ , this is the added step which is equivalent as the previous equation.


where,

$\displaystyle \alpha =\max^{n-1}\_{i=0} \ \|\chi _{i} \|\ ;\ \alpha  >0\ $

> Note that there is no overflow for intermediate results (when squaring) will happen because all the elements are of magnitude less than or equal to one.


## How to Handle p-Norm Overflow ?

Global Variables:

{% highlight Python %}

x = [] # Define the Vector
p = 1  # Define p >=1, for the p-Norm

{% endhighlight %}

Traditional Method which have a problem for Overflow while computing *p*-Norm:

{% highlight Python %}

temp = []
for i in x:
    temp.append(i**p)
total = sum(temp)
sol2 = (total)**(1/p)
print(sol2)
{% endhighlight %}

Proposed Solution to eliminate Overflow while computing *p*-Norm:

{% highlight Python %}

alpha = max(x)

temp = []
for i in x:
    temp.append((i/alpha)**(p))
total = sum(temp)

root = (total)**(1/p)
sol1 = root*alpha
print(sol1)

{% endhighlight %}



### References

1. https://www3.ntu.edu.sg/home/ehchua/programming/java/datarepresentation.html
2. https://en.wikipedia.org/wiki/Euclidean_distance
