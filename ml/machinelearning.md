# ML

## Confusion Matrix

![confusion](assets/confusion-matrix.png)

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

## Batch Normalization

Normalization on layer which will help our algorithm to fine min loss faster! (minus avg and divide it with variance) (Have trainable parameters)

![batch](assets/batch/1.jpg)
![batch](assets/batch/2.jpg)
![batch](assets/batch/3.jpg)

Like Dropout, but does not replace it and we still use dropout for better results.

### Layer Normalization

![](assets/normz.jpg)

## PCA - Principal Component Analysis

<https://youtu.be/9oSkUej63y>

![pca](assets/pca.png)
