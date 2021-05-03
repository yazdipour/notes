# Classification

```py
from sklearn.linear_model import LogisticRegression,SGDClassifier
from sklearn.svm import SVC, LinearSVC, NuSVC
from sklearn.naive_bayes import MultinomialNB,BernoulliNB
```

## Linear Regression

ex. Predict House prize based on other houses properties and prize -> Draw random line -> try minimize error using Gradient Descent (least square).

```py
from sklearn import preprocessing, cross_validation, svm
from sklearn.linear_model import LinearRegression

X = np.array(df.drop(['label'], 1))
X = preprocessing.scale(X)
y = np.array(df['label'])

X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, y, test_size=0.2)
# classifier
clf = LinearRegression() #OR another algo clf = svm.SVR()
clf.fit(X_train, y_train)
confidence = clf.score(X_test, y_test)
print(confidence) #0.960000

# predict
forecast_set = clf.predict(X_lately)
```

`clf = LinearRegression(n_jobs=-1)` So here, you can specify exactly how many threads you'll want. If you put in -1 for the value, then the algorithm will use all available threads.

![](https://pythonprogramming.net/static/images/machine-learning/positive-correlation.png)

![](https://pythonprogramming.net/static/images/machine-learning/best-fit-slope.png)

![](https://pythonprogramming.net/static/images/machine-learning/best-fit-y-intercept.png)

```py
def best_fit_slope(xs,ys):
    m = (((mean(xs)*mean(ys)) - mean(xs*ys)) /
         ((mean(xs)**2) - mean(xs**2)))
    return m
```

### Regression - R Squared = Coefficient of Determination Theory

The distance between the regression line's y values, and the data's y values is the error, then we square that. The line's squared error is either a mean or a sum of this, we'll simply sum it.

![](https://pythonprogramming.net/static/images/machine-learning/squared-error-visual.png)

"r squared" comes in, also called the "coefficient of determination." The equation for this is

![](https://pythonprogramming.net/static/images/machine-learning/coefficient-of-determination-r-squared.png)

The equation is essentially 1 minus the division of the squared error of the regression line and the squared error of the mean y line. The mean y line is quite literally the mean of all of the y values from the dataset.

```py
def squared_error(ys_orig,ys_line):
    return sum((ys_line - ys_orig) * (ys_line - ys_orig))
def coefficient_of_determination(ys_orig,ys_line):
    y_mean_line = [mean(ys_orig) for y in ys_orig]
    squared_error_regr = squared_error(ys_orig, ys_line)
    squared_error_y_mean = squared_error(ys_orig, y_mean_line)
    return 1 - (squared_error_regr/squared_error_y_mean)
```

## K-Nearest Neighbors Classification

```py
from sklearn import preprocessing, cross_validation, neighbors
clf = neighbors.KNeighborsClassifier()
clf.fit(X_train, y_train)
accuracy = clf.score(X_test, y_test)
#
metrics.accuracy_score(y_train,ypre) #(TrainAcc going to be ==1)
metrics.accuracy_score(y_test,ypre) #(TestAcc is RIGHT)
```

K is a hyper-parameter. K is a number you can choose, and then neighbors are the data points from known data. We're looking for any number of the "nearest" neighbors. Let's say K = 3, so then we're looking for the two closest neighboring points. For example:

![](https://pythonprogramming.net/static/images/machine-learning/simple-classification-example-data-with-test-4.png)

In the above image, I circled the three nearest neighbors. In that case, all three were of the + class. K Nearest Neighbors is going to basically go to a majority vote based on the neighbors. In this case, all three neighbors were +, so this is 100% a + class. If 2 neighbors were red + and 1 was a black dot, we'd still classify this is a +, just with a bit less confidence. Note that, due to the nature of the vote, you will likely want to use an odd number for K, otherwise you may find yourself in a 50/50 split situation. There are ways to apply "weights" to the distance, to penalize more for greater distances, so then you could have an even number for K if you wanted.

### Euclidean Distance theory

Euclidean Distance is basically the main math behind K Nearest Neighbors.

![Euclidean](https://pythonprogramming.net/static/images/machine-learning/euclidean-distance.png)

```py
plot1 = [1,3]; plot2 = [2,5]
euclidean_distance = sqrt( (plot1[0]-plot2[0])**2 + (plot1[1]-plot2[1])**2 )
```

## Logistic Regression

ex. Divide two classes by a line -> random line til reduce sum of error with gradient descent (log lost method!)

```py
from sklearn.linear_model import LogisticReg
model=LogisticRegression()
model.fit(xtr,ytr)
accuracyTrain=model.score(xtr,ytr)
ypre=model.predict(xtest)
accuracy=metrics.accuracy_score(yte,ypre)
```

## SVM (Support vector machine) - SVC_lassifier

- [Simply Binary Classifier] - Possible for MultiClass:
  1. OVR - One Vs Rest [default]
  1. OVO - One Vs One
- Like LR find the best divider. The line with maximum distance from the classes. -> Find maximum distance with Gradient Descent or other algothims!
- The best separating hyperplane is defined as the hyperplane that contains the "widest" margin between support vectors. The hyperplane may also be referred to as a decision boundary.
- PROS: Good at dealing with high DIM data + Works well on small data sets
- CONS: Need all data to calculate + Picking the right kernel and parameters can be intensive

![svm](assets/svm.png)
![SVM](https://pythonprogramming.net/static/images/machine-learning/support-vector-machine-6.png)

```py
# clf = svm.SVC() #default
clf = svm.SVC(kernel='rbf', C=1, gamma=2**-5, decision_function_shape='ovr')
clf.fit(X_train, y_train)
confidence = clf.score(X_test, y_test)
```

### Vector

![Vector](https://pythonprogramming.net/static/images/machine-learning/vector-magnitude.png)

![Vector](https://pythonprogramming.net/static/images/machine-learning/vector-dot-product.png)

### Support Vector Assertions

<https://pythonprogramming.net/support-vector-assertions-machine-learning-tutorial/>

![SVM](https://pythonprogramming.net/static/images/machine-learning/svm-projection-classification.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/equation-for-support-vector.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/optimization-and-constraint-problem.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/support-vector-width.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/support-vector-width-step-1.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/support-vector-width-step-2.png)

![SVM](https://pythonprogramming.net/static/images/machine-learning/svm-formal-optimization.png)

That's looking pretty ugly, and, due to the alpha squared, we're looking at a quadratic programming problem.

The SVM's optimization problem is a convex problem, where the convex shape is the magnitude of vector w:

![optimization](https://pythonprogramming.net/static/images/machine-learning/optimization-steps.png)

### Gradient Descent

ex. Getting down from Mount. Height from ground. Goal is to get down easiest way. (Height is the error in Data Mining algorithms)

### Kernel Method

Like LR when can't divide it in 2D. Add Z param so we can divide them with Surface in 3D.

```py
[A(0,3),B(1,2),B(2,1),A(3,0)]
-> add Z=xy -> (x,y,xy)
Or in 2D divide with curve y=1/x
```

#### Popular SVM Kernel Functions

- Linear Kernel
- Gaussian Kernel - Gaussian Radial Basis Function (RBF)
- Sigmoid Kernel
- Bassel Kernel
- ANOVA kernel
- Radial Kernel (RBD)
- Polynomial Kernel

![Polynomial Kernel](https://i2.wp.com/dataaspirant.com/wp-content/uploads/2020/12/16-svc-classifier-using-polynomial-kernel.png?w=400&ssl=1)

### Soft Margin Support Vector Machine

First, there are two major reasons why the soft-margin classifier might be superior. One reason is your data is not perfectly linearly separable, but is very close and it makes more sense to continue using the default linearly kernel. The other reason is, even if you are using a kernel, you may wind up with significant over-fitment if you want to use a hard-margin. For example, consider:

![SoftMargin](https://pythonprogramming.net/static/images/machine-learning/linear-soft-margin-example.png)

![SoftMargin](https://pythonprogramming.net/static/images/machine-learning/new-svm-minimization-vector-w-slack.png)

## SVR (Support Vector Regression)

SVR is support vector regression.

```py
for k in ['linear','poly','rbf','sigmoid']:
    clf = svm.SVR(kernel=k)
    clf.fit(X_train, y_train)
    confidence = clf.score(X_test, y_test)
    print(k,confidence)
```

## Naive Bayse

ex. Spam Mail Detector
