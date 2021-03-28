# ML

## Confusion Matrix

![confusion](assets/confusion-matrix.png)

## Precision, Recall & F-Measure

<https://youtu.be/j-EB6RqqjGI>

![](assets/measure1.jpg)
![](assets/measure2.jpg)

## Loss Function

<https://youtu.be/QBbC3Cjsnjg>

In Regression

![loss](assets/loss/1.jpg)
![loss](assets/loss/2.jpg)
![loss](assets/loss/3.jpg)

In Classification

![loss](assets/loss/4.jpg)
![loss](assets/loss/5.jpg)
![loss](assets/loss/6.jpg)

There are more Loss functions, but we can use Adaptive Loss.

All losses have general equaltion, by using maximum likelihood estimation we will find our best Loss method.

![loss](assets/loss/8.jpg)
![loss](assets/loss/7.jpg)

## Optimzers

![sgd](https://ruder.io/content/images/2015/12/without_momentum.gif)

- <https://youtu.be/mdKjMPmcWj>
- Blog with more details <https://ruder.io/optimizing-gradient-descent/index.html#adagrad>

Gradient descent variants

- Batch gradient descent
- Stochastic gradient descent
- Mini-batch gradient descent

Gradient descent optimization algorithms

- Momentum
- Nesterov accelerated gradient
- Adagrad
- Adadelta
- RMSprop
- Adam
- AdaMax
- Nadam
- AMSGrad
- Other recent optim

## Learning rate

The learning rate, often noted α or sometimes η, indicates at which pace the weights get updated.

This can be fixed or adaptively changed. The current most popular method is called Adam, which is a method that adapts the learning rate.

## Backpropagation

Backpropagation is a method to update the weights in the neural network by taking into account the actual output and the desired output. The derivative with respect to weight w is computed using chain rule and is of the following form:

![backprop](assets/backprop.jpg)

### Updating weights

In a neural network, weights are updated as follows:

- Step 1: Take a batch of training data.
- Step 2: Perform forward propagation to obtain the corresponding loss.
- Step 3: Backpropagate the loss to get the gradients.
- Step 4: Use the gradients to update the weights of the network.

## Dropout

Dropout is a technique meant to prevent overfitting the training data by dropping out units in a neural network. In practice, neurons are either dropped with probability p or kept with probability 1-p.

## Batch Normalization

Normalization on layer which will help our algorithm to fine min loss faster! (minus avg and divide it with variance) (Have trainable parameters)

![batch](assets/batch/1.jpg)
![batch](assets/batch/2.jpg)
![batch](assets/batch/3.jpg)

Like Dropout, but does not replace it and we still use dropout for better results.

It is usually done after a fully connected/convolutional layer and before a non-linearity layer and aims at allowing higher learning rates and reducing the strong dependence on initialization.

### Layer Normalization

![](assets/normz.jpg)

## PCA - Principal Component Analysis

<https://youtu.be/9oSkUej63y>

![pca](assets/pca.png)
