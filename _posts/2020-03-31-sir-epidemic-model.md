---
layout: post
title: SIR Epidemic Model with some Modifications
excerpt: ""
categories: [Epidemic, Statistical Modelling, Code]
tags: [COVID-19, Code]
share: true
comments: true
mathjax: true
---
## The SIR Model

The **SIR model** is one of the simplest compartmental models, and many models are derivatives of this basic form. 

The model consists of three compartments: 

- **S** for the number of susceptible, 
- **I** for the number of infectious, and 
- **R** for the number of recovered or deceased (or immune) individuals. 

This model is reasonably predictive for infectious diseases which are transmitted from human to human, and where recovery confers lasting resistance, such as measles, mumps and rubella.

These variables ( **S** , **I**, and **R**) represent the number of people in each compartment at a particular time. To represent that the number of susceptible, infected and recovered individuals may vary over time (even if the total population size remains constant), we make the precise numbers a function of t(time): **S(t)**, **I(t)** and **R(t)**. For a specific disease in a specific population, these functions may be worked out in order to predict possible outbreaks and bring them under control.

(Source: [Wikipedia](https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology#The_SIR_model))


## Mathematical Background

Let **N** be the size of the total population. 

Then,

$\displaystyle S(t) + I(t) + R(t) = N$

The SIR system be expressed by the following set of ordinary differential equations:

$\displaystyle \frac{\DifferentialD S}{\DifferentialD t} =-\beta SI$

$\displaystyle \frac{\DifferentialD I}{\DifferentialD t} =\beta SI - \gamma I$

$\displaystyle \frac{\DifferentialD R}{\DifferentialD t} =\gamma I$


Python Code to Implement SIR Model:

```python

from scipy.integrate import odeint
import matplotlib.pyplot as plt
import numpy as np


# Total population, N.
N = 1000
# Initial number of infected and recovered individuals, I0 and R0.
I0, R0 = 1, 0
# Everyone else, S0, is susceptible to infection initially.
S0 = N - I0 - R0
# Contact rate, beta, and mean recovery rate, gamma, (in 1/days).
beta, gamma = 0.2, 1./10 
# A grid of time points (in days)
t = np.linspace(0, 160, 160)

# The SIR model differential equations.
def deriv(y, t, N, beta, gamma):
    S, I, R = y
    dSdt = -beta * S * I / N
    dIdt = beta * S * I / N - gamma * I
    dRdt = gamma * I
    return dSdt, dIdt, dRdt

# Initial conditions vector
y0 = S0, I0, R0
# Integrate the SIR equations over the time grid, t.
ret = odeint(deriv, y0, t, args=(N, beta, gamma))
S, I, R = ret.T

# Plot the data on three separate curves for S(t), I(t) and R(t)
fig = plt.figure(facecolor='w')
ax = fig.add_subplot(111, axisbelow=True)
ax.plot(t, S/1000, 'b', alpha=0.5, lw=2, label='Susceptible')
ax.plot(t, I/1000, 'r', alpha=0.5, lw=2, label='Infected')
ax.plot(t, R/1000, 'g', alpha=0.5, lw=2, label='Recovered with immunity')
ax.set_xlabel('Time /days')
ax.set_ylabel('Number (1000s)')
ax.set_ylim(0,1.2)
ax.yaxis.set_tick_params(length=0)
ax.xaxis.set_tick_params(length=0)
ax.grid(b=True, which='major', c='w', lw=2, ls='-')
legend = ax.legend()
legend.get_frame().set_alpha(0.5)
for spine in ('top', 'right', 'bottom', 'left'):
    ax.spines[spine].set_visible(False)
plt.show()

```

**Output:**

![Picture](Traditional.png)
