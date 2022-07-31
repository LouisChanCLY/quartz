---
tag: root-searching
date: 2022-07-21
approach: "Iterative"
convergence: "Not Guaranteed"
knowledge_of_root: "Not Required"
n_initial_seeds: "2"
slow_convergence_risk: "Initial Seed not Close Enough to Root"
method_of_problem_space_reduction: "Approximate Derivative with Finite Difference"
convergence_speed: "Super-linear"
---

## Metadata
- Association: [[Root Searching Algorithms]]
- Domain: [[Domain Root - Data Science]]

## Quasi-Newton’s Method

What if we **do not know where the brackets are**? Well, then secant method can be very useful. Secant method is an iterative algorithm that starts with two estimates and attempts to converge towards the target value. While we can get a better performance when the algorithm convergence and also that we do not need knowledge of the rough location of root, we may run into **risk of divergence if the two initial estimates are too far away from the actual root**.

**Key Strength:**

-   Does not require a bracket that contains the root
-   Does not require knowledge of the approximate area of root

**Key Weakness:**

- Secant does not guarantee convergence

![](https://miro.medium.com/max/700/0*PTvDSGXWNvM-Ycft.png)

Secant’s method of locating x_3 based on x_1 and x_2. Credit: Wikipedia

This method starts by checking two user-defined seeds, say we want to search for a root for `x² — math.pi=0` starting with `x_0=4` and `x_1=5`, then our seeds are 4 and 5. (note that this is the same as searching for `x` such that `x²=math.pi`)

We then locate the intercept with the target value `x_2` by drawing a straight line through `f(x_0)` and `f(x_1)` like what we have done in Regula-Falsi. If `f(x_2)` is not close enough to the target value, we repeat the step and locate `x_3`. In general, the next `x` can be calculated as:

$$x_{n+1} = x_n - f(x_n)\frac{x_n - x_{n-1}}{f(x_n) - f(x_{n-1})}$$

## Pseudo Code

```gist
1f937190b2fdb4375fe763346b6251b4
```