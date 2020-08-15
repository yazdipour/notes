# ML

## Jupyter Tricks

- Multicursor support with `ALT`
- Big data analysis
  - [ipyparallel](https://github.com/ipython/ipyparallel) is a good option for simple map-reduce operations in python. We use it in rep to train many machine learning models in parallel
  - [pyspark](http://www.cloudera.com/documentation/enterprise/5-5-x/topics/spark_ipython.html)
  - spark-sql magic [%%sql](https://github.com/jupyter-incubator/sparkmagic)

```py
# To show Help/Man
?str.replace()
# IPython Magic Commands
# Full list https://ipython.readthedocs.io/en/stable/interactive/magics.html
%env: Set Environment Variables
# %env without any arguments lists all environment variables
%env OMP_NUM_THREADS
# The line below sets the environment variable
%env OMP_NUM_THREADS=4
# %run will execute and show the output from all code cells of the specified notebook or Python file
%run ./two-histograms.ipynb
%run ./two-histograms.py
# %load will replace the contents of the cell with an external script. You can either use a file on your computer as a source, or alternatively a URL.
%load ./hello_world.py
# %store: Pass variables between notebooks
data = 'this is the string I want to pass to different notebook'
%store data
del data # This has deleted the variable
# Now, in a new notebook…
%store -r data
print(data)
# %who: List all variables of global scope.
one = "for the money"
two = "for the show"
%who str #prints one two
# %%time will give you information about a single run of the code in your cell.
%%time
import time
for _ in range(1000): time.sleep(0.01) # sleep for 0.01 seconds
>> CPU times: user 21.5 ms, sys: 14.8 ms, total: 36.3 ms Wall time: 11.6 s
# %%timeit uses the Python timeit module which runs a statement 100,000 times (by default) and then provides the mean of the fastest three times.
import numpy
%timeit numpy.random.normal(size=100)
>> The slowest run took 7.29 times longer than the fastest. This could mean that an intermediate result is being cached.
100000 loops, best of 3: 5.5 µs per loop
# %%writefile magic saves the contents of that cell to an external file.
# %pycat does the opposite, and shows you (in a popup) the syntax highlighted contents of an external file.
%%writefile pythoncode.py
import x
...# saves in pythoncode.py
%pycat pythoncode.py # will load the file in the cell
# `%prun statement_name` will give you an ordered table showing you the number of times each internal function was called within the statement, the time each call took as well as the cumulative time of all runs of the function.
%prun some_useless_slow_function()
# Debugging with %pdb
%pdb
code here
# $Using LaTeX for forumlas
$P(A \mid B) = \frac{P(B \mid A)P(A)}{P(B)}$
```

## Topics

- Gensin Library
- Persian Stuff:
  - Hazm - NLP Preprocessor
  - Word2Vec-Doc2Vec
- ResNet50
- Xception
- Corpora:

  - Bijankhan
  - Persica
  - Hamshahri 1/2
  - Tnews

- https://paperswithcode.com/sota
- Facial Recongnition Database: https://www.kairos.com/blog/60-facial-recognition-databases
- Gensim (مانند LDA، LSI و یا Word2Vec) https://radimrehurek.com/gensim/
- https://keras.io/
- 100DaysOfMLCode: https://github.com/harshitahluwalia7895/100DaysOfMLCode
- Basic Concepts: https://github.com/yazdipour/notes/blob/master/assets/BasicConcepts.png
- WGet Kaggle Datasets in Google Driver:https://mh-salari.me/wqet-download/
- http://www.r2d3.us/visual-intro-to-machine-learning-part-1/
- https://github.com/xviniette/FlappyLearning
- https://deeplearnjs.org/
- https://community.cloud.databricks.com
- http://snap.stanford.edu/data/
- https://msropendata.com/
- https://www.deeplearning.ai/
- https://developers.google.com/machine-learning/crash-course/ml-intro
- http://playground.tensorflow.org
- https://www.ailab.microsoft.com/
- http://www.fast.ai/
- https://deepai.org/

## Job

- https://ai-jobs.net/

## Online IDE/CodeEditors

- https://notebooks.azure.com
- https://codelabs.developers.google.com/

## DataSets

- http://datasetsearch.research.google.com
- Iran Open DataSets: https://virgool.io/@NimaShafiezadeh/فهرست-سایتهای-ایرانی-که-دادههای-باز-منتشر-میکنند-zenlqrfgddkt
- https://gallery.azure.ai/
- [[2 Million Politicians tweet Dataset](https://pastebin.com/1beXduu0)
- 25 Datasets for Deep Learning in
  IoT](https://hub.packtpub.com/25-datasets-deep-learning-iot/)
- https://msropendata.com/
- http://data.okfn.org/data
- https://datproject.org/
- https://toolbox.google.com/datasetsearch
- https://rajpurkar.github.io/SQuAD-explorer/
- https://www.datasetlist.com/
- https://www.visualdata.io/
- https://www.datasetlist.com/

## Book

- https://github.com/RatulGhosh/awesome-machine-learning
- https://m2dsupsdlclass.github.io/lectures-labs/
- http://incompleteideas.net/book/the-book-2nd.html
- How can machine learning solve my problem? http://mbmlbook.com/toc.html
- https://www.automl.org/book/

## Farsi References

- [ترجمه فارسی اصطلاحات داده کاوی و غیره](https://github.com/shervinea/cheatsheet-translation/tree/master/fa)
- https://dataio.ir/
- By https://twitter.com/afshinea
  - https://github.com/afshinea/stanford-cs-229-machine-learning
  - یاگیری با نظارت: https://stanford.io/2O7zuqn
  - یادگیری بدون نظارت: https://stanford.io/2zU5TrI
  - یادگیری عمیق: https://stanford.io/2Ryuaum
  - نکات و ترفندهای یادگیری ماشین: https://stanford.io/2E08dS8
  - https://stanford.edu/~shervine/l/fa/teaching/cs-229/cheatsheet-supervised-learning
  - https://stanford.edu/~shervine/l/fa/teaching/cs-229/cheatsheet-unsupervised-learning
  - https://stanford.edu/~shervine/l/fa/teaching/cs-229/cheatsheet-deep-learning
  - https://stanford.edu/~shervine/l/fa/teaching/cs-229/cheatsheet-machine-learning-tips-and-tricks
  - https://stanford.edu/~shervine/l/fa/teaching/cs-230/cheatsheet-deep-learning-tips-and-tricks
  - https://stanford.edu/~shervine/l/fa/teaching/cs-230/cheatsheet-convolutional-neural-networks
  - https://stanford.edu/~shervine/l/fa/teaching/cs-230/cheatsheet-recurrent-neural-networks

## Tutorial

- https://ml-cheatsheet.readthedocs.io/en/latest/index.html
- https://lnkd.in/eJzXREq
- https://www.aparat.com/ma_keyvanrad
- https://aischool.microsoft.com/
- https://academy.microsoft.com/en-us/tracks/artificial-intelligence/
- [3D Visualization of a Convolutional Neural Network](http://scs.ryerson.ca/~aharley/vis/conv/)
- [GuiTeNet is a graphical user interface for (quantum) tensor networks](https://guitenet.github.io/)
- http://cs231n.github.io/
- https://lilianweng.github.io/lil-log/2018/02/19/a-long-peek-into-reinforcement-learning.html
- http://blog.class.vision/1397/04/اتصال-مستقیم-سرویس-کولب-google-colab-به-درایو-google-drive/
- [Introducing Wav2letter++](https://towardsdatascience.com/introducing-wav2latter-9e94ae13246)
- [Gans](http://blog.class.vision/1397/10/generative-adversarial-networks/)
- http://blog.class.vision/1397/11/chatbot-with-voice/
- http://onlinehub.stanford.edu/cs230
- http://deeplearning.ir/آموزش-شبکه-عصبی-بازگشتی-بخش-پنجم-معرفی/
- http://deeplearning.ir/آموزش-شبکه-های-عصبی-بازگشتی-recurrent-neural-networks-بخش-ا/
- http://deeplearning.ir/آموزش-شبکه-عصبی-بازگشتی-بخش-چهارم-معرف/
- http://deeplearning.ir/آموزش-شبکه-های-عصبی-بازگشتی-recurrent-neural-network-بخش-س/
- http://deeplearning.ir/آموزش-شبکه-های-عصبی-بازگشتی-recurrent-neural-networks-بخش-د

## Projects

- [Latest Deep Learning OCR with Keras and Supervisely in 15 minutes](https://hackernoon.com/latest-deep-learning-ocr-with-keras-and-supervisely-in-15-minutes-34aecd630ed8)
- [تشخیص پلاک فارسی خودرو](https://www.youtube.com/watch?v=Lb4IcGF5iTQ)
- http://winter96.class.vision/
- http://fall97.class.vision/
- [تشخیص تخلف در کارت های اعتباری](http://www.ai-man.ir/post/detecting-credit-card-fraud-using-machine-learning/)
- [آشنایی با چند مورد از رکامندر سیستم‌های اپن‌سورس](https://sokanacademy.com/blog/9043/آشنایی-با-چند-مورد-از-رکامندر-سیستم‌های-اپن‌سورس)
- [Liveness Detection with OpenCV](https://www.pyimagesearch.com/2019/03/11/liveness-detection-with-opencv/)
- [Traditional Face Detection With Python](https://realpython.com/traditional-face-detection-python/)
- https://www.pyimagesearch.com/2019/04/01/pan-tilt-face-tracking-with-a-raspberry-pi-and-opencv/
- http://blog.class.vision/1397/10/voice-style-transfer/
- http://blog.class.vision/1397/10/speech-emotion-recognition/
- http://blog.class.vision/1397/10/machine-translation/

## Books

Social Media Mining
http://dmml.asu.edu/smm/book/

Automate the Boring Stuff with Python
https://automatetheboringstuff.com/

Neural Networks and Deep Learning
http://neuralnetworksanddeeplearning.com/index.html

Natural Language Processing with Python
https://www.nltk.org/book/

DATA SCIENCE HANDBOOK
https://www.thedatasciencehandbook.com/get-the-book#2

## Basic Consepts

| ---                 | ---                                                                                                                                                                            |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MLP                 | Mutli layer perseptron                                                                                                                                                         |
| Ensemble learning   | multi time trying and group of models votes for final result!                                                                                                                  |
| Batch normalization | Normalization on layer which will help our algorithm to fine min loss faster! (minus avg and divide it with variance) (Have trainable parameters)                              |
| Data Dividing       | Train_Data 70%, Validation/Dev_Data 20%, Test_Data 10%                                                                                                                         |
| Cross Validation    | Split data in 10 parts, use one part as TestData and the rest for training, and then do the same process with another part. **_Not Usable for Deep learning [its expensive]_** |

## Confusion Matrix

![confusion](assets/confusion-matrix.png)

## Recommender systems

- Content-based filtering : Consider properties of Object and content of it
- Collaborative filtering : Use users opinion
- Hybrid Recommender systems

## Discriminative

1. Regression
2. Logistic regression
3. decision tree (Hunt)
4. neural network(traditional network, deep network)
5. Support Vector Machine(SVM)

## Generative

1. Hidden Markov model
2. Naive bayes
3. K-nearest neighbor(KNN)
4. Generative adversarial networks(GANs)

## ImageNet Models

- Classic: LeNet5, AlexNet, ZFNet, VGG(Nice structure, Bad Memory usage)
- Inception: (Idea: use )
- ResNet

## Image Classification

A core task in Computer Vision

- Challenges: Illumination, Deformation, Occlusion, Background clutter, Intraclass variation
- Never use pure k-Nearest Neighbor on images. Cause: Distance metrics on level of whole images can be very unintuitive
