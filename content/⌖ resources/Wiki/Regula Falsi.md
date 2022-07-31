---
tag: root-searching
date: 2022-07-21
approach: "Bracket"
convergence: "Guaranteed"
knowledge_of_root: "Required"
n_initial_seeds: "2"
slow_convergence_risk: "Stagnant Bound"
method_of_problem_space_reduction: "Approximate Derivative with Finite Difference"
convergence_speed: "Linear"
---

## Metadata
- Association: [[Root Searching Algorithms]]
- Domain: [[Domain Root - Data Science]]

## Regula Falsi

Just like [[Bisection Algorithm]], Regula Falsi also uses a bracketing approach. However, unlike [[Bisection Algorithm]], it does not use a brute-force approach of dividing the problem space in half for every iteration. Instead, Regula Falsi iteratively draws a straight line from `f(a)` to `f(b)` and **compares the intercept with the target value**. It is however not guaranteed that the searching efficiency is always improved. For example, the diagram below shows how only the lower bound has been increased in a reducing rate, while the upper bound remains a **[[Stagnant Bound]]**.

![[Pasted image 20220721220340.png]]

**Key Strength:**

-   Often faster convergence than [[Bisection Algorithm]]

> Regula Falsi takes advantage of that as bracket gets smaller, the continuous function will converge to a straight line.

**Key Weakness:**

-   Slower convergence when algorithm hits a [[Stagnant Bound]]
-   Requires knowledge of the approximate area of root e.g. 3 ≤ π ≤ 4

The key difference in the implementation between Regula Falsi and [[Bisection Algorithm]] is that `c` is no longer the mid-point between `a` and `b`, but instead is being calculated as:

$$c = \frac{af(b) - bf(a)}{f(b) - f(a)}$$

## Pseudo Code

```gist
e02b6daf938e843fbed844a6da478d74
```