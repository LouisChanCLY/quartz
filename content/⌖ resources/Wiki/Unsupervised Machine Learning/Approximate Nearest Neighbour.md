---
tag: unsupervised_ml
date: 2022-07-19
github: https://github.com/spotify/annoy
---

## Metadata
- Association:
- Domain: [[Domain Root - Data Science]]

## Approximate Nearest Neighbour

ANN has three main steps:

1.  **Vector transformation:** Applying [[Dimension Reduction]] on a higher dimensional dataset. **An oversimplified example can be [[Principal Component Analysis]]** where multiple dimensions are collapsed into principal components that are orthogonal to each other while maximising variance for separating the data points.
2.  **Vector Encoding:** Essentially indexing the entire dataset. As a dataset grows in size, it becomes harder and harder to sort and search and iterate through the table. Indexing a dataset will significantly reduce the complexity of searching a dataset. **An oversimplified example can be [[Binary Search Trees]]** where all our data points are nicely sorted and organised, ready to be searched.
3.  **Non-exhaustive Searching:** A binary search tree is well and good, but it also means that we need to start from the root. Using the image below as an example, to determine the nearest neighbour of number 4, we start from the root 12, to 6 and to 2 where we realise 4 is the only leave so we take a step back to 6 and then traverse to 8 where all its leaves can be considered as approximately nearest neighbours. **An oversimplified example can be [[inverting Binary Search Trees]]** where we map 4 to 8, reducing the problem of finding the nearest neighbours of 4 to among the leaves of 8, instead of among all the other nodes. **In this simple example, this trick has reduced the number of tree traversal by half.**

![[Pasted image 20220719221032.png]]

## Application

Apart from being used as an [[Unsupervised Machine Learning]] algorithm, ANN can also be used as a [[Collaborative Filtering Recommendation System]]. More on that [here](https://pub.towardsai.net/ann-recommendation-system-for-stock-selection-c9751a3a0520)

## GitHub Repository

**ANNOY:** Spotify’s C++ implementation of ANN with Python bindings so that we can enjoy both the flexibility of Python language and lightspeed computation of C++. GitHub link [here](https://github.com/spotify/annoy).

```python
from annoy import AnnoyIndex

t = AnnoyIndex(NUM_FEATURES, metric="euclidean") # euclidean distance

# append items to the tree, each with an id and a vector
for i, vector in enumerate(ann_items):
	t.add_item(i, vector)

# build an ANN with 200 trees
t.build(200)

# get 200 nearest neighbours of the item with id 1
t.get_nns_by_item(1, 200)
```