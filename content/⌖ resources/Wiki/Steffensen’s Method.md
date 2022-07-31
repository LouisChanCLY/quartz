---
tag: root-searching
date: 2022-07-21
approach: "Iterative"
convergence: "Not Guaranteed"
knowledge_of_root: "Not Required"
n_initial_seeds: "1"
slow_convergence_risk: "Initial Seed not Close Enough to Root"
method_of_problem_space_reduction: "Approximate Derivative with Polynomial Fit"
convergence_speed: "Quadratic"
---

## Metadata
- Association: [[Regula Falsi]] [[Root Searching Algorithms]]
- Domain: [[Domain Root - Data Science]]

## Steffensen’s Method

[[Quasi-Newton’s Method]] further improves the [[Regula Falsi]] algorithm by removing the requirement of a bracket which contains a root. Recall that the straight line is in fact just a naive estimate of the tangent line (i.e. the derivative) of the of two `x` values (or upper and lower bound in [[Regula Falsi]] and [[Modified Regula-Falsi]] algorithm). This estimate will be more accurate as the search converges. In Steffensen’s algorithm, we will attempt to replace the straight line with a **better estimate of the derivative** for further improving the Secant’s method.

**Key Strength:**

-   Does not require a bracket that contains the root
-   Does not require knowledge of the approximate area of root
-   Faster convergence than [[Quasi-Newton’s Method]] if possible

**Key Weakness:**

-   Does not guarantee convergence if the initial seed is too far away from the actual root
-   The continuous function will be evaluated twice that of Secant’s method in order to better estimate the derivative

In order to estimate the derivative better, Steffenson’s algorithm will compute the following based on the user-defined initial seed `x_0`.

$$g(x) = \frac{f(x + f(x))}{f(x)} - 1$$

which is equivalent to the following where $h = f(x)$:

$$g(x) = \frac{f(x + h)}{h} - 1$$

> Does it look like derivative of $f(x)$?

The generalised estimated slope function will then be used to locate the next step following the similar step as [[Quasi-Newton’s Method]]:

$$x_{n+1} = x_n - \frac{f(x_n)}{x_n \times g(x_n)}$$

```gist
907ed0ba4d500170df441ff7734ed879
```