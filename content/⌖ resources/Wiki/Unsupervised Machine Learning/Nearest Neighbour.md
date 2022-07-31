---
tag: todo, unsupervised_ml
date: 2022-07-19
---

## Metadata
- Association:
- Domain: [[Domain Root - Data Science]]

## Nearest Neighbour
Nearest Neighbour (NN) has been one of the most versatile algorithms in the realm of computer science and machine learning. It has been proved to be applicable to [text categorization](https://www.sciencedirect.com/science/article/pii/S1877705814003750), [text classification](https://www.sciencedirect.com/science/article/pii/S1877050920301757), [image recognition](https://ieeexplore.ieee.org/abstract/document/5384892), [predictive maintenance](http://xml.jips-k.org/full-text/view?doi=10.3745/JIPS.04.0183), and more. The main goal of an NN is to identify candidates within the dataset that are the closest to each other. Without diving into too much of the code, there are usually two different directions in its implementation:

-   **[[Exhaustive Search]]:** We will never know which data point is the closest until we have checked every data point in the dataset. This has a linear space and time complexity (a computer science way of saying that the time and memory the algorithm takes is proportional to the dataset size). Because of that, an exhaustive searching algorithm often **suffers a lot as dataset size increases and dimension/number of features increases (the [[Curse of Dimensionalities]]). A well-known example is [[K Nearest Neighbour]] (KNN).**
-   **[[Grid Search]]:** Grid search alleviates the curse of dimensionalities by approximating the problem and subdividing it into smaller chunks, which will each has a smaller space and time complexity, and hence will be able to **finish faster while taking less computational resources.** **An example of this approximate approach is [[Approximate Nearest Neighbour]] (ANN).**