---
tag: todo
date: 2022-07-25
---

## Metadata
- Association:
- Domain: [[Domain Root - Data Science]]

## Stein Variational Gradient Descent

[[Neural Variational Gradient Descent]]
[[Bayesian Inference]] beyond VI and MCMC

Is it possible to combine the advantages of [[MCMC]] and [[Variational Inference]]? Stein methods are a promising family of algorithms for approximate bayesian inference. The basic idea is to create a system of particles and optimize the system so the set of particles represents the properties of the posterior. For example, SVGD like VI tries to minimise the [[KL Divergence]] but in a non-parametric way. This approach leverages both sampling and optimisation. The drawback of SVGD is being sensitive to the chosen kernel which is used to realize the geometry of space. NVGD has been proposed to address this problem, so it can capture the geometry automatically.  
  
Some probabilistic programming languages like PyMC3 and Pyro have already implemented some algorithms of this family.

Stein Variational Gradient Descent: A General Purpose Bayesian Inference Algorithm, 2016  
Arxiv: [https://lnkd.in/eWSFT4SJ](https://lnkd.in/eWSFT4SJ)

Neural Variational Gradient Descent, 2021  
Arxiv: [https://lnkd.in/eNWpyq9P](https://lnkd.in/eNWpyq9P)

Stein methods in Pyro: [https://lnkd.in/eRWyYYjS](https://lnkd.in/eRWyYYjS)

SVGD in PyMC: [https://lnkd.in/eTchSAxF](https://lnkd.in/eTchSAxF)