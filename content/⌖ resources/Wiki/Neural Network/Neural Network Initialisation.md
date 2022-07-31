---
tag: neural_network, todo
date: 2022-07-19
---

## Metadata
Association:
Domain: [[Domain Root - Data Science]]

## Neural Network Initialisation
[[Neural Network]] initialisation is a process of setting initial weights to all the neurons of a neural network. These weights will be used for computing the very first batch of scores before being updated by [[Backward Propagation]] after lost/cost has been computed.

Initialising weights for [[Neural Network]] are usually as simple as a oneliner:
```python
# one-liner weight initialisation for tensorflow
tf.keras.initializers.RandomUniform(minval=-0.05, maxval=0.05, seed=None)
```

## Rule of Thumb for Weight Initialisation

As deep learning models get more and more complex, the problem of [[Vanishing Gradient]] and [[Exploding Gradient]] will only be more pronounced. **A general rule of thumb for initialising weights is to (1) make it random, (2) have a stable variance for each layer, and (3) potentially make the distribution symmetric.** Based on that, there has been a lot of excellent work dedicated to weight initialisation aiming at better and **faster convergence with reduced gradient problems**. Here are two of the more common initialisation methods that you may find useful for building your own deep learning models:

1. -   **[[He Initialisation]]** [**(He et al. 2015)**](https://arxiv.org/abs/1502.01852)**:** This is more suited for initialising weights for [[ReLu]] and [[Leaky ReLu]] [[Activation Function]].
   $$W^{[l]} = N(0, \sqrt{\frac{2}{size^{[l-1]}}})$$
3. -   **[[Xavier Initialisation]]** [**(Glorot et al. 2010)**](http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf)**:** This is more suited for initialising weights for [[Hyperbolic Tangent]] [[Activation Function]]
   $$W^{[l]} = N(0, \sqrt{\frac{1}{size^{[l-1]}}})$$

That being said, there are some common pitfalls when it comes to [[Neural Network]] initialisation.

## [[Zero Initialisation]] - [[Symmetry Problem]]

- **When does it happen:** All initialised weights of a [[Neural Network]] is zero.
- **Result:** The [[Neural Network]] will become a **[[Linear Model]]**

One of the strengths of [[Neural Network]] are their [[Non-linearity]]. By setting all the weights to zero, all the [[Partial Derivatives]] in [[Backward Propagation]] will be the same for every neuron. While this won't break the algorithm, this will stall learning progress as all neurons in the same layer will be learning the same parameter.

## Too-small Initialisation - [[Vanishing Gradient]]
-   **Why does it happen:** Initialised weights of a neural network are too small
-   **Result:** Premature convergence
-   **Symptoms:** Model performance improves very slowly during training. The training process is also likely to stop very early.

If the initial weights of the neurons are too small relative to the inputs, the **gradient of the hidden layers will diminish exponentially as we propagate backward**. Or you may also say, vanishing through the layers. To better understand that, let’s assume that we have a three-layer fully connected neural network below where every layer has a sigmoid activation function with zero bias:

![[Pasted image 20220719212521.png]]

If we quickly recall how a [[Sigmoid]] function and its derivates look like, we can see that the maximum value of the derivative (i.e. gradient) of the sigmoid function is at 0.25 when $x=0$. For reference, derivative of a [[Sigmoid]] function is $\sigma(x)(1 - \sigma(x))$.

When training a model using [[Gradient Descent]], we will be updating the weights of the entire neural network using [[Backward Propagation]] by taking partial derivatives of the loss values with respect to the weights of each layer. To take the partial derivates for the network we have above, we need to first know about the mathematical expression of it. Assuming

-   $a$ stands for the output vector of activation function,
-   $sigma$ stands for the sigmoid function (i.e. our activation function),
-   $z$ stands for the output of the neurons of a layer, and
-   $W$ stands for the vector of weights of each layer

the output of the neural network above can be represented as follows:

$$\hat{y} = a^{[3]} = \sigma z^{[3]} = \sigma W^{[3]} a^{[2]} = ... = \sigma W^{[3]} \sigma W^{[2]} \sigma W^{[1]} x$$

Hence, the partial derivative for updating $W^{[1]}$, weights in the first layer, will be as follows:

$$\frac{\partial Loss}{\partial W^{[1]}} = \frac{\partial Loss}{\partial a^{[3]}}\frac{\partial a^{[3]}}{\partial z^{[3]}}\frac{\partial z^{[3]}}{\partial a^{[2]}}\frac{\partial a^{[2]}}{\partial z^{[2]}}\frac{\partial z^{[2]}}{\partial a^{[1]}}\frac{\partial a^{[1]}}{\partial z^{[1]}}\frac{\partial z^{[1]}}{\partial W^{[1]}}$$

#todo ==Find more intuitive explanation for this please!==

**Ways to alleviate vanishing gradient can be:**

-   LSTM can solve the vanishing gradient problem with its gates
-   Use activation function like ReLu or leaky ReLu which are both less prone to vanishing gradient
-   Reduce the number of layers
-   Randomly initialize weights at a sufficiently large expected value

## Too-large Initialisation — [[Exploding Gradient]]

-   **When does it happen:** Initialised weights of a neural network are too large
-   **Result:** Loss value will oscillate around minima but unable to converge
-   **Symptoms:** The model will have large changes in its loss value on each update due to its instability. Loss values may also reach `NaN`.
- 
On the opposite, when the weights are too large, **the gradients (partial derivates) will increase exponentially as we propagate backward** to update the weights. Or you may also say, exploding through the layers. As a result, weights change drastically between iterations, leading to an unstable model. The instability of the training process will also make it harder for the model to converge towards global optima but instead just oscillate around it.

#todo ==Find more intuitive explanation for this please!==

**Ways to avoid exploding gradient can be:**

-   [[Gradient Clipping]] which limits the size of the gradient
-   Use activation function like [[ReLu]] or [[Leaky ReLu]] which are both less prone to exploding gradient
-   Randomly initialize weights with sufficiently small expected values
-   Reduce the number of layers