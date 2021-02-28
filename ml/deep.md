# Deep Learning - DNN

- When there is >=3 hidden layers in NN.
- Layers Count := | InputLayer + HiddenLayer |
- Best Blog Resource: <https://colah.github.io/>

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

- RNNs are the Feed Forward Neural Networks that are rolled out over time.
- Unlike normal Neural Networks, RNNs are designed to take a series of inputs with no predetermined limit on size. “Series” as in any input of that sequence has some relationship with their neighbour’s or have some influence on them.
- Basic feed forward networks “remember” things too, but they remember the things they learnt during training. While RNNs learn similarly while training, in addition, they remember things learnt from prior input(s) while generating output(s).
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

<https://youtube.com/playlist?list=PLTl9hO2Oobd9ZXfLjfXpJ0zgZGeJQZ09a>

![](assets/cnn/ae.jpg)

Output is not important, but the vector is what we care about.

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

![dcgan](assets/cnn/dcgan.jpg)
![dcgan](assets/cnn/dcgan2.jpg)

### CoGAN - Coupled GAN

![cogan](assets/cnn/cogan.jpg)
![cogan](assets/cnn/cogan2.jpg)

## Transformer

- An encoder decoder architecture based on attention layers.
- One main difference is that the **input sequence can be passed parallelly**, so that **GPU** can be utilized effectively, and the speed of training can also be increased. And it is based on the multi-headed attention layer, vanishing gradient issue is also overcome by a large margin.
  ![Transformer](assets/trans/tr.jpg)
- <https://youtu.be/TQQlZhbC5ps>

![Transformer](https://miro.medium.com/max/875/1*57LYNxwBGcCFFhkOCSnJ3g.png)

### Encoder Block

![Encoder](assets/trans/tr_en.jpg)
Embedding Space: It’s like an open space or dictionary where words of similar meanings are grouped together or are present close to each other in that space.
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

- Useful in Text Translation/Summarization because we have the future words.
- Created by stacking multiple encoders of Transformer.

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

<https://colah.github.io/posts/2015-08-Understanding-LSTMs/>

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

## What Filters learns

<https://youtu.be/eL80Im8Hq0k>

![Filters](assets/cnn/filterz.jpg)

### Bilinear Interpolation

Upscalling technique

![Bilinear Interpolation](assets/cnn/Bilinear.jpg)

### Activation function and masking

![activation_mask](assets/cnn/activation_mask.jpg)

### Intersection over Union - IoU

A Metic messures overlap.

![iou](assets/cnn/iou.jpg)

We need a dataset with the image and its corresponding masks for every single object in the image.

We determine the IoU for each of the object masks and our mask. The largest IoU is the classification that our network produces.

## Depthwise Separable Convolution

A faster method of convolution with less computation power & parameters.

## CapsuleNet

## Siamese

- siamese cnn
- siamese lstm
- siamese bi-lstm
- siamese CapsuleNet

## Time series data
