---
tag: root-searching
date: 2022-07-21
approach: "Bracket"
convergence: "Guaranteed"
knowledge_of_root: "Required"
n_initial_seeds: "2"
slow_convergence_risk: "N/A"
method_of_problem_space_reduction: "Brute-force Halving"
convergence_speed: "Linear"
---

## Metadata
- Association: [[Binary Search Trees]] [[Binary Search]] [[Root Searching Algorithms]]
- Domain: [[Domain Root - Data Science]]

## Bisection Algorithm

Bisection algorithm, or more famously known for its discrete version ([[Binary Search]]) or tree variant ([[Binary Search Tree]]), is an efficient algorithm for searching for a target value within a bound. Because of that, this algorithm is also known as a **bracketing approach to finding a root of an algorithm**.

**Key Strength:**

-   Robust algorithm that guarantees reasonable rate of convergence to the target value

**Key Weakness:**

-   Requires knowledge of the approximate area of root e.g. 3 ≤ π ≤ 4
-   Works well there is only **one root** in the approximate area

Assuming that we know `x` is between `f(a)` and `f(b)`, which forms the bracket of the search. The algorithm will check if `x` is greater than or less than `f((a + b) / 2)`, which is the mid-point of the bracket.

A **margin of error** is required for checking against the mid-point of the bracket. When searching a continuous function, it is possible that we will never be able to locate the exact value (e.g. locating the end of π). A margin of error can be treated as an early stopping when the computed value is close enough to the target value. E.g. if margin of error is 0.001%, 3.141624 is close enough to π, which is approximately 3.1415926…

If the computed value is close enough to the target value, the search is done, otherwise, we search for the value in the bottom half if `x < f((a + b) / 2)` and vice versa.

## Pseudo Code

```gist
aa11cb2065c4bc19779f2f06472cda9e
```