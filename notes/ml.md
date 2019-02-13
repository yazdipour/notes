# Machine Learning

* Facial Recongnition Database: https://www.kairos.com/blog/60-facial-recognition-databases
* Gensim (مانند LDA، LSI و یا Word2Vec) https://radimrehurek.com/gensim/

## Discriminative

1:#Regression
2:#Logistic regression
3:#decision tree(Hunt)
4:#neural network(traditional network, deep network)  
5:#Support Vector Machine(SVM)

## Generative

1:#Hidden Markov model
2:#Naive bayes
3:#K-nearest neighbor(KNN)
4:#Generative adversarial networks(GANs)

## Dictionary

* Hyperparameter:
* MLP: Mutli layer perseptron
* Ensemble learning: multi time trying and group of models votes for final result!

## 9 Steps in becoming a Machine Learning Expert

1. Understand the basics
2. Learn Some Statics
3. Learn python for Data Analysis
4. Complete an Exploratory analysis project
5. Create Unsupervised learning models
6. Create supervised learning models
7. Understand big data technologies
8. Explorer deep learning models
9. Undertake and complete a data project

## Basic Concepts

https://github.com/yazdipour/notes/blob/master/assets/BasicConcepts.png

## 100DaysOfMLCode

https://github.com/harshitahluwalia7895/100DaysOfMLCode

## PyCon 2017

* Gensin Library
* Image Net
* Persian Stuff:
    * Hazm - NLP Preprocessor
    * Word2Vec-Doc2Vec
* ResNet50
* Xception
* Keras
* Corpora:
    * Bijankhan
    * Persica
    * Hamshahri 1/2
    * Tnews

## Basics from Udacity Youtube Videos

### Naive Bayse

ex. Spam Mail Detector

### Gradient Descent

ex. Getting down from Mount. Height from ground. Goal is to get down easiest way. (Height is the error in Data Mining algorithms)

### Regression Linear

ex. Predict House prize based on other houses properties and prize -> Draw random line -> try minimize error using Gradient Descent (least square).

### Logistic Regression

ex. Divide two classes by a line -> random line til reduce sum of error with gradient descent (log lost method!)

### SVM (Support vector machine)

Like LR find the best divider. The line with maximum distance from the classes. -> Find maximum distance with Gradient Descent or other algothims!

### Kernel Method

Like LR when can't divide it in 2D. Add Z param so we can divide them with Surface in 3D.

```py
[A(0,3),B(1,2),B(2,1),A(3,0)] -> add Z=xy -> (x,y,xy)
Or in 2D divide with curve y=1/x
```

### K-Means Clustering

ex. Know numbers of clusters = K. find K centers for K groups

### Hierarchical Clustering

ex. Like K-Means instead of K numbers of clusters, group objects with maximum distance that we defind, so we have unknown numbers clusters.

### K-Nearest Classification

* PYTHON Predict  > `n = Knearest(); n.fit(x,y); n.predict(X)`
* PYTHON Validate > `n.score(xtest,ytest)*100`
* K is a hyper-parameter.

# Neural Networks

Divide classes auto with weird shapes. (Is above Line1->TRUE | Is above Line2->FALSE ::-> TRUE ....)

* Perceptron (The biological neuron)
    * Simple Perceptron can handle Linear problems.
    * MLP (Multi layer perseptron) can handle more.
    * PARTS:
    * Input + BIAS (To avoid cases with ZERO inputs)
    * Output
    * Activation Function
    * Weights
