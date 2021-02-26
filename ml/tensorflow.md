# Tensorflow

## Tensor

| rank | object     |
| ---- | :--------- |
| 0    | scalar     |
| 1    | vector     |
| 2    | N×N matrix |
| >=3  | tensor     |

Why is it called TensorFlow?

- "stateful dataflow graphs"
- Sessions provides execution environments for Graphs to flow
- Tensors trained via mutation of Variables
- Models asked to make Predictions after Training

## Basics

```py
import tensorflow as tf
# creates nodes in a graph "construction phase"
x1 = tf.constant(5)
x2 = tf.constant(6)
result = tf.mul(x1,x2)
print(result) # no result > Just tensor structure
# defines our session and launches graph to calculate
with tf.Session() as sess:
    output = sess.run(result)
    print(output)

# ON GPU
with tf.Session() as sess:
  with tf.device("/gpu:1"):
    matrix1 = tf.constant([[3., 3.]])
    matrix2 = tf.constant([[2.],[2.]])
    product = tf.matmul(matrix1, matrix2)
```

## MNIST By Hand

```py
'''
input > weight > hidden layer 1 (activation function) > weights > hidden l 2 (activation function) > weights > output layer
compare output to intended output > cost or loss function (ex. cross entropy) optimization function (optimizer) > minimize cost (ex. AdamOptimizer....SGD, AdaGrad)
backpropagation
feed forward + backprop = epoch
'''

import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("/tmp/data/", one_hot = True) #oneHot 3=[0,0,0,1,0,0,0,0,0]

n_nodes_hl1 = 500
n_nodes_hl2 = 500
n_nodes_hl3 = 500
n_classes = 10
batch_size = 100

# height x width
# Notice that I have used [None,784] as a 2nd parameter in the first placeholder. This is an optional parameter. It can be useful, however, to be explicit like this. If you are not explicit, TensorFlow will stuff anything in there.
x = tf.placeholder('float', [None, 784])
y = tf.placeholder('float')
def neural_network_model(data):
    # (input* weight)+ biases
    hidden_1_layer = {'weights':tf.Variable(tf.random_normal([784, n_nodes_hl1])),
                      'biases':tf.Variable(tf.random_normal([n_nodes_hl1]))}
    hidden_2_layer = {'weights':tf.Variable(tf.random_normal([n_nodes_hl1, n_nodes_hl2])),
                      'biases':tf.Variable(tf.random_normal([n_nodes_hl2]))}
    hidden_3_layer = {'weights':tf.Variable(tf.random_normal([n_nodes_hl2, n_nodes_hl3])),
                      'biases':tf.Variable(tf.random_normal([n_nodes_hl3]))}
    output_layer = {'weights':tf.Variable(tf.random_normal([n_nodes_hl3, n_classes])),
                    'biases':tf.Variable(tf.random_normal([n_classes]))}
    l1 = tf.add(tf.matmul(data,hidden_1_layer['weights']), hidden_1_layer['biases'])
    l1 = tf.nn.relu(l1)
    l2 = tf.add(tf.matmul(l1,hidden_2_layer['weights']), hidden_2_layer['biases'])
    l2 = tf.nn.relu(l2)
    l3 = tf.add(tf.matmul(l2,hidden_3_layer['weights']), hidden_3_layer['biases'])
    l3 = tf.nn.relu(l3)
    return tf.matmul(l3,output_layer['weights']) + output_layer['biases']

def train_neural_network(x):
    prediction = neural_network_model(x)
    cost = tf.reduce_mean( tf.nn.softmax_cross_entropy_with_logits(logits=prediction, labels=y) )
    optimizer = tf.train.AdamOptimizer().minimize(cost)
    hm_epochs = 10
    with tf.Session() as sess:
        sess.run(tf.global_variables_initializer())

        for epoch in range(hm_epochs):
            epoch_loss = 0
            for _ in range(int(mnist.train.num_examples/batch_size)):
                epoch_x, epoch_y = mnist.train.next_batch(batch_size)
                _, c = sess.run([optimizer, cost], feed_dict={x: epoch_x, y: epoch_y})
                epoch_loss += c
            print('Epoch', epoch, 'completed out of',hm_epochs,'loss:',epoch_loss)

        correct = tf.equal(tf.argmax(prediction, 1), tf.argmax(y, 1))
        accuracy = tf.reduce_mean(tf.cast(correct, 'float'))
        print('Accuracy:',accuracy.eval({x:mnist.test.images, y:mnist.test.labels}))
```

### TensorBoard Callback

- Connect to TensorBoard <https://pythonprogramming.net/tensorboard-analysis-deep-learning-python-tensorflow-keras>

```py
from tensorflow.keras.callbacks import TensorBoard

NAME = "Cats-vs-dogs-CNN-{}".format(int(time()))
tensorboard = TensorBoard(log_dir="logs/{}".format(NAME))
...
model.fit(X, y, batch_size=32, epochs=3, validation_split=0.3,
          callbacks=[tensorboard])

# Go Terminal and type
# tensorboard --logdir=logs/ #log directory path
```

- Optimizing Models with TensorBoard - <https://pythonprogramming.net/tensorboard-optimizing-models-deep-learning-python-tensorflow-keras/>

