# Deep Learning - DNN

- When there is >=3 hidden layers in NN.
- Layers Count := | InputLayer + HiddenLayer |
- Best Blog Resource: <https://colah.github.io/>

![](https://raw.githubusercontent.com/Foroozani/Deep-Neural-Nets/main/images/DL.png)

## Hyperparameters

- Hyper optimization
  - GridSearch, RandomSearch
  - Bayesian Optimization
- Regularization: Dropout, L2, L1
  - DNNs = Dropout
  - L2 = most common
  - L1 = sparsity (zeros) & feature-selection (rarer circumstances)
- Optimizers (SGD): Momentum -> Adagrad -> RMSProp -> Adam -> Nadam
- Initializers: Zeros, Random Uniform, Xavier
- Scaling
  - Feature-scaling: MinMaxScaler, StandardScaler, RobustScaler
  - Features + inter-layer: Batch Normalization

## Activation Function

![Activation Function](assets/activation.jpg)
![Activation Function](assets/vanishingGrad.jpg)
![Activation Function](assets/dyingRelu.jpg)

- <https://youtu.be/s-V7gKrsels>
- Usually use `softmax` activiation function at the last layer which it will normalize the result for us. ( all 0 to 1)
- For Regression: Don't need activation funciton.
- Use a nonlinear activation function for CNN.
- `reLu/Leaky reLu` typically used for activation function.
- `Leaky reLu` avoids the `dying reLu` problem.

## RNN - Recurrent Neural Network

- RNNs are the Feed Forward Neural Networks that are rolled out over time.
- Unlike normal Neural Networks, RNNs are designed to take a series of inputs with no predetermined limit on size. “Series” as in any input of that sequence has some relationship with their neighbour’s or have some influence on them.
- Basic feed forward networks “remember” things too, but they remember the things they learnt during training. While RNNs learn similarly while training, in addition, they remember things learnt from prior input(s) while generating output(s).
- Types of gatesHere are the different types of gates that we encounter in a typical recurrent neural network:
  - Input gate: Write to cell or not?
  - Forget gate: Erase a cell or not?
  - Gate: How much to write to cell?
  - Output : How much to reveal cell?
- <https://colah.github.io/posts/2015-08-Understanding-LSTMs/>

![RNN](https://colah.github.io/posts/2015-08-Understanding-LSTMs/img/RNN-unrolled.png)

![](assets/cnn/rnn.jpg)

This way (BPTT - Back Propagation Through Time) has speed and storage problem. So we use Teacher Forcing to fix the issue.

![](assets/cnn/rnn2.jpg)

![](assets/cnn/rnn_1.jpg)
![](assets/cnn/rnn_2.jpg)
![](assets/cnn/rnn_3.jpg)
![](assets/cnn/rnn_4.jpg)

RNN disadvantages:

- Slow to train.
- Long sequence leads to vanishing gradient or, say, the problem of long term dependencies. In simple terms, its memory is not that strong when it comes to remembering the old connection.

## seq2seq

![seq2seq](assets/cnn/seq2seq.jpg)

The most popular and most used variant, take input as a sequence and give output as another sequence with variant sizes. Eg. Language translation, for time series data for stock market prediction.

## vec2seq

![vec2seq](assets/cnn/vec2seq.jpg)

- Eg. Image Captioning
- Fixed size Input > Output Sequence

## seq2vec

![seq2vec](assets/cnn/seq2vec.jpg)

- Eg. Sentiment Analysis
- Input of any length > Output Vector of fixed size

## Encoder Decoder

![](assets/cnn/encoder-decoder.jpg)

Seq 2 Vec 2 Seq: Used in Translation which they may have different input and ouput size.

## AutoEncoder

- <https://youtube.com/playlist?list=PLTl9hO2Oobd9ZXfLjfXpJ0zgZGeJQZ09a>
- https://pythonprogramming.net/autoencoders-tutorial/

![](assets/cnn/ae.jpg)

- Some examples are in the form of compressing the number of input features and noise reduction.
- Output is not important, but the vector is what we care about.

Types:

- Sparce AutoEncoder
- Denoising AutoEncoder
- Variational Autoencoders

Used in:

- Image Segmentation
- Semantic Hashing
- Neural Inpainting (eg. Removing Watermarks)

## VAE - Variational Autoencoders

- **VAE is a GAN and AE.**
- AE Can't generate new data because we dont know how to assign values to the vector during the generation phase. (VAE is the solution)

![](assets/cnn/ae-gen.jpg)

How VAE solve this:

![](assets/cnn/vae2.jpg)
![](assets/cnn/vae3.jpg)

![](assets/cnn/var-vs-norm.jpg)
![](assets/cnn/var-vs-gan.jpg)

## GAN - Generative adversarial network

![gan](assets/cnn/ganz.jpg)
![gan](assets/cnn/gan.jpg)
![gan](assets/cnn/gan2.jpg)

### DCGAN - Deep Convolutional GAN

- CNNs used in unsupervised learning
- Generators are Deconvolutional NN
- Discriminators are CNNs

![dcgan](assets/cnn/dcgan.jpg)
![dcgan](assets/cnn/dcgan2.jpg)

### CoGAN - Coupled GAN

![cogan](assets/cnn/cogan.jpg)
![cogan](assets/cnn/cogan2.jpg)

### CGAN - Confitional GAN

![cgan](assets/cnn/cgan.jpg)

### Info GAN

![igan](assets/cnn/igan.jpg)

### WGAN - Wasserstein GAN

- Replaces the old method of measuring loss, Jenson-Shannon Divergence with the new Wasserstein distance.
- We can now train discriminator until convergence, leading to higher quality samples generated by the generator.

### CycleGAN

- <https://www.youtube.com/watch?v=NyAosnNQv_U>
- https://junyanz.github.io/CycleGAN/

Cycle consistent adversarial networks for unpaired image-image translation. Some image-image translation problems include:

- Season Transfer
- Object Transfiguration
- Style transfer
- Photo Enhancement

![](https://junyanz.github.io/CycleGAN/images/teaser.jpg)

## Transformer

- An encoder decoder architecture based on attention layers.
- One main difference is that the **input sequence can be passed parallelly**, so that **GPU** can be utilized effectively, and the speed of training can also be increased. And it is based on the multi-headed attention layer, vanishing gradient issue is also overcome by a large margin.
  ![Transformer](assets/trans/tr.jpg)

- <https://youtu.be/TQQlZhbC5ps>
- Implementation https://nlp.seas.harvard.edu/2018/04/03/attention.html

![Transformer](https://miro.medium.com/max/875/1*57LYNxwBGcCFFhkOCSnJ3g.png)

### Encoder Block

![Encoder](assets/trans/tr_en.jpg)
**Embedding Space - Word Embedding**: It’s like an open space or dictionary where words of similar meanings are grouped together or are present close to each other in that space.
![Embedding](assets/trans/tr2.jpg)
But one other issue: every word in different sentences has different meanings. So, to solve this issue, we take the help of Positional Encoders. It is a vector that gives context according to the position of the word in a sentence.
![Embedding](assets/trans/tr3.jpg)
Attention vector: For every word we can have an attention vector generated, which captures the contextual relationship between words in that sentence.
![Embedding](https://miro.medium.com/max/875/1*-4_5Ko6KF7mpAkMddl0xTQ.png)
The only problem it faces is that for every word it weighs its value much higher on itself in the sentence, but we are inclined towards it’s interaction with other words of that sentence. So, we determine multiple attention vectors per words and take a weighted average, to compute final attention vector of every word.
As we are using multiple attention vectors, it is called the Multi-Head Attention Block.
Feed Forward Network accepts attention vectors “one at a time”.
And the best thing here is unlike the case of RNN, here each of these attention vectors are independent of each other. So, parallelization can be applied here, and that makes all the difference.

### Decoder Block

![decoder](assets/trans/tr_de.jpg)

In Masked Multi-Head Attention Block we need to know how the learning mechanism works. First we give a English word, it will translate in it’s French version itself using previous results, then it will match and compare with the actual French translation (which we fed in the decoder block). After comparing both, it will update it’s matrix value. This is how it will learn after several iterations.
![Transformer](https://miro.medium.com/max/875/1*HtMxxJk_U9-LpY_B_kebmw.png)

Now, the resulting attention vectors from the previous layer and the vectors from the Encoder Block are passed into another Multi-Head Attention Block. That’s why it is called Encoder-Decoder Attention Block. The output of this block is attention vectors for every word in English and French sentences. Each vector represents the relationship with other words in both the languages.

A linear layer is another feed forward layer. It is used to expand the dimensions into numbers of words in the Sanskrit language after translation.

Now it is passed through a Softmax Layer, which transforms the input into a probability distribution, which is human interpretable. And the resulting word is produced with highest probability after translation.

![](https://3.bp.blogspot.com/-aZ3zvPiCoXM/WaiKQO7KRnI/AAAAAAAAB_8/7a1CYjp40nUg4lKpW7covGZJQAySxlg8QCLcBGAs/s640/transform20fps.gif)

## BERT - Bidirectional Encoder Representations from Transformers

![bert](assets/cnn/bert.jpg)

### Word Embedding

- Play with code <https://colab.research.google.com/drive/1yFphU6PW9Uo6lmDly_ud9a6c4RCYlwdX>
- BERT is pre-trained and has fixed Vocabulary.
- It breaks down unknown words into subwords.

![](assets/subword.jpg)

### Advantages of Fine-Tuning

BERT already encodes a lot about our language.

1. Quicker Development
2. Less Data Required
3. Better Results

![bert](assets/trans/bert1.jpg)
![bert](assets/trans/bert2.jpg)
![bert](assets/trans/bert3.jpg)
![bert](assets/trans/bert4.jpg)

- C is binary. 1 if Sentence B follows Sentence A and 0 if it does not.
- Each T in WordVector that correspond to outputs for the masked language model problem. They have same size and generated simultaneously.

![bert](assets/trans/bert5.jpg)
![bert](assets/trans/bert6.jpg)
![bert](assets/trans/bert6_embd.jpg)
![bert](assets/trans/bert7.jpg)
![bert](assets/trans/bert8.jpg)

## GPT - Generative Pre-trained Transformer

Made by Stacking Decoders

![GPT](assets/trans/gpt.jpg)
![GPT](assets/trans/trans_nextword.jpg)

## XLNet

![xlnet](assets/trans/xlnet.jpg)

## Attention

![attention](assets/att/1.jpg)
![attention](assets/att/2.jpg)

### Types of Attention

![attention](assets/att/t1.jpg)
![attention](assets/att/t2.jpg)

### Application of Attention

![attention](assets/att/app1.jpg)
![attention](assets/att/app2.jpg)
![attention](assets/att/app3.jpg)

## LSTM - Long Short Term Memory

LSTM network is a type of RNN model that avoids the vanishing gradient problem by adding 'forget' gates.

<https://colah.github.io/posts/2015-08-Understanding-LSTMs/>

![](https://pythonprogramming.net/static/images/machine-learning/long-short-term-memory-cell-LSTM.png)

Recurring data goes through what is referred to as the Keep Gate or Forget Gate, basically which decides what to keep and zwhat to remove from the recurring data. From here, we get to the new input data, determining what new to add from it, then, finally, we decide what our new output will be.

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
![](assets/cnn/conv.jpg)

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

### Dropout Layer

- Randomly turning off neurouns in layers.
- Dropblock <https://www.youtube.com/watch?v=GcvGxXePI2

![Dropout](assets/cnn/dropout.jpg)

## What Filters learns

<https://youtu.be/eL80Im8Hq0k>

![Filters](assets/cnn/filterz.jpg)

### Bilinear Interpolation

Upscalling or upsampling technique

![Bilinear Interpolation](assets/cnn/Bilinear.jpg)

### Activation function and masking

![activation_mask](assets/cnn/activation_mask.jpg)

### Intersection over Union - IoU

A Metic messures overlap.

![iou](assets/cnn/iou.jpg)

We need a dataset with the image and its corresponding masks for every single object in the image.

We determine the IoU for each of the object masks and our mask. The largest IoU is the classification that our network produces.

## Depthwise Separable Convolution

- A faster method of convolution with less computation power & parameters.
- Performing convolution with significantly less multiplication operation.
- Basiclly we are applying different filters to each individual channel (in Std Conv we apply to all).

## Masked R-CNN - Mask Region based Convolution Neural Networks

![masked](assets/cnn/maskedrcnn.jpg)

- Object Detection + Semantic Segmentation = Instance Segmentation
- Masked R-CNN achieves Instance Segmentation
- Faster R-CNN + FCN = Masked R-CNN
- Rol Align preserves spatial orientation of features with no loss of data

## Few Shot Learning

- There are applications wherein we neither have enough data for each class and the total number classes is huge as well as dynamically changing. Thus, the cost of data collection and periodical re-training is too high. On the other hand, in a one shot classification, we require only one training example for each class.
- One Shot Learning with Siamese Networks using Keras <https://towardsdatascience.com/one-shot-learning-with-siamese-networks-using-keras-17f34e75bb3d>

![few shot](assets/cnn/few.jpg)

## Time series

<https://www.kaggle.com/freespirit08/time-series-for-beginners-with-arima>

Time Series is a series of observations taken at specified time intervals usually equal intervals. Analysis of the series helps us to predict future values based on previous observed values. In Time series, we have only 2 variables, time & the variable we want to forecast.

![Time series](assets/ts.jpg)
![Time series](assets/ts2.jpg)

## Image Captioner

- <https://youtu.be/c_bVBYxX5EU>
- <https://github.com/yunjey/show-attend-and-tell>

![Captioner](assets/Captioner.jpg)

## Siamese

- siamese cnn
- siamese lstm
- siamese bi-lstm
- siamese CapsuleNet

## Inception Network (also known as GoogLeNet)

![](https://miro.medium.com/max/800/1*KMdg-mRHZCCwGoa3qwJJag.jpeg)

This is a historically significant CNN design, having won the ImageNet recognition competition in 2014. The Inception model is also significant because it uses 12 times fewer parameters than the AlexNet.

Before further explaining how the Inception block works, we will quickly comment on the difference between Inception and other popular advanced CNN designs such as ResNet and DenseNet. ResNet and DenseNet increase the capacity of CNNs by increasing the depth of the network. This is done by adding shortcut connections that combat problems with feature redundancy.

Contrastingly, the Inception network focuses on the **width** of each layer, oppossed to the **depth** of the overall network. In more concrete terms, the Inception network presented in this paper contains 22 parametric layers, whereas ResNets or Highway networks usually contain over 100 layers.

### Inception Block: To shrink the depth of the feature map

![Inception Block](https://paperswithcode.com/media/methods/Screen_Shot_2020-06-22_at_3.22.39_PM.png)

(a). Stacking many different layers together. The Inception module copies the original input and feeds this same input to each of the different operations.

(b). we see that the input is initially passed through a 1x1 convolution before the 3x3, 5x5, and max-pool. This is done in order to reduce computational complexity, remember that a 1x1 convolution preserves the spatial dimensions of feature maps but can be used to decrease/increase the depth with the number of filters maps hyper-parameter.

### Intermediate Classifiers to Solve Vanishing Gradient

![Intermediate Classifiers](https://miro.medium.com/max/1250/1*Z_tzA_tY41GaDX3zH1mzaw.png)

Intermediate Classifiers forces the intermediate features learned in this network to have discriminative features for the task at hand. With respect to the mechanisms used for implementation, the loss from each intermediate classifier is nerfed by a factor of 0.3 when updating the parameters via backpropagation.

## DenseNet

- <https://towardsdatascience.com/understanding-and-visualizing-densenets-7f688092391a>
- Counter-intuitively, by connecting this way DenseNets require fewer parameters than an equivalent traditional CNN, as there is no need to learn redundant feature maps.
- Furthermore, some variations of ResNets have proven that many layers are barely contributing and can be dropped. In fact, the number of parameters of ResNets are big because every layer has its weights to learn. Instead, DenseNets layers are very narrow (e.g. 12 filters), and they just add a small set of new feature-maps.
- Another problem with very deep networks was the problems to train, because of the mentioned flow of information and gradients. DenseNets solve this issue since each layer has direct access to the gradients from the loss function and the original input image.

![DEnse](https://miro.medium.com/max/474/1*GeK21UAbk4lEnNHhW_dgQA.png)

![Dense](https://paperswithcode.com/media/methods/Screen_Shot_2020-06-20_at_11.35.53_PM_KroVKVL.png)

## CapsuleNet

??
