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

## Keras

- Saving checkpoints while training model in Keras

  ```py
  filepath = "saved-model-{epoch:02d}-{val_acc:.2f}.hdf5"
  checkpoint = keras.callbacks.ModelCheckpoint(filepath, monitor='val_acc', verbose=1, save_best_only=False, mode='max')
  ```

- <https://github.com/yazdipour/SRU-deeplearning-workshop/>
- np.squeeze > Remove single-dimensional entries from the shape of an array.
- model = Sequential() > Standard MLP Model
- model.add(Dense(64 `hyperparameter - hidden neuron` , activation='relu', input=25 `input params - only for first layer`))
- Usually add softmax at the last layer `model.add(Dense(activiation='softmax'))` / softmax will normalize the result for us.
- model.summery() > will print model structure > ex. FC | (NONE `is mini_batch`, 64)
- `model.compile(loss=,optimizer=,metrics=,validation_split=0.2)`