## ModelCheckpoint Callback

Saving checkpoints while training model in Keras

```py
filepath = "saved-model-{epoch:02d}-{val_acc:.2f}.hdf5"
checkpoint = keras.callbacks.ModelCheckpoint(filepath, monitor='val_acc', verbose=1, save_best_only=False, mode='max')
```

# Keras

## MNIST in NN (not CNN)

It's generally a good idea to "normalize" your data. This typically involves scaling the data to be between 0 and 1, or maybe -1 and positive 1. In our case, each "pixel" is a feature, and each feature currently ranges from 0 to 255. Not quite 0 to 1. Let's change that with a handy utility function:

```py
(x_train, y_train), (x_test, y_test) = mnist.load_data()   # 28x28 numbers of 0-9
x_train = tf.keras.utils.normalize(x_train, axis=1).reshape(x_train.shape[0], -1)
x_test = tf.keras.utils.normalize(x_test, axis=1).reshape(x_test.shape[0], -1)
```

To show the image with color mapping:

```py
plt.imshow(x_train[0],cmap=plt.cm.binary)
plt.show()
```

A sequential model is what you're going to use most of the time. It just means things are going to go in direct order. A feed forward model. No going backwards...for now.

Recall our NN image? Was the input layer flat, or was it multi-dimensional? It was flat. So, we need to take this 28x28 image, and make it a flat 1x784.

Next, we want our hidden layers. We're going to go with the simplest NN layer, which is just a `Dense layer`. This refers to the fact that it's a densely-connected layer, meaning it's `"fully connected"`.

This layer has `128` units. The activation function is `relu`.

In final layer, our activation function is a `softmax` function, since we're really actually looking for something more like a probability distribution of which of the possible prediction options this thing we're passing features through of is.

```py
model = tf.keras.models.Sequential()
model.add(tf.keras.layers.Flatten())
model.add(tf.keras.layers.Dense(128, activation=tf.nn.relu))
model.add(tf.keras.layers.Dense(128, activation=tf.nn.relu))
model.add(tf.keras.layers.Dense(10, activation=tf.nn.softmax))
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
model.fit(x_train, y_train, epochs=3)
```

The `Adam optimizer` is just a great default to start with.

Next, we have our `loss metric`. Loss is `a calculation of error`. A NN doesn't actually attempt to maximize accuracy. It attempts to minimize loss. Again, there are many choices, but some form of categorical crossentropy is a good start for a classification task like this.

### Evaluate

Getting a high accuracy and low loss might mean your model learned how to classify digits in general (it `generalized`)...or it simply memorized every single example you showed it (it `overfit`). This is why we need to test on out-of-sample data (data we didn't use to train the model).

`val_loss, val_acc = model.evaluate(x_test, y_test)`

### Save and Load model

```py
model.save('epic_num_reader.model')
new_model = tf.keras.models.load_model('epic_num_reader.model')
```

### Predict

```py
predictions = model.predict(x_test)
print(np.argmax(predictions[0]))
# >> 7
# see the img
plt.imshow(x_test[0],cmap=plt.cm.binary)
plt.show()
```

## Cat or Dog CNN

- Loading Image & Resizing & Shuffling in <https://pythonprogramming.net/loading-custom-data-deep-learning-python-tensorflow-keras/>

  Now our data is just all dogs, then all cats. This will usually wind up causing trouble too, as, initially, the classifier will learn to just predict dogs always. Then it will shift to oh, just predict all cats! Going back and forth like this is no good either.

  `import random;random.shuffle(training_data)`

- CNN implementation - <https://pythonprogramming.net/convolutional-neural-network-deep-learning-python-tensorflow-keras/>

## X

- dropout?? https://www.tensorflow.org/api_docs/python/tf/keras/layers/Dropout
  max_pooling2d
  layers
  estimators
  optimzer
  metrics
  Calculate Loss (for both TRAIN and EVAL modes)
  loss = tf.losses.sparse_softmax_cross_entropy(labels=labels, logits=logits)

  - np.squeeze > Remove single-dimensional entries from the shape of an array.

## MIST RNN LSTM

```py
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout, LSTM

mnist = tf.keras.datasets.mnist  # 28x28 images
(x_train, y_train),(x_test, y_test) = mnist.load_data()
# normalizing
x_train = x_train/255.0
x_test = x_test/255.0

model = Sequential()

# IF you are running with a GPU, try out the CuDNNLSTM layer type instead (don't pass an activation, tanh is required)

model.add(LSTM(128, input_shape=(x_train.shape[1:]), activation='relu', return_sequences=True))
model.add(Dropout(0.2))

model.add(LSTM(128, activation='relu'))
model.add(Dropout(0.1))

model.add(Dense(32, activation='relu'))
model.add(Dropout(0.2))

model.add(Dense(10, activation='softmax'))

opt = tf.keras.optimizers.Adam(lr=0.001, decay=1e-6)

model.compile( loss='sparse_categorical_crossentropy', optimizer=opt, metrics=['accuracy'])

model.fit(x_train, y_train, epochs=3, validation_data=(x_test, y_test))
```
