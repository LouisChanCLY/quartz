---
tag: explainable_ai
date: 2022-07-19
---

# SHAP
> Local interpretability of predictive model

## Metadata
- Association: [[KernelSHAP vs TreeSHAP]], [[Explainable AI]], [[SHAP Values Explained Exactly How You Wished Someone Explained to You]]
- Domain: [[Domain Root - Data Science]]

## Introduction
SHapley Additive exPlanations (SHAP) is an algorithm first published in 2017 by [[Scott Lundberg]] and [[Su-In Lee]] in [[A Unified Approach to Interpreting Model Predictions]] for reverse-engineering the output of any predictive algorithm.

In fact, SHAP is derived from [[Shapley Values]], a concept from [[Game Theory]]. In this context, the game for SHAP is sat up as follows:

- **Game Objective:** Reproduce the output of the model
- **Players:** Features included in the model

In essence, SHAP is quantifying the contribution of each feature on the prediction output of the model i.e. **local interpretability**
## How it works?

Assume $F$ be the number of features of a model

1. Create [[Power Set]] of all features (i.e. [[Cardinality]] of $2^F$)
2. Train a predictive model for each coalition of the power set (i.e. $2^F$ models) with the exact same [[Hyperparameter]] and [[Training Data]] as the origin predictive model
3. Run an observation through model inference for all the above models
4. Compute the marginal contributions of each feature under different coalition set
5. Compute the weighted sum of marginal contributions for each feature using the following formula:

$$SHAP_{feature}(s) = \sum_{\mathclap{set:feature \in set}}[|set| \times \begin{pmatrix} F \\ |set| \end{pmatrix}]^{-1}[Predict_{set}(x) - Predict_{set\backslash feature}(x)]$$

## Example Walkthrough

Assumes a predictive model uses $Age$, $Gender$, and $Job$ for predicting some other socio-ecomonic status of a person. (i.e. $F=3$). The [[Power Set]] of all feature will be as follows:

![[Pasted image 20220720221454.png]]

For each node above, a predictive model with the same [[Hyperparameter]] and [[Training Data]] is trained. For an observation vector $x_0$, the inference results for the eight models are as follows:

![[Pasted image 20220720221729.png]]

To compute the marginal contribution for feature $Age$, we will need to compute the following:
$$\begin{cases}
MC_{Age, \{Age\}}(x_0) = Predict_{\{Age\}}(x_0) - Predict_\varnothing(x_0) = 40k - 50k = -10k \\
MC_{Age, \{Age, Gender\}}(x_0) = Predict_{\{Age, Gender\}}(x_0) - Predict_{\{Gender\}}(x_0) = 39k - 48k = -9k \\
MC_{Age, \{Age, Job\}}(x_0) = Predict_{\{Age, Job\}}(x_0) - Predict_{\{Job\}}(x_0) = 85k - 100k = -12k \\
MC_{Age, \{Age, Gender, Job\}}(x_0) = Predict_{\{Age, Gender, Job\}}(x_0) - Predict_{\{Gender, Job\}}(x_0) = 83k - 95k = -12k
\end{cases}$$

![[Pasted image 20220720222550.png]]

The corresponding weights $w_1$, $w_2$, $w_3$, and $w_4$ are then computed as follows:

$$\begin{cases}
w_1 = [1 \times \begin{pmatrix} F \\ 1 \end{pmatrix}]^{-1} = 1/3 \\
w_2 = [2 \times \begin{pmatrix} F \\ 2 \end{pmatrix}]^{-1} = 1/6 \\
w_3 = [2 \times \begin{pmatrix} F \\ 2 \end{pmatrix}]^{-1} = 1/6 \\
w_4 = [3 \times \begin{pmatrix} F \\ 3 \end{pmatrix}]^{-1} = 1/3 \\
\end{cases}$$

![[Pasted image 20220720223157.png]]

To put it simply, the weight for a coalition with cardinality $f$ will be the reciprocal of the number of possible marginal contributions to all the models with $f$ features.

> Note that all the weights for a feature $f$ should sum up to 1

With the weights, the SHAP value for $Age$ on observation $x_0$ can then be calculated as follows:

$$SHAP_{Age}(x) = 
\begin{bmatrix} w_1 & w_2 & w_3 & w_4 \end{bmatrix} \cdot 
\begin{bmatrix} MC_{Age, \{Age\}}(x_0) \\ MC_{Age, \{Age, Gender\}}(x_0) \\ MC_{Age, \{Age, Job\}}(x_0) \\ MC_{Age, \{Age, Gender, Job\}}(x_0) \end{bmatrix}
= 
\begin{bmatrix} 1/3 & 1/6 & 1/6 & 1/3 \end{bmatrix} \cdot 
\begin{bmatrix} -10k \\ -9k \\ -15k \\ -12k \end{bmatrix}
= -11.33k$$

Repeating it for the other features would get $SHAP_{Gender}(x_0) = -2.33k$ and $SHAP_{Job}(x_0) = 46.66k$. Summing all three SHAP values would give $33k$ which is the different between the output of the full model (${Age, Gender, Job}$) at $83k$, and the output of the dummy model ($\varnothing$) at $50k$.

## Approximation of SHAP

As illustrated above, the original SHAP algorithm does not scale well and would suffer from [[Curse of Dimensionalities]] as $2^F$ models would need to be trained to explain a $F$-feature-model. As such, the following approximation algorithms have been derived for different situations:

- [[KernelSHAP]]: model agnostic approximation of SHAP with time complexity more dependent on number of features
- [[TreeSHAP]]: approximation of SHAP for tree-based models with time complexity more dependent on number of trees and tree depth
- [[DeepSHAP]]: approximation of SHAP for [[Neural Network]]

## Feature Dependencies

## Interaction Effects

## Alternatives to SHAP

## Comparison of SHAP Options

| Algorithm | Time Complexity | Applicability |
| --- | --- | --- |
| [[KernelSHAP]] | $O(TL2^M)$ | Model Agnostic |
| [[TreeSHAP]] | $O(TLD^2)$ | Tree-based Models Only |