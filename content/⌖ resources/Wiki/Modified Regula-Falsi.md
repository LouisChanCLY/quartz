---
tag: root-searching
date: 2022-07-21
approach: "Bracket"
convergence: "Guaranteed"
knowledge_of_root: "Required"
n_initial_seeds: "2"
slow_convergence_risk: "Stagnant Bound"
method_of_problem_space_reduction: "Approximate Derivative with Finite Difference"
convergence_speed: "Super-linear"
---

## Metadata
- Association: [[Regula Falsi]] [[Root Searching Algorithms]]
- Domain: [[Domain Root - Data Science]]

## Modified Regula-Falsi

In order to get pass the [[Stagnant Bound]], we can add in a conditional rule for when a bound remain stagnant for two rounds. Taking the previous example, as `b` has not moved for two round, and that `c` is not close to the root `x` yet, in the next round, the line will be drawn to `f(b) / 2` instead of `f(b)`. Same applies for the lower bound if instead lower bound is the [[Stagnant Bound]].

![[Pasted image 20220721220450.png]]

**Key Strength:**

-   Often faster convergence than both [[Bisection Algorithm]] and [[Regula-Falsi]]
-   Avoid stagnant bound by halving the [[Stagnant Bound]]’s distance to the target value

**Key Weakness:**

-   Slower convergence when algorithm hits a [[Stagnant Bound]]
-   Requires knowledge of the approximate area of root e.g. 3 ≤ π ≤ 4

## Pseudo Code

```gist
901fa283fa393b3beb014e9247f1727c
```