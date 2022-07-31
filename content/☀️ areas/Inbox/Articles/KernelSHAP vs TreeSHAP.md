---
tag: explainable_ai
source: medium
---
# KernelSHAP vs TreeSHAP

![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article1.be68295a7e40.png)

## Metadata
- Author: [[Conor O'Sullivan]]
- Full Title: [[KernelSHAP]] vs [[TreeSHAP]]
- Category: #articles
- URL: https://medium.com/p/e00f3b3a27db
- GitHub Link: https://github.com/conorosully/medium-articles/blob/master/src/interpretable%20ml/SHAP/kernelSHAP_vs_treeSHAP.ipynb

## Highlights
- [[KernelSHAP]] is model agnostic. This means it can be used with any machine learning algorithm
- Only the complexity for [[TreeSHAP]] is impacted by depth (D). On the other hand, only [[KernelSHAP]] is impacted by the number of features (M). The difference is that [[KernelSHAP]] complexity is exponential w.r.t M and [[TreeSHAP]] is quadratic w.r.t D. Considering that we also had more features (M = 10) than tree depth (D= 4), we can see why [[KernelSHAP]] was slower.
- Before making your choice, there are some other differences that you might want to consider. These include the fact that [[KernelSHAP]] is model agnostic, the methods are impacted by feature dependencies and only [[TreeSHAP]] can be used to calculate interaction effects.
- Neural networks also have their own approximation methods. You can use [[DeepSHAP]] for these algorithms.
- Feature dependencies can skew the approximations made by [[KernelSHAP]]. The algorithm estimates [[SHAP]] values by randomly sampling feature values.
- That is a feature that has no impact on the prediction can get a [[SHAP]] value that is non-zero. This can happen when the feature is correlated with another feature that does impact the prediction.
- [[SHAP]] interaction values you will have to use [[TreeSHAP]]


#todo/next-action 
- [ ] Translate content of [[KernelSHAP vs TreeSHAP]] into knowledge graph