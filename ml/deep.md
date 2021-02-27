# Deep Learning - DNN

- When there is >=3 hidden layers in NN.
- Layers Count := | InputLayer + HiddenLayer |

## Activation Function

![Activation Function](assets/activation.jpg)
![Activation Function](assets/vanishingGrad.jpg)
![Activation Function](assets/dyingRelu.jpg)

- <https://youtu.be/s-V7gKrsels>
- Usually use `softmax` activiation function at the last layer which it will normalize the result for us.
- For Regression: Don't need activation funciton.
- Use a nonlinear activation function for CNN.
- `reLu/Leaky reLu` typically used for activation function.
- `Leaky reLu` avoids the `dying reLu` problem.

## RNN - Recurrent Neural Network

![](https://pythonprogramming.net/static/images/machine-learning/recurrent-neural-network-basics.png)

Another way to look at this is more like this:

![](https://pythonprogramming.net/static/images/machine-learning/basic-recurrent-neural-network-unfolded-concept.png)

More Details <https://youtu.be/yZv_yRgOvMg>

![](assets/cnn/rnn.jpg)

This way (BPTT - Back Propagation Through Time) has speed and storage problem. So we use Teacher Forcing to fix the issue.

![](assets/cnn/rnn2.jpg)

![](assets/cnn/rnn_1.jpg)
![](assets/cnn/rnn_2.jpg)
![](assets/cnn/rnn_3.jpg)
![](assets/cnn/rnn_4.jpg)

## seq2seq

![](assets/cnn/seq2seq.jpg)

### Encoder Decoder

![](assets/cnn/encoder-decoder.jpg)

Seq 2 Vec 2 Seq: Used in Translation which they may have different input and ouput size.

## seq2vec

![](assets/cnn/seq2vec.jpg)

- Eg. Sentiment Analysis

## vec2seq

![](assets/cnn/vec2seq.jpg)

- Eg. Image Captioning

## BERT

![](assets/cnn/bert.jpg)

- Useful in Text Translation/Summarization because we have the future words.

## LSTM - Long Short Term Memory

![](https://pythonprogramming.net/static/images/machine-learning/long-short-term-memory-cell-LSTM.png)

Recurring data goes through what is referred to as the Keep Gate or Forget Gate, basically which decides what to keep and what to remove from the recurring data. From here, we get to the new input data, determining what new to add from it, then, finally, we decide what our new output will be.

- Sigmoid and Tahn activation function are useful in LSTM
- [MNIST - RNN with LSTM cell example in TensorFlow](https://pythonprogramming.net/rnn-tensorflow-python-machine-learning-tutorial/)
- To understand LSTM http://colah.github.io/posts/2015-08-Understanding-LSTMs/
- More Details <https://youtu.be/QciIcRxJvsM>

![lstm](assets/cnn/lstm2.jpg)
![lstm](assets/cnn/lstm3.jpg)

## GRU

Like LSTM but simpler

![](assets/cnn/gru.jpg)

## CNN - Convolutional Neural Network

![](assets/cnn/cnn3.jpg)

The basic CNN structure is as follows:

Convolution -> Pooling -> Convolution -> Pooling -> Fully Connected Layer -> Output

![](https://pythonprogramming.net/static/images/machine-learning/convolution-new-featuremap.png)

![](https://pythonprogramming.net/static/images/machine-learning/max-pooling-example.png)

### Convolutional Layer

![](assets/cnn/cnn.jpg)
![](assets/cnn/cnn2.jpg)

### Pooling Layer

- Stide = How many pixel to skip

![](assets/cnn/pooling.jpg)

## FC - Fully Connected Layer

![](assets/cnn/fc.jpg)

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
