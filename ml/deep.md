# Deep Learning

- When there is >=3 hidden layers in NN.
- Layers Count := | InputLayer + HiddenLayer |

## RNN - Recurrent Neural Network

![](https://pythonprogramming.net/static/images/machine-learning/recurrent-neural-network-basics.png)

Another way to look at this is more like this:

![](https://pythonprogramming.net/static/images/machine-learning/basic-recurrent-neural-network-unfolded-concept.png)

## LSTM - Long Short Term Memory

![](https://pythonprogramming.net/static/images/machine-learning/long-short-term-memory-cell-LSTM.png)

Recurring data goes through what is referred to as the Keep Gate or Forget Gate, basically which decides what to keep and what to remove from the recurring data. From here, we get to the new input data, determining what new to add from it, then, finally, we decide what our new output will be.

- Sigmoid and Tahn activation function are useful in LSTM
- [MNIST - RNN with LSTM cell example in TensorFlow](https://pythonprogramming.net/rnn-tensorflow-python-machine-learning-tutorial/)
- To understand LSTM http://colah.github.io/posts/2015-08-Understanding-LSTMs/

## CNN - Convolutional Neural Network

The basic CNN structure is as follows:

Convolution -> Pooling -> Convolution -> Pooling -> Fully Connected Layer -> Output

![](https://pythonprogramming.net/static/images/machine-learning/convolution-new-featuremap.png)

![](https://pythonprogramming.net/static/images/machine-learning/max-pooling-example.png)

- [MNIST CNN with TensorFlow](https://pythonprogramming.net/cnn-tensorflow-convolutional-nerual-network-machine-learning-tutorial/)
- [3D CNN on medical imaging data (CT Scans) for Kaggle](https://pythonprogramming.net/3d-convolutional-neural-network-machine-learning-tutorial/#Kaggle-Competition)
- [Classifying Cats vs Dogs with a CNN on Kaggle](https://pythonprogramming.net/convolutional-neural-network-kats-vs-dogs-machine-learning-tutorial/)
- [Using a NN to solve OpenAI's CartPole balancing environment](https://pythonprogramming.net/openai-cartpole-neural-network-example-machine-learning-tutorial/)

## CapsuleNet

## Siamese

- siamese cnn
- siamese lstm
- siamese bi-lstm
- siamese CapsuleNet

## Time series data