* Neurons and Activation Functions
    * StepFunction: `z = wx + b (b for bias)` (Cons: Little changes doesn't have effect on final result)
    * Sigmoid (Curved Step fuction): `f(x)= 1/1+e^-x`  (Cons: In near infinity, Derivative is close to 0)
    * Hyperbolic Tangent: Tanh(z): `Tanh x=sinh x/cosh x` (Like Sigmoid Func)
    * ReLU: Rectified Linear Unit: `f(z)= max(0,z)`  `((z=0 in Negative Area and z=x in Positive Area))`
* Cost Functions
    * How bad is the model
    * y':=TrueValue, y=PredictedValue
    * `σ(z)=y < wx+b = z`
    * Simple Cost function: `C = Σ(y’-y)2 / n` (Cons: Slow Covergence)
    * Cross Entropy: `C = -Σ y’_i*log(y_i)` (Fast, Bigger Penalty on error changes)
        * This function helps to boost Learning Speed.
        * For `C` big, nueron learns faster.
        * ***If delta between TrainingLoss and TestLoss is alot, it is overftting***
* Gradient Descent
    * is a first-order iterative optimization algorithm for finding the minimum of ***the Cost function***.
    * To find a local minimum of a function using gradient descent, one takes steps proportional to the negative of the gradient of the function at the current point.
* Backpropagation
* DropOut: Killing random neuron on each epochs. / No Param to Learn

## Encoding / Representing class data

* One-hot encoding: Encode classes to Matrix of 1 and 0s.
    * Labels= ['shoe', 'shirt'] -> shirt == [0, 1]
    * Test=[0,1], Predict=[1,0]
    * Test2=[0,1], Predict2=[0,1]
    * -> (test*predict).sum() = 1 (1 wrong)

## Validation

* Data Dividing: Train_Data 70%, Dev_Data 20%, Test_Data 10%
* Cross Validation: Split data in 10 parts, use one part as TestData and the rest for training, and then do the same process with another part. ***Not Usable for Deep learning [its expensive]***

## Image Classification

A core task in Computer Vision

* Challenges: Illumination, Deformation, Occlusion, Background clutter, Intraclass variation
* k-Nearest Neighbor on images never used.
    * Distance metrics on level of whole images can be very unintuitive

# Deep Learning

* When there is >=3 hidden layers in NN.
* Layers Count := |Input+HiddenLayer|

1. CNN
2. RNN
3. LSTM
4. CapsuleNet
5. Siamese:
    * siamese cnn
    * siamese lstm
    * siamese bi-lstm
    * siamese CapsuleNet
6. Time series data

## CNN

Usually use ConvLayer at first layers, FC Layers for last ones and a softmax for last one.
* Fully Connected **FC**: NN with mesh connections between layers.
    * Why Not: Locality is not important in FC.
    * Why Not: Sometimes its imposible to compute all the connections.
* Pooling **POOL**: To make the input smaller but using Max/Min/Avg Pooling. With we make the input matrix in half. (No param to learn)
* Convolution **CONV**: Multipling different filters to the image.
    * Dense layers learn global patterns in their input feature space
    * Convolution layers learn local patterns
    * The patterns they learn are translation invariant
    * They can learn spatial hierarchies of patterns
    * ***Challenge***: After each multiple operation Centered Numbers in matrix have more effect on final result than cornered ones.
    * ***Solution***: Adding Padding (One Line Zero Padding)
    * Padding
        * Valid Convolution: Normal Convolution
        * Same Convolution: Convolution with add padding in each multiplation.
    * Stride: Number of Row*Columns to Skip on each multiplation.
    * Convolution Output: `[1+ (n+2p-f)/s] x [1+ (n+2p-f)/s]` ((nxn image, fxf filter, p padding, s stride)) (f,s are hyperparameter)
* “sandwich” architecture (SCSCSC...)
    * simple cells: modifiable parameters
    * complex cells: perform pooling
* RGB Conv
    * Do `R*f1 + G*f2 + B*f3 + BIAS` will result in 3D Filter. and then sweep it on the RGB Matrix. This will result in 4x4 matrix. Then we can learn proper filter with repeating the process with different filters.

## Optimizers

?

# Python

* https://github.com/yazdipour/SRU-deeplearning-workshop/
* np.squeeze > Remove single-dimensional entries from the shape of an array.
* model = Sequential() > Standard MLP Model
* model.add(Dense(64 `hyperparameter - hidden neuron` , activation='relu', input=25 `input params - only for first layer`))
* Usually add softmax at the last layer `model.add(Dense(activiation='softmax'))` / softmax will normalize the result for us.
* model.summery() > will print model structure > ex. FC | (NONE `is mini_batch`, 64)
* model.compile(loss=,optimizer=,metrics=,validation_split=0.2)