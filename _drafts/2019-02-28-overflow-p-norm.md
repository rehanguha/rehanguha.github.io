---
layout: post
title: Handling Overflow condition in calculating Euclidean Norm
excerpt: "An error that occurs when the computer attempts to handle a number that is too large for it. If during execution of Euclidean Distance it arrives at a number outside this range, How will you handle it ?"
categories: [Mathematics, Metric geometry, Code]
tags: [Norm, Distance, Code]
share: true
comments: true
mathjax: true
---

#### Continued from...
[Handling Overflow condition in calculating Euclidean Norm](https://rehanguha.github.io//articles/2019-02/overflow-euclidean-norm) 


## *p*-Norm or $L^p$ Norm

On an n-dimensional Euclidean space $\displaystyle R_{n}$, the intuitive notion of length of the vector $\displaystyle x\ =\ ( x_{1} ,x_{2} ,\ ...,\ x_{n})$ is captured by the formula
 
$$||X||_{p} \ :=\ \left(\sum ^{n}_{i=1} |x_{i} |^{p}\right)^{\frac{1}{p}} \ $$

When *p*=2, it is called Euclidean norm, Euclidean length, $\displaystyle L^{2}$ distance, $\displaystyle L^{2}$ norm.




## How can we solve the problem  during numerical computation ?





## What is Overflow and Underflow condition ?

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