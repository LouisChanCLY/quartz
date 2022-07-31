---
tag: explainable_ai, todo
date: 2022-07-19
---
## Metadata
- Association: [[KernelSHAP vs TreeSHAP]]
- Domain: [[Domain Root - Data Science]]

## KernelSHAP

KernelSHAP is a model agnostic approximation of [[SHAP]]. 

## Complexity

Complexity of KernelSHAP: $O(TL2^M)$, where `T` is the number of trees, `L` is the maximum number of leaves in the tree, and `M` is the number of features

This means that KernelSHAP can suffer from [[Curse of Dimensionalities]] as the complexity grows exponentially with the number of features

## Feature Dependency

KernelSHAP can be skewed by [[Feature Dependency]]. KernelSHAP randomly samples feature values for estimating [[SHAP]] values. As such, it could be the case that unusual combination of feature values are selected giving an inaccurate approximation of the [[SHAP]] values by biasing towards unlikely observations.